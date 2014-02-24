---
layout: post
title: TIL Debugging Mochitests.
---

{{ page.title }}
================

<p class="meta">24 Feb 2014 - Toronto, ON</p>

Turns out there's an easy way to debug Chrome JS in mochitests, as described by Gijs Kruitbosch in his blog: [Debugging Chrome JS and Mochitest Redux](http://www.gijsk.com/blog/2013/10/debugging-chrome-js-and-mochitests-redux/). All you need to do is to use the <code>--jsdebugger</code> flag. Your tests will start with the debugger enabled by default and stopped before their execution. You can add breakpoints on the fly or use the <code>debugger;</code> command in your JavaScript code.

Here's an example of running some of the a11y tests from your _gecko-dev_ directory:

<code>
./mach mochitest-a11y --jsdebugger accessible/tests/mochitest/jsat/
</code>

yzen
