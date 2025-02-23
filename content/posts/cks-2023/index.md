---
title: "Taking the CKS Kubernetes Security Specialist certification in 2023"
date: 2023-02-07T14:43:19+10:00
categories:
  - Cloud
tags:
  - kubernetes
  - openshift
thumbnail: "/img/cks2023thumb.png"
images:
  - https://bargenqua.st/img/cks2023thumb.png
toc: false
comments: true
---

Some time ago, I [wrote a post](https://bargenqua.st/posts/cks/) about my experiences studying for and undertaking the [Certified Kubernetes Security Specialist](https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/) exam. Well, the two year validity period for that certification expired for me this past week, and since I’m still floating through the world of Kubernetes in my daily job, I figured I’d attempt to re-acquire it.

Now that I’m on the tail-end of that experience with the certification back under my belt for another two years, it feels like a good opportunity to revisit this topic and provide some pointers for anyone looking to take (or re-take) the plunge themselves.

## Has the exam changed much?

Naturally, I won’t (and can’t) go into details of specific questions that the exam contains, but I found the exam experience in 2023 to be not much different to the experience I had in 2021 in terms of content, length or difficulty.

Content-wise, there are of course some changes. You can no longer expect any questions about Pod Security Policies, given its [deprecation](https://kubernetes.io/blog/2021/04/06/podsecuritypolicy-deprecation-past-present-and-future/) in 2021. You can additionally expect the Kubernetes environment to be at least v1.26 (at time of writing). You will not be asked anything that isn’t in some way covered in the list of expected competencies, but you can also safely anticipate not being tested on every single one of them, either.

The way that the exam is undertaken, however, is markedly different and now performed inside of a dedicated “secure browser” offered by the exam provider rather than a browser running locally. [This article](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e) goes over the changes in some detail. The secure browser was the source of much frustration for me when attempting the exam, resulting in over two hours of troubleshooting with their support team prior to me being able to commence the exam at all. However, my experiences may not be necessarily reflective of anyone else’s, so I will keep most of my thoughts on this experience isolated to a separate blog, if anything.

What I will note, though, is to pay attention to the [supported OSes](https://helpdesk.psionline.com/hc/en-gb/articles/4409608794260-PSI-Bridge-Platform-System-Requirements)! If you’re a Linux user, note that Ubuntu 18.04 and 20.04 are the only “supported” Linux OSes at this time. This means, if you have problems - as I did, running Fedora 37 - the tech support folks are likely to suggest that you just try with an OS that is supported.

## How to prepare?

I prepared by simply doing a quick 1.5x speed refresher of Killer Shell’s [CKS Udemy course](https://www.udemy.com/course/certified-kubernetes-security-specialist/), which was the same course that I prepared with back in 2021. I still consider this course to be of high quality, and I was quite pleased to note that it’s been updated with new tests for each chapter that operate within killercoda.com’s simulation environment.

The course content teaches you almost everything you’ll need to know, but more importantly it gives you the skills and knowledge to know how to troubleshoot and find answers to the things that the exam may test you on. Whether you’re studying the certification for the first time, or looking to re-certify, it’s a good option (and no, I’m not affiliated with the course in any way).

## Don’t forget the practice exams

Another big difference in 2023 is that purchasing the certification exam grants you access to two attempts at a practice CKS exam. The aforementioned Udemy course used to have practice exams, but now it seems that they’ve migrated that to become an official offering that comes with the CKS exam itself.

Actually finding the links to this exam is curiously challenging. I found it in my browser history by visiting this site, but that’s the only place I recall seeing the link, and I’ll be darned if I could navigate back to that page just by browsing around the training portal. I could just have completely overlooked something here - nevertheless, that’s where you’ll find it.

Don’t assume that the questions in the real exam will be exactly like the practice exam, or that even the same type of content will be covered. However, if you can confidently do the questions in the practice exam (and not through rote memorisation of answers), you’ll likely possess enough general knowledge to be able to deal with the real exam’s curveballs. The practice exam also tries to emulate the look and feel of the real exam environment as best as it can, too.

One thing I do want to note is that the practice exam comes with an extremely-well-done “solutions” section that walks through, step by step, the actions needed to answer the question and why they should be performed (or what to interpret from them). It makes a world of difference.

In short: definitely don’t forget to do the practice exam. At time of writing, once you “start” the exam you’ll have access to it for the next 36 hours, so it’s worth doing in the day or two leading up to your real exam.

## You don’t need to memorize bookmarks..

One mercifully good thing about the CKS exam is that you’re able to access relevant documentation. I linked to a lot of it in my last blog. There’s a [list of allowed resources](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-security-specialist-cks), but don’t worry, you don’t need to memorize these. If you’re asked a question where you might need to consult documentation more specific than just https://kubernetes.io/docs, you’ll likely be provided with a direct link to those docs in the question.

## ..but you should still be comfortable knowing where to find docs

You’re still going to have a much easier time of things if you can rapidly go from “I’ve been asked a question about X” to reading the most relevant documentation for it that’ll help you in the exam.

Use the practice exam as an opportunity to refine your documentation search terms and familiarise with the most helpful documentation.

## Know the API server

It is not a spoiler to say that in this exam you are going to be interacting with the kube-apiserver a lot. You’re going to be configuring it, troubleshooting it, restarting it, securing it.

Know how to configure the API server. Know where the docs are. Be sure you know how to get to [this page](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/) with all the configuration options on it.

Know where to look for logs, particularly if you find that the API server just isn’t starting up any more after you make a change. Remember: /var/log/containers/kube-apiserver* !

Know how to effect an API server restart if you need. Remember: moving the kube-apiserver.yaml file in and out of /etc/kubernetes/manifests will achieve this.

## Remember you get a re-take

Lastly, as mentioned in my [previous blog](https://bargenqua.st/posts/cks/), remember that you get two tries at this. That takes a load of pressure off the first attempt - it’s like getting a sneak peek at the exam before you have to take it! So try to keep those worries at bay. Unless it’s your second attempt, in which case - if you’ve done any of the preparation I’ve mentioned above, don’t worry, you’ll do great!
