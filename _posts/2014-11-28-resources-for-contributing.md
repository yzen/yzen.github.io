---
layout: post
category: firefoxos
title: Resources For Contributing to Firefox OS Accessibility.
---

{{ page.title }}
================

<p class="meta">28 Nov 2014 - Toronto, ON</p>

I believe when contributing to **Firefox OS** and *Gaia*, just like with most open source projects, a lot of attention should be given to reducing the barrier for entry for new contributors. It is even more vital for *Gaia* since it is an extremely fast moving project and the number of things to keep track of is overwhelming. In an attempt to make it easier to start contributing to Firefox OS Accessibility I compiled the following list of resources, that I will try keeping up to date. It should be helpful for a successful entry into the project:

Firstly, links to high level documentation:

* [Developing *Gaia*](https://developer.mozilla.org/en-US/Firefox_OS/Developing_Gaia)
* [*dev-gaia* mailing list](https://lists.mozilla.org/listinfo/dev-gaia)

===
Git
===

*Gaia* project is hosted on [**Github**](https://github.com/) and the version control that is used is [**Git**](http://www.git-scm.com/). Here's a link to the project source code:

[*https://github.com/mozilla-b2g/gaia/*](https://github.com/mozilla-b2g/gaia/)

One of my coworkers (James Burke) proposed the following workflow that you might find useful ([link to source](https://bugzilla.mozilla.org/show_bug.cgi?id=1068713#c12)):

* Fork *Gaia* using Github UI (I will use my *Github* user name - <code>yzen</code> as an example)
* From your fork of *Gaia* ([*https://github.com/yzen/gaia*](https://github.com/yzen/gaia)), clone that locally, and set up a "remote" that is called "upstream" that points to the mozilla-b2g/gaia repo:

```shell
    git clone --recursive git@github.com:yzen/gaia.git gaia-yzen
    cd gaia-yzen
    git remote add upstream git@github.com:mozilla-b2g/gaia.git
```

* For each bug you are working on, create a branch to work on it. This branch will be used for the pull request when you are ready. So taking this bug number *123* as an example, and assuming you are starting in your clone's *master* branch in the project directory:

```shell
    # this updates your local master to match mozilla-b2g's latest master
    # you should always do this to give better odds your change will work
    # with the latest master state for when the pull request is merged
    git pull upstream master

    # this updates your fork on github's master to match
    git push origin master

    # Create bug-specific branch based on current state of master
    git checkout -b bug-123
```

* Now you will be in the `bug-123` branch locally, and its contents will look the same as the `master` branch. The idea with bug-specific branches is that you keep your master branch pristine and only matching what is in the official *mozilla-b2g* branch. No other local changes. This can be useful for comparisons or rebasing.

* Do the changes in relation to the bug you are working on.

* Commit the change to the branch and then push the branch to your fork. For the commit message, you can just copy in the title of the bug:

```shell
    git commit -am "Bug 123 - this is the summary of changes."
    git push origin bug-123
```

* Now you can go to [*https://github.com/yzen/gaia*](https://github.com/yzen/gaia) and do the pull request.

* In the course of the review, if you need to do other commits to the branch for review feedback, once it is all reviewed, you can flatten all the commits into one commit, then force push the change to your branch. I normally use <code>rebase -i</code> for this. So, in the <code>gaia-yzen</code> directory, while you are in the *bug-123*, you can run:

```shell
    git rebase -i upstream/master
```
At this point, git gives you a way to edit all the commits. I normally *'pick'* the first one, then choose *'s'* for squash for the rest, so the rest of the commits are squashed to the first picked commit.

Once that is done and git is happy, you can the force push the new state of the branch back to *GitHub*:

```shell
    git push -f origin bug-123
```

More resources at:

* [Making *Gaia* code changes](https://developer.mozilla.org/en-US/Firefox_OS/Developing_Gaia/Making_Gaia_code_changes)
* [Submitting a Gaia patch](https://developer.mozilla.org/en-US/Firefox_OS/Developing_Gaia/Submitting_a_Gaia_patch)

===========
Source Code
===========

* All apps are located in *apps/* directory. Each up is located within its own directory. So for example if you are working on a *Calendar* app you would be making your changes in the *apps/calendar* directory.

* The way we want to make sure that the improvements that we work on actually help *Firefox OS* accessibility and do not regress we have a policy of adding *gaia-ui* python Marionette tests for all new accessible functionality. You can find tests in the *tests/python/gaia-ui-tests/gaiatest/tests/accessibility/* directory.

More resources at:

* [Understanding the *Gaia* codebase](https://developer.mozilla.org/en-US/Firefox_OS/Developing_Gaia/Understanding_the_Gaia_codebase)

=========================
Building and Running *Gaia*
=========================

* [Different ways to run *Gaia*](https://developer.mozilla.org/en-US/Firefox_OS/Developing_Gaia/Different_ways_to_run_Gaia)
* [*Gaia* build system primer](https://developer.mozilla.org/en-US/Firefox_OS/Developing_Gaia/Build_System_Primer)

=======
Testing
=======

* [Testing *Gaia* code changes](https://developer.mozilla.org/en-US/Firefox_OS/Developing_Gaia/Testing_Gaia_code_changes)
* [*Gaia* unit tests](https://developer.mozilla.org/en-US/Firefox_OS/Platform/Automated_testing/Gaia_unit_tests) used for low level unit testing.
* [*Gaia* integration tests](https://developer.mozilla.org/en-US/Firefox_OS/Platform/Automated_testing/Gaia_integration_tests) used for higher level integration tests.
* [*Gaia* UI tests](https://developer.mozilla.org/en-US/Firefox_OS/Platform/Automated_testing/gaia-ui-tests) used for higher level integration tests. All accessibility tests are written as *Gaia* UI tests.

============
Localization
============

Localization is very relevant to accessibility especially because one of the tasks that we perform when making something accessible is ensuring that all elements in the applications are labeled for the user of assistive technologies. Please see [Localization best practices](https://developer.mozilla.org/en-US/Firefox_OS/Developing_Gaia/localization_code_best_practices) for guidelines on how to add new text to applications.

=========
Debugging
=========

* [Debugging Firefox OS](https://developer.mozilla.org/en-US/Firefox_OS/Debugging)
* [WebIDE](https://developer.mozilla.org/en-US/docs/Tools/WebIDE)
* [Mulet](https://developer.mozilla.org/en-US/Firefox_OS/Developing_Gaia/Different_ways_to_run_Gaia#Using_Gaia_in_Firefox_Mulet)

=====================
Using a screen reader
=====================

Using a device or navigating a web application is different with the screen reader. Screen reader introduces a concept of virtual cursor (or focus) that represents screen reader's current position inside the app or web page. For mode information and example videos please see: [Screen Reader](https://wiki.mozilla.org/Accessibility/Mobile/ScreenReader)

=============
Accessibility
=============

Here are some of the basic resources to help you get to know what mobile accessibility (and accessibility) is:

* [Mobile Accessibility Checklist](http://yzen.github.io/firefoxos/2014/04/30/mobile-accessibility-checklist.html)
* [ARIA](http://www.w3.org/WAI/intro/aria)

yzen
