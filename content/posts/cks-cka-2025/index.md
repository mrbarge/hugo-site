---
title: "Thoughts on taking the Kubernetes CKS and beta CKA exams in 2025"
date: 2025-02-22T14:54:14+10:00
draft: false
categories:
  - Cloud
tags:
  - kubernetes
  - ai
thumbnail: "/img/cks-cka-2025.png"
images:
  - https://bargenqua.st/img/cks-cka-2025.png
toc: false
comments: true
---

Goodness, how time flies... Two years have passed since my last CKS-related blog post—enough time for my certification to expire. So, I guess it's time to dust off the ol' Hugo template and write about it again! I recently renewed my Certified Kubernetes Security Specialist certification in February and also had the opportunity to beta-test the 2025 revision of the Certified Kubernetes Administrator exam. How have things changed for both of these? Read on to find out.

## The virtual exam experience

I dedicated a sizable portion of my [last post](https://bargenqua.st/posts/cks-2023/) to bemoaning the virtual exam environment... so buckle up, because I'm about to do it again! This time, I attempted the exam on a Mac Mini running an up-to-date macOS. In theory, this should not have been a problem. It passed the PSI Online compatibility pre-checks, so I went into the exam brimming with confidence in a trouble-free experience. In practice, however, I launched the exam but was unable to proceed because it detected a running `SideCarRelay` process on my system. I have no idea what that is, but PSI Online apparently does—and they don't like it.

Troubleshooting random system issues is the last thing anyone wants to do before a tricky and stressful exam, but that was my reality. Killing the process only caused it to respawn. I tried renaming the underlying binary, but macOS decided my `sudo` wasn't quite `sudo` enough to let me do that. Some frantic searching followed, all while under the time pressure of needing to start the exam within 30 minutes or risk it being marked as a fail. Numerous results suggested various fixes, including disabling iCloud components and screen mirroring, none of which worked. Finally, mercifully, I found a small post suggesting I disable Bluetooth. However, both my keyboard and mouse were Bluetooth devices!

After frantically hunting for a wired keyboard and mouse with the correct ports—the Mac Mini has only two USB-A ports, one of which was occupied by the required webcam, meaning I had to find a USB-C mouse—I eventually disabled Bluetooth. After a reboot, I was finally able to permanently kill SideCarRelay and proceed with the exam.

The next ten minutes were spent giving the anonymous exam proctor a webcam tour of my room and body cavities, which at least gave me time to catch my breath before diving into the two-hour exam completely frazzled. Suffice it to say, this was not an ideal start.

Once inside the exam, things were mostly stable, except for a ten-minute period where my network connection started lagging, turning commands like `k get deploy` into `k get ddddddddddeploy`. Not exactly what you want when time is tight. This may have been an issue on my or my ISP's end, though I regularly use remote desktop software and rarely experience similar problems.

TL;DR: If you're on a Mac and can't get rid of `SideCarRelay`, try turning off Bluetooth.

## The CKS exam in 2025

The CKS underwent a [refresh](https://training.linuxfoundation.org/cks-program-changes/) in October 2024, introducing some [important changes](https://www.youtube.com/watch?v=3YWLuidA2JI). These changes were included in my exam, so expect them in yours. Notably, you should familiarize yourself with Software Bill of Materials (SBOM) generation and Cilium network policies.

Fortunately, the exam still includes a complementary practice test provided by [Killer Shell](https://killer.sh). Much like my 2023 experience, I found it to be excellent and thorough. If you don't attempt the practice exam at least once and review the solutions afterward, you're doing yourself a great disservice. I firmly believe that mastering it adequately prepares you for the real exam.

That said, time management is crucial. I was confident in almost every question, yet I still ran out of time before finishing everything. _Have a time management strategy in place and use it_. Here's what worked for me (your approach may vary):

- **Questions are not ordered by difficulty**. Easier ones may be at the end. Check ahead and prioritize those you can answer without consulting documentation. Flag tougher ones for later.
- **Skim ahead but don't overdo it**. Reviewing all the questions at the start wastes time. Instead, I aimed to stay aware of the next five or so questions.
- **Know when to move on**. If you're stuck for more than a few minutes, flag the question and return to it later. Don't get bogged down.
- **Don't wait for stuff to finish, keep working**. For example, if you've changed `/etc/kubernetes/manifests/kube-apiserver.yaml` and are waiting for everything to restart, move on to another question in the meantime, and return later to verify everything worked.

For me, the biggest learning curve was [Cilium network policies](https://docs.cilium.io/en/latest/security/policy/index.html). The excellent [online network policy editor](https://editor.networkpolicy.io/) helped me construct different scenarios and translate them into policies. If you want to experiment in a live environment, Killer Coda offers a free [Cilium playground](https://killercoda.com/killer-shell-cks/scenario/playground-cilium).

## The refreshed CKA exam in 2025

In January, I had the opportunity to beta-test the revised 2025 _Certified Kubernetes Administrator_ exam. My understanding is that the 2025 changes were [planned to go live](https://training.linuxfoundation.org/certified-kubernetes-administrator-cka-program-changes/) on February 18, though I'm unsure if that has happened. Regardless, please note that my opinions here are based on the beta, and the final exam may differ.

I found the CKA exam to be even more of a time crunch than the CKS. My time expired with several questions left unanswered, largely due to:

- **Poor time management**. I spent too long on individual questions instead of moving on. I took the CKA before the CKS, and it was a wake-up call to improve my approach.

- **Lack of familiarity with some topics**. I needed to consult external documentation but didn't realize some external sites were allowed. Although they weren't on the overall list of permitted resources, certain questions explicitly stated their documentation could be used. This may be clarified in the final version of the exam.

On the whole, while I believe the exam is achievable within the time limit, there is very little room for leisurely searching through documentation.

As for content, the new exam incorporated updated curriculum topics. I was particularly pleased with the changes, as the questions were more challenging and avoided rote repetition of documentation examples. For instance, one question required installing a cluster—similar to previous versions of the CKA—but this time, it had to be configured with automatic modifications. These adjustments make the certification more reflective of real-world administrative scenarios.

## The obligatory AI bit, and, is it all worth it?

If there's one sure thing that can derail any discussion in the year of 2025, it's AI. When I last did these exams, the current AI trend felt very much in its nascency. Nowadays it's a different story, and it's been on my mind as I reflect upon completing both exams, and the overall value of certifications.

I feel relatively confident that an AI could pass these exams, if one could be wired up to interact with an interactive `kubectl` prompt. Whether that heralds the death of Kubernetes administration as a stable career choice, I'm neither here nor there. 

For my part, I do these certifications because I enjoy throwing myself into these sort of testing situations and assessing whether I can still operate under some degree of pressure, on a topic that I feel I can speak about with some degree of authority.  Does completing both of these mean I'm a Kubernetes administration guru? Most certainly not. Would possessing a CKA or CKS certification be a major factor that sways my choice to hire one candidate over another? Goodness gracious no. Still, I find that these sort of certifications are a good, goal-driven way to inspire someone towards achieving a skill or mastery in something.. and if that helps motivate someone to seek and learn rather than depend upon a chatbot.. right now I'm all for it.

(Article thumbnail credit: [Jay Gomez](https://unsplash.com/photos/a-dog-sitting-in-a-chair-outside-b61qEKQIVNc))