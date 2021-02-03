---
title: "Everything you need to know about the CKS Kubernetes Security Specialist certification (except the answers)"
date: 2021-02-03T20:01:00+10:00
draft: false
categories:
  - Cloud
tags:
  - kubernetes
  - openshift
thumbnail: "/img/cksthumb.png"
images:
  - https://bargenqua.st/img/cksthumb.png
toc: false
---

Having just passed the exam myself, I wanted to do a write-up whilst many of these thoughts are fresh in my mind. Disclaimer: opinions are my own, not my employer's, etc.

## What is it?

The [Certified Kubernetes Security Specialist](https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/) (CKS) is a certification course offered by the Linux Foundation. It builds on the skills required by the Certified Kubernetes Administrator (CKA) certification with a focus on Kubernetes and cloud security. It’s a relatively new certification, having been released in November 2020, and requires the practitioner to firstly hold an active CKA certification.

## What does it cover?

As the name would imply, primarily Kubernetes security. That covers a whole gamut of topics, ranging from properly securing the Kubernetes API server through to the security of container images running as application workloads. The full curriculum of topics the certification expects practitioners to be well-versed in is [available online](https://github.com/cncf/curriculum).

## Do I need it?

I’m not about to wade into the debate about the overall value of certifications, or what they might say (or don’t say) about a person’s abilities. Personally, I possess an almost Funko Pop-like obsession in collecting them because I simply quite enjoy putting myself into exam pressure environments.. but that’s just me.

However, if we look at this from the angle of:

_“I’m a Kubernetes administrator, do I need to know the material this certification assesses?”_

then I would say yes, with an asterisk attached. Many topics in the curriculum (API server, RBAC, Pod security contexts, Audit) are ones that I feel every Kubernetes administrator should have a good working grasp of. Others, such as image vulnerability scanning or user workload static analysis, are ones that I’d argue are somewhat less important, if only because there are a growing number of third-party tools and providers that are doing a great job of that, and I suspect it's going to be a rapidly changing landscape. That said, it's all still very relevant knowledge to possess.

## Is it harder than CKA?

Exam difficulty is obviously going to be a subjective feeling, so I’ll be speaking purely personal feelings here. When comparing it to its CKA companion, which I found to be quite straightforward, the CKS exam definitely felt harder in comparison. However, the style of questions is mostly the same - with each question there is very little ambiguity about what you need to do, and there aren’t many “tricks” to mess with you - you just need to get on with it.

Like the CKA, the exam is “open book”, in so far as you will be able to browse the Kubernetes documentation (and a set of other tool-specific documentation URLs) in a separate tab. You can relax knowing that you’re not going to need to memorize the structure of an AdmissionController resource YAML and recite it by heart - so long as you know where to find examples in the documentation. For that reason I recommend preparing your bookmarks ahead of time. I will provide my own personal “exam prep” bookmarks later in this blog.

What I found most challenging with the CKS was the time pressure. This is the first certification exam I’ve done where I ran out of time before I could even attempt every question. Granted, part of that was because I got caught up on debugging two questions due to silly mistakes, but even ignoring that I still feel that it’s a pretty packed two hours. This is not an exam where you’ll have much time freedom to read up on topics mid-exam  - you’ll be expected to have a good handle on the material and just use the docs for the quick-reference type of stuff.

## Studying for the exam

If you are looking for a more guided preparation, there are a few paid courses which are available to help you prepare. The following are ones that I tried:

* The Linux Foundation offer their own [Kubernetes Security Essentials](https://training.linuxfoundation.org/training/kubernetes-security-essentials-lfs260/) training course, which can be bundled with the exam itself.

* [killer.sh](killer.sh)'s [Udemy CKS course](https://www.udemy.com/course/certified-kubernetes-security-specialist/).

Both will assuredly teach you everything you need to know, but if I had to choose between them - and again, this is purely a personal perspective - I'd go with killer.sh's offering. I found it to be a much more presentable approach divided equally between theory and practice. It also includes an exam simulation environment that is very similar to the experience of doing the CKS exam itself. 

I'll also note that Kim Wuestkamp, the author of the killer.sh course, is producing a [series of free helper guides](https://wuestkamp.medium.com/) for CKS topics, so that might be worth checking out.

## Exam tips 

* The usual exam tips apply. Get a good sleep first. Resist the urge to stress and last-minute-cram unless that’s just Your Thing. Have a bottle of water with you. Don’t do what I did and schedule it for 9pm on a Monday night.

* Prepare your exam environment ahead of time. I’ve done many remote-proctored exams, but the CKS one was particularly strict about ensuring my environment was clear of clutter. This is definitely the first time I’ve needed to completely remove my audio speakers from my desk and cover a second monitor with a towel! Not really things you want to be improvising moments before an exam.

* Pick the high-ranking questions to do first. Each question will have a % weight attached in regards to how much it contributes to your overall score. As I mentioned, time is of the essence in this exam - skim through all the questions at the start of the exam and attack the heaviest-weighted ones first. (also note that the heaviest-weighted ones are not necessarily always going to be the hardest!)

* Don’t stress out! I'm pretty sure that - like the CKA - if you fail the CKS you get a free re-try. So remember that the stakes are very low for that first attempt - even if you fail, you’ll be going into the second attempt with a _huge_ advantage.

* Prepare your Kubernetes documentation bookmarks ahead of time. More on that at the end of the blog.

## Just one more thing..

Good luck! You've got this! 👍

## Appendix: The big list of CKS bookmarks

Here's my handy list of bookmarks on topics relevant to the CKS material. Each of these links is allowable to be viewed during the exam.

* Admission Controllers
  * https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/
  * https://kubernetes.io/blog/2019/03/21/a-guide-to-kubernetes-admission-controllers/#why-do-i-need-admission-controllers
  * https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#imagepolicywebhook

* AppArmor
  * https://kubernetes.io/docs/tutorials/clusters/apparmor/#example

* API Server
  * https://kubernetes.io/docs/concepts/security/controlling-access/
  * https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/
  * https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/

* Audit
  * https://kubernetes.io/docs/tasks/debug-application-cluster/audit/

* Dashboard
  * https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/README.md
  * https://github.com/kubernetes/dashboard/blob/master/docs/common/dashboard-arguments.md

* General knowledge
  * https://kubernetes.io/docs/tasks/configure-pod-container/configure-volume-storage/
  * https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
  * https://kubernetes.io/docs/concepts/configuration/secret/

* Etcd encryption
  * https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/

* Falco
  * https://falco.org/docs/rules/supported-fields/

* Network ingress
  * https://kubernetes.io/docs/concepts/services-networking/ingress/

* Network policies
  * https://kubernetes.io/docs/concepts/services-networking/network-policies/
  * https://kubernetes.io/docs/tasks/administer-cluster/declare-network-policy/

* OpenPolicyAgent
  * https://kubernetes.io/blog/2019/08/06/opa-gatekeeper-policy-and-governance-for-kubernetes/

* Pod security
  * https://kubernetes.io/docs/concepts/policy/pod-security-policy/
  * https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.20/#podsecuritycontext-v1-core
  * https://kubernetes.io/docs/tasks/configure-pod-container/security-context/

* RBAC
  * https://kubernetes.io/docs/reference/access-authn-authz/rbac/

* Runtime classes
  * https://kubernetes.io/docs/concepts/containers/runtime-class/

* Scheduling
  * https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/

* Seccomp
  * https://kubernetes.io/docs/tutorials/clusters/seccomp/

* Service accounts
  * https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
  * https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/

* Users
  * https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/

* Upgrading
  * https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/

