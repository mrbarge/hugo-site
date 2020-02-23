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
In this blog we're going to learn how we can use `kubectl`'s `patch` command to modify the configuration of Kubernetes-managed resources via the command-line. Before we do that though, we'll go through a quick primer on how you can display Kubernetes resources so that you know what and where to patch.

## Getting Kuberenetes resources

One of the first [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/) commands a Kubernetes beginner will become intimately acquainted with is the [get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. It displays all manner of different resources that Kubernetes is aware of, such as pods, deployments and secrets.

```bash {linenos=inline}
# kubectl get pods
NAME                           READY     STATUS    RESTARTS   AGE
appuio-php-docker-ex-1-build   1/1       Running   0          11s
```

In the example above, we can see that the default behaviour of the ``get`` command is to produce human-readable output. We can customize that behaviour with the use of the ``--output`` (or ``-o``) option to select from parseable formats such as [yaml](https://yaml.org/) and [json](https://www.json.org/). These formats are useful to view in order to understand how we can subsequently patch them. In the example below we are retrieving the list of Kubernetes projects, but in YAML form:

```bash {linenos=inline}
# kubectl get projects -o yaml
apiVersion: v1
items:
- apiVersion: project.openshift.io/v1
  kind: Project
  metadata:
    name: default
    namespace: ""
    resourceVersion: "1205"
  spec:
    finalizers:
    - kubernetes
```

We can even define our own output formats via [JSONPath](https://goessner.net/articles/JsonPath/index.html) or [Golang templates](https://golang.org/pkg/text/template/). These grant us the flexibility to specify the fields we want to see and how we wish to see them, making them useful for scenarios where we wish to feed the state of Kubernetes into other scripts. This is a useful technique to have at our disposal, so let's look at JSONPath in particular.

JSONPath is similar in concept to [jq](https://stedolan.github.io/jq/), a well-known CLI tool for interacting with JSON. JSONPath has a different syntax for querying the JSON, but largely achieves the same goals. In the simple exmaple below, we'll use JSONPath to pull back the project name for a project that happens to have a matching UID value. 

```bash {linenos=inline}
# kubectl get projects --output \
#    jsonpath='{.items[?(@.metadata.uid=="054dda83-4e53-11ea-aed8-000c29eb7917")].metadata.name}'
hello
```

However, if you're already quite familiar with ``jq``, you can of course pipe your json output to it instead and achieve the same goal:

```bash {linenos=inline}
# kubectl get projects --output json | \
#    jq '.items[] | select(.metadata.uid=="054dda83-4e53-11ea-aed8-000c29eb7917") | .metadata.name'
"hello"
```

There is an excellent and steadily-growing resource of creative ways to use ``kubectl`` and ``jsonpath`` to produce a concise summary of information over in this [github gist](https://gist.github.com/so0k/42313dbb3b547a0f51a547bb968696ba).

## Patching Kubernetes resources

Now that we know how to display Kubernetes resources, let's learn how we can modify them. ``kubectl`` provides the [patch](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#patch) command for exactly this purpose. What's more, it provides three different techniques for applying patches, each of which has advantages (or disadvantages) in certain situations. Whilst you might be able to get away with its default behaviour (the "*strategic merge*") for most scenarios, being aware of the other techniques is helpful. We're going to look at those alternate methods first, and then see how the default behaviour differs.

### Patching the JSON Merge way

JSON Merge is the first technique we'll explore, and - as the name would suggest - lets you merge new JSON into existing JSON document. To illustrate this with an example, let's first create a configmap:

```bash {linenos=inline}
# kubectl create configmap hello-config \
#    --from-literal=foo=bar --from-literal=beep=boop \
#    -o json
configmap/hello-config created
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

```bash {linenos=inline}
# kubectl patch configmap hello-config \
#     --type=merge -p '{"data": {"foo": "baz"}}' \
#     -o json
configmap/hello-config patched
{
    "apiVersion": "v1",
    "data": {
        "beep": "boop",
        "foo": "baz"
    },
    ... output trimmed ...
```   

If we supply previously non-existent JSON, it will just get merged straight in. The example below illustrates this, by adding an additional key-value pair:

```bash {linenos=inline}
# kubectl patch configmap hello-config \
#     --type=merge -p '{"data": {"new": "yes"}}'
#     -o json
configmap/hello-config patched
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

```bash {linenos=inline}
# echo """apiVersion: v1
# kind: LimitRange
# metadata:
#   creationTimestamp: 2020-02-16T11:51:35Z
#   name: core-resource-limits
#   namespace: myproject
# spec:
#   limits:
#   - max:
#       memory: 1Gi
#     min:
#       memory: 6Mi
#     type: Pod""" | oc create -f -
limitrange/core-resource-limits created
```

We'll now attempt to add a new array element for `containers` with the `merge` technique:

```bash {linenos=inline}
# kubectl patch limitrange core-resource-limits \
#     --type=merge -p '''
#         { "spec": 
#             { "limits": [ 
#                { "default" : { "memory": "200Mi"}, 
#                  "defaultRequest" : { "memory": "200Mi"}, 
#                  "type": "Container"}
#                ]
#             }
#         }''' \
#     -o yaml
"core-resource-limits" patched
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
* specify the `path` to the JSON where the patch is applied
* specify the `value` to be used in the patch

Here's an example below:

```json {linenos=inline}
[{ "op": "add", 
   "path": "/spec/containers/-", 
   "value": {
     "name": "php-hello-world", 
     "image": "php-hello-world-1.0" 
   }
}]
```

As we've seen earlier, the `JSON Merge` technique is poor for array operations, but this is a place in which `JSON Patch` excels. Using array-like indexing, we can be surgical about where in the array an item should be patched. Let's revisit our earlier `limitrange` patching example with a `JSON Patch` approach.

As you'll recall, our JSON looks like the example below.

```yaml {linenos=inline}
  limits:
  - max:
      memory: 1Gi
    min:
      memory: 6Mi
    type: Pod
```

We wish to add a new array element. We'll do so at the end of the array, indicated using the `-` symbol.

```bash {linenos=inline}
# kubectl patch --type=json \
#     limitrange core-resource-limits -p '''
#       [{ "op": "add", 
#           "path": "/spec/limits/-", 
#           "value": {
#             "defaultRequest" : {
#               "memory": "200Mi"
#             }, 
#             "type": "Container"
#       }}]''' \
#     -o yaml
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

```yaml {linenos=inline}
spec:
  containers:
    - name: httpd
      image: httpd-1.0
    - name: sidecar
      image: my-sidecar-1.0
```

and we wanted to patch the `image` value for the `sidecar` container, can we do so? If we were confident that it always appeared in the second position of the array, maybe, but we can't always make that assumption. The last technique we'll look at, the `Strategic Merge`, goes some way towards alleviating this issue.

By the way, if you're starting to get confused about JSON Patch and JSON Merge.. well, I don't blame you! But there is a [great resource](http://erosb.github.io/post/json-patch-vs-merge-patch/) that summarizes the differences between the two. 

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
* ..which contains a `containers` array of type [Container](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#container-v1-core), which defines a patch strategy of `merge` and a `merge key` of `name`.

The *merge key* is used as the distinguishing element between array field elements. Let's look at this in practice by attempting to patch a  `DaemonSet` example:

```yaml {linenos=inline}
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

The `name` field in the `containers` array is our merge key in this instance, uniquely identifying that particular array entry. We must therefore supply the `name` in our patch, alongside the value of `daemonset-example`. If we don't do that, our patch will be added in as a new array element instead of merging with the existing one.

Let's patch the array entry to change the command to `bash`. Our patch will look like the following:

```json {linenos=inline}
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

```bash {linenos=inline}
kubectl patch daemonset daemonset-example -p "$(cat patch.json)" -o yaml
```

and can subsequently observe that the command portion of the array entry has changed to:

```yaml {linenos=inline, linenostart=17}
        command:
        - /bin/bash
```

If we provided a different value of `name`, for instance `new-daemonset-example`, our patch would instead try to create a second list element using our patch. In our example, this would actually fail because our patch would be missing a required field:

```bash
The DaemonSet "daemonset-example" is invalid: 
  spec.template.spec.containers[0].image: Required value
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

```bash
# kubectl patch dc/hello-world -p "$(cat mypatch.yaml)"
```

### OpenShift/OKD and patching

We've been referring to `kubectl` above, but if you're a user of [Red Hat OpenShift](https://www.openshift.com) or [OKD](https://www.okd.io), do note that the `oc` client behaves in the same manner and that all examples are cross-compatible.

### Why are there so many different ways to mess with JSON data?

Sorry friend, you're asking the wrong person there. 

### For more reading

* [The official Kubernetes documentation on patching](https://kubernetes.io/docs/tasks/run-application/update-api-object-kubectl-patch/)
* [More about strategic merge patching](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/strategic-merge-patch.md)

---
