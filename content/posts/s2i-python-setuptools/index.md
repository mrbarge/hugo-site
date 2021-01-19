---
title: "Keeping setuptools updated in OpenShift Python S2I"
date: 2021-01-19T20:42:00+10:00
draft: false
categories:
  - Cloud
  - Coding
tags:
  - openshift
  - python
thumbnail: "/img/s2i-python-setuptools.png"
images:
  - https://bargenqua.st/img/s2i-python-setuptools.png
---

After a recent commit to a Python project that I work on, I noticed that my resulting OpenShift pod had begun crashlooping after the rebuild.

A quick check of the pod logs showed why: for some reason, it could no longer find the `alembic` module, despite that being a transitive dependency of `SQLAlchemy`, which my project already had in its `requirements.txt`. 

Curious, I checked the build logs and noticed an odd error during the dependency install:

```bash
egg_info for package alembic produced metadata for project name unknown. 
Fix your #egg=alembic fragments.
```

A quick search revealed this to be a common issue experienced in a variety of modules, and the problem in all cases was universally that the version of [setuptools](https://pypi.org/project/setuptools/) being used was too old.

Fortunately, OpenShift has a quick and easy way to resolve this problem - you can instruct the S2I builder to update its own pip and setuptools modules before commencing the build of your application.

This is as easy as setting the `UPGRADE_PIP_TO_LATEST` environment variable to `true` in your OpenShift buildconfig.

```bash
oc set env bc/$BUILD_CONFIG_NAME UPGRADE_PIP_TO_LATEST=true
```

With this environment set and a new build triggered, I was once again greeted by my application running once more. Hope you find this tip useful!