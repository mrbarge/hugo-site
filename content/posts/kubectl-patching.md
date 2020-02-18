---
title: "Patching Kubernetes resources with kubectl"
date: 2020-02-17T21:02:21+10:00
draft: false
categories:
  - Cloud
tags:
  - json
  - kubernetes
  - openshift
thumbnail: "/img/teddypatch.jpg"

---
## Getting Kuberenetes resources

One of the first [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/) commands a Kubernetes beginner will become intimately acquainted with is the [get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. It displays all manner of different resources that Kubernetes is aware of, such as pods, deployments and secrets.

```
-bash-4.2$ kubectl get pods
NAME                           READY     STATUS    RESTARTS   AGE
appuio-php-docker-ex-1-build   1/1       Running   0          11s
```

In the example above, we can see that the default behaviour of the ``get`` command is to produce human-readable output. We can customize that behaviour with the use of the ``--output`` (or ``-o``) option to select from more parseable formats such as [yaml](https://yaml.org/), [json](https://www.json.org/), [jsonpath](https://goessner.net/articles/JsonPath/index.html) and even [golang templates](https://golang.org/pkg/text/template/). 

The latter two in particular grant us the flexibility to hone in on the fields we want to see and how we wish to see them, making them useful for scenarios where we wish to provide the state of Kubernetes into a broader script or automation process.

JSONPath is similar in concept to [jq](https://stedolan.github.io/jq/), the CLI tool that should be in every engineer's toolbelt. JSONPath has a different way of interrogating the json, but achieves the same goals. In the simple exmaple below, we're pulling back the project name for any project that happens to have a matching UID value.

```
-bash-4.2$ kubectl get projects --output jsonpath='{.items[?(@.metadata.uid=="054dda83-4e53-11ea-aed8-000c29eb7917")].metadata.name}'
hello
```

However, if you're already quite familiar with ``jq``, you can of course pipe your json output to it instead and achieve the same goal:

```
 kubectl get projects --output json | jq '.items[] | select(.metadata.uid=="054dda83-4e53-11ea-aed8-000c29eb7917") | .metadata.name'
"hello"
```

There is an excellent and steadily-growing resource of creative ways to use ``kubectl`` and ``jsonpath`` to produce a concise summary of information over in this [github gist](https://gist.github.com/so0k/42313dbb3b547a0f51a547bb968696ba).

## Patching Kubernetes resources

``kubectl`` also provides the [patch](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#patch) command, which allows for on-the-fly alterations to Kubernetes resources. What's more, it provides three different techniques for performing patches, each of which has advantages in specific situations.

The default behaviour is what's known as the `strategic merge`, but before we take a look at that, let's see what else `kubectl` has to offer. 

### Patching the JSON Merge way

JSON Merge is the first technique we'll explore, and - as the name would suggest - lets you merge new JSON into existing JSON document. To illustrate this with an example, let's first create a configmap:

```
-bash-4.2$ kubectl create configmap hello-config --from-literal=foo=bar --from-literal=beep=boop
configmap/hello-config created
```

And then display it:

```
-bash-4.2$ kubectl get configmap hello-config -o json
{
    "apiVersion": "v1",
    "data": {
        "beep": "boop",
        "foo": "bar"
    },
    "kind": "ConfigMap",
    "metadata": {
        ... output trimmed ...
    }
}
```

To use the JSON Merge technique when patching, we must provide the `--type=merge` argument, and then supply the JSON to merge in. If we want to change the value of the `foo` key, we can simply supply that portion of the JSON:

```
-bash-4.2$ kubectl patch configmap hello-config --type=merge -p '{"data": {"foo": "baz"}}'
-bash-4.2$ kubectl get configmap hello-config -o json
{
    "apiVersion": "v1",
    "data": {
        "beep": "boop",
        "foo": "baz"
    },
    ... output trimmed ...
```   

Previously non-existent JSON that is supplied will just get merged straight in. The example below illustrates this by adding an additional key-value pair:

```
-bash-4.2$ kubectl patch configmap hello-config --type=merge -p '{"data": {"new": "yes"}}'
configmap/hello-config patched
-bash-4.2$ kubectl get configmap hello-config -o json
{
    "apiVersion": "v1",
    "data": {
        "beep": "boop",
        "foo": "baz",
        "new": "yes"
    },
    ... output trimmed ...
```

There is a catch, however! When you use this technique on JSON arrays it will replace the entire array, rather than merge a new item into it. Let's see that with an example.

We'll start with a `limitrange` definition for `pods`:

```
spec:
  limits:
  - max:
      memory: 1Gi
    min:
      memory: 6Mi
    type: Pod
```

We'll now attempt to add a new array element for `containers` with the `merge` technique:

```
-bash-4.2$ kubectl patch limitrange core-resource-limits --type=merge -p '{"spec": { "limits": [ { "default" : { "memory": "200Mi"}, "defaultRequest" : { "memory": "200Mi"}, "type": "Container"}]}}' -o yaml

spec:
  limits:
  - default:
      memory: 200Mi
    defaultRequest:
      memory: 200Mi
    type: Container
```

Our entire array has been replaced by the new item, which we clearly don't want. How can we perform patches on arrays non-destructively? Our remaining two `kubectl` patching methods cater for that.

More information on the JSON Merge technique can be read about [in RFC7386](https://tools.ietf.org/html/rfc7386).

### Patching, the JSON Patch way

The next technique we'll look at is known as the [JSON Patch](https://tools.ietf.org/html/rfc6902). This allows for a more sophisticated ability to manipulate the JSON by allowing us to be explicit about the technique we wish to perform (`add`, `remove`, `replace`, `move` and `copy`) and what we wish to see affected.

To apply the `JSON Patch` technique, we need to:

* inform `kubectl` via the `--type=json` argument.
* specify the operation taking place (`replace`, `add`, `move`, and so on)
* specify the path to the JSON where the patch is applied
* specify the value to be used in the patch

```
[
  { "op": "add", "path": "/spec/containers/-", "value": {"name": "php-hello-world", "image": "php-hello-world-1.0" }
]
```

As we've seen earlier, the `JSON Merge` technique is poor for array operations, but this is a place in which `JSON Patch` excels. Using array-like indexing, we can be surgical about where in the array an item should be patched. Let's revisit our earlier `limitrange` patching example with a `JSON Patch` approach.

As you'll recall, our JSON looks like the example below.

```
  limits:
  - max:
      memory: 1Gi
    min:
      memory: 6Mi
    type: Pod
```

We wish to add a new array element. We'll do so at the end of the array, indicated using the `-` symbol.

```
-bash-4.2$  kubectl patch --type=json limitrange core-resource-limits -p '[{ "op": "add", "path": "/spec/limits/-", "value": {"defaultRequest" : {"memory": "200Mi"}, "type": "Container"}}]' -o yaml

spec:
  limits:
  - max:
      cpu: "2"
      memory: 1Gi
    min:
      cpu: 200m
      memory: 6Mi
    type: Pod
  - defaultRequest:
      memory: 200Mi
    type: Container
```

As you can see, both the existing and the new element are present within the array.

There is one weakness with JSON Patch and array operations, however. We must know beforehand precisely where we want to operate on the array. We cannot, for example, search for the correct position to apply a patch based on the array's sub-elements. 

If we had a pod spec as follows:

```
spec:
  containers:
    - name: httpd
      image: httpd-1.0
    - name: sidecar
      image: my-sidecar-1.0
```

and we wanted to patch the `image` value for the `sidecar` container, can we do so? If we were confident that it always appeared in that position in the array, maybe, but we can't always make that assumption. The last technique we'll look at, the `Strategic Merge`, goes some way towards alleviating this issue.

By the way, if you're starting to get confused about JSON Patch and JSON Merge.. well, I don't blame you! But there is a [http://erosb.github.io/post/json-patch-vs-merge-patch/](great resource) that summarizes the differences between the two. 

### Patching strategically

The `Strategic Merge` is the default behaviour of `kubectl`. That is to say, if you don't specify a `--type` at all, it'll be interpreted as a strategic merge.

`Strategic Merge`s look similar to `JSON Merge`s, but are more array-aware through the application of a *patch strategy*. The patch strategy dictates what happens when a patch is applied to an array and is 

* `merge`
* `replace`
* `delete`

You can look up whether an array resource definition has a patch strategy defined in the [Kubernetes API Documentation]([https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#podspec-v1-core]). If there isn't one defined, the default strategy is to `replace` the array.

Look at the [documentation](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#daemonset-v1-apps) for the `DaemonSet` resource definition as an example. We can see that:

* The `spec` sub-field is a [DaemonSetSpec](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#daemonsetspec-v1-apps), which contains a `template` struct of type [PodTemplateSpec](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#podtemplatespec-v1-core).. 
* ..which contains a `spec` struct of type [PodSpec](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#podspec-v1-core)..
* ..which contains a `containers` array of type [Container](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#container-v1-core), which a patch strategy of `merge` and a `merge key` of `name`.

The *merge key* is used as the distinguishing element between array field elements. Continuing our look at the `DaemonSet` resource, let's follow an example of patching an example:

```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: daemonset-example
spec:
  selector:
    matchLabels:
      app: daemonset-example
  template:
    metadata:
      labels:
        app: daemonset-example
    spec:
      containers:
      - name: daemonset-example
        image: ubuntu:trusty
        command:
        - /bin/sh
        args:
        - -c
        - >-
          while [ true ]; do
          echo "DaemonSet running on $(hostname)" ;
          sleep 10 ;
          done```
```

The `Containers` merge key of `name` means that if we want to change the existing `daemonset-example` array entry, we must supply the `name` in our patch as the identifying key, along with the corresponding matching value. If we don't do that, our patch will be added in as a new list element instead.

Let's patch the array entry to change the command to `bash`. Our patch will look like the following; note we have included `name` as our merge key value:

```
{ "spec": 
  { "template": 
    { "spec": 
      { "containers": 
        [ { "name": "daemonset-example", "command": [ "/bin/bash" ] } ] 
      } 
    } 
  } 
}
```

We can apply it as follows:

``` 
kubectl patch daemonset daemonset-example -p "$(cat patch.json)" -o yaml
```

and can subsequently observe that the command portion of the array entry has changed to:

```
        command:
        - /bin/bash
```

If we provided a different value of `name`, for instance `new-daemonset-example`, our patch would instead try to create a second list element using our patch. In our example, this would actually fail because our patch would be missing a required field:

```
The DaemonSet "daemonset-example" is invalid: spec.template.spec.containers[0].image: Required value
```

You might be wondering: what happens if you're operating on an array that doesn't seem to have a patch strategy defined? The default behaviour is to *replace* the list - in essence, the same behaviour that we observe with `JSON Merge`. Therefore, it is prudent to check what patch strategy might exist before rushing into performing a strategic merge operation on a list.

To fully discuss the `strategic` technique is well beyond the scope of this article. However, the best documentation I have seen on the topic is available [here](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/strategic-merge-patch.md).

## The fine print

### Look before you leap 

Patching a Kubernetes resource with ``patch`` is a venture that's risky. There's no backups kept, and no preserved history of your previous state. Whilst ``kubectl`` will protect you from outright corruption of the structural integrity of the resource (for example, by supplying improperly-formatted JSON), the changes are immediate and may impact running workloads.

It may be wise to employ use of the ``--dry-run`` and ``--output`` parameters to see what your requested change would have done without actually carrying it out.

### YAML is fine too

In the examples above, we've supplied JSON representations of the various patches we've wanted to apply. But if you're more of a YAML person, you're in luck! YAML will work just as well. 

Because YAML is a newline-oriented format, the easiest way to supply it is by writing the patch to a file and then passing it to `kubectl` via a subshell:

```
kubectl patch dc/hello-world -p "$(cat mypatch.yaml)"
```

### OpenShift/OKD and patching

We've been referring to `kubectl` above, but if you're a user of [Red Hat OpenShift](https://www.openshift.com) or [OKD](https://www.okd.io), do note that the `oc` client behaves in the same manner and that all examples are cross-compatible.

### For more reading

* [The official Kubernetes documentation on patching](https://kubernetes.io/docs/tasks/run-application/update-api-object-kubectl-patch/)
* [More about strategic merge patching](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/strategic-merge-patch.md)

---
