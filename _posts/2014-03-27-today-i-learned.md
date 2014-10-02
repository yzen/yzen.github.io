---
layout: post
category: firefoxos
title: TIL Running Gaia tests on Try.
---

{{ page.title }}
================

<p class="meta">27 Mar 2014 - Toronto, ON</p>

After getting some *Gaia* unit test failures on **Try** when one of my pull requests was merged in, I discovered how to use **Try** to test my pull request branch myself. This is a pretty important time saver for myself and anyone else who has to deal with my mistakes. So here are the instructions:

Prerequisits:
------------

* Commit Level 1
* Have your [pull request] *Gaia* branch handy.
* Have a local mercurual repository for  mozilla central.

Instructions:
------------

* You need to modify the following file in your mozilla central source <code>b2g/config/gaia.json</code> from:

```json
{
    "git": {
        "git_revision": "",
        "remote": "",
        "branch": ""
    },
    "revision": "57c407d3e94ba322688b4bd121eda317806ab44e", // Current rev.
    "repo_path": "/integration/gaia-central"
}
```

to

```json
{
    "git": {
        "git_revision": "",
        // Replace with your own gaia remote.
        "remote": "https://github.com/yzen/gaia.git",
        // Replace with the [pull request] branch you want to test.
        "branch": "969553"
    },
    "revision": "57c407d3e94ba322688b4bd121eda317806ab44e", // Current rev.
    "repo_path": "/integration/gaia-central"
}
```

* The correct *trychooser* message is:

<code>try: -b o -p linux64_gecko,linux32_gecko,macosx64_gecko -u all -t none</code>

* That's it! When you push to **Try**, the tests will run against your branch instead of the current */integration/gaia-central* revision.

yzen
