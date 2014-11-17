---
layout: post
category: firefoxos
title: TIL Debugging Gaia with B2G Desktop and WebIDE.
---

{{ page.title }}
================

<p class="meta">24 Oct 2014 - Toronto, ON</p>

With some great help from Rob Wood from Mozilla Firefox OS Automation team, I finally managed to get **Gaia** up and running and ready for debugging with [B2G Desktop Nightly](http://nightly.mozilla.org/#Desktop Boot2Gecko) build and [WebIDE](https://developer.mozilla.org/en-US/docs/Tools/WebIDE).

It is currently [impossible](https://bugzilla.mozilla.org/show_bug.cgi?id=1070830) to develop / debug **Gaia** using Firefox for Desktop. Thus, it's a pretty big barrier for new contributors who are just starting out with **Gaia**. Turns out, it is fairly easy to run **Gaia** codebase with *B2G Desktop* build. Here are the instructions:

Prerequisites:
------------

* Download and install [B2G Desktop Nightly](http://nightly.mozilla.org/#Desktop Boot2Gecko) build
* Download and install [Firefox for Desktop Nightly](http://nightly.mozilla.org/#Desktop) build
* Check out **Gaia** code base: <code>git clone https://github.com/mozilla-b2g/gaia.git</code>

Instructions:
------------

* In your **Gaia** repository build a **Gaia** user profile from scratch:
<code>make</code>

* Run the following command to start the *B2G Nightly* build with **Gaia** profile that you just built:
<code>/path/to/your/B2G/b2g-bin -profile /path/to/your/gaia/profile -start-debugger-server [PORT_NUMBER]</code>
For example: <code>/Applications/B2G.app/Contents/MacOS/b2g-bin -profile /Users/me/gaia/profile -start-debugger-server 7000</code>

* Start [Firefox for Desktop Nightly](http://nightly.mozilla.org/#Desktop) build

* Open *WebIDE* (*Tools -> Web Developer -> WebIDE*)

* Press *Select Runtime -> Remote Runtime*

* Replace the port with the one used in step 2 (<code>7000</code>) and click OK

* A dialog should pop up within the *B2G* emulator asking to permit remote debugging. Press OK

* At this point you should have access to all apps bundled with the profile as well as the Main Process via WebIDE

* When you make changes to **Gaia** code base, you can run <code>make</code> again to rebuild your profile. **Hint:** if you are working on a single app, just run <code>APP=my_app make</code> to only rebuild the app.

yzen
