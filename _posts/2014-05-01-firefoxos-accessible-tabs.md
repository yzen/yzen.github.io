---
layout: post
title: FirefoxOS Accessible Tabs
---

{{ page.title }}
================

<p class="meta">01 May 2014 - Toronto, ON</p>

Firefox OS accessibility has been one of the main focus items for our team for quite a while now. The *TODO* list is fairly [long](https://bugzilla.mozilla.org/buglist.cgi?j_top=OR&f1=blocked&o1=substring&resolution=---&query_based_on=the-big-list&o2=substring&query_format=advanced&f2=short_desc&v1=893789&v2=[AccessFu]&known_name=the-big-list&list_id=9909885) so it's important to prioritize the most impactful items. We recently completed making the *Tabs* widgets accessible across all Firefox OS applications.

*Tabs* is part of __Building Blocks__ - a collection of commonly used patterns in CSS, HTML and, eventually, Javascript that comprise different commonly used widgets such as *header, list, button, etc* (currently located [here](https://github.com/mozilla-b2g/gaia/tree/master/shared/style) in *Gaia* source code). This meant that by addressing *Tabs* accessibility we would improve accessibility of all *Gaia* apps that use them. It would also serve as a good accessible *Tabs* template for the upcoming apps that would need to use them.

Most of the changes were specific to HTML and CSS with a little extra Javascript work, all described below:

* *Tabs* in Gaia now use the following markup:

  ```
  <ul role="tablist" class="bb-tablist">
    <li role="presentation">
      <a id="tab1" href="#tabpanel1" role="tab" aria-controls="tabpanel1"
        aria-selected="false">Tab 1</a>
      <div id="tabpanel1" class="bb-tabpanel" role="tabpanel"
        aria-labelledby="tab1">Tab Panel 1</div>
    </li>
    ...
    <li role="presentation">
      <a id="tab2" href="#tabpanel1" role="tab" aria-controls="tabpanel2"
        aria-selected="true">Tab 2</a>
      <div id="tabpanel2" class="bb-tabpanel" role="tabpanel"
        aria-labelledby="tab2">Tab Panel 2</div>
    </li>
  </ul>
  // Note: elements with the role="tabpanel" do not have to be siblings of the
  // role="tab" elements.
  ```
* You can find the CSS, that *Tabs* in Gaia use, [here](https://github.com/mozilla-b2g/gaia/blob/master/shared/style/tabs.css). As you can see from the markup above and the corresponding CSS file, there is an explicit separation between the aria roles and the styling. This was done to address a common pitfall of using the aria roles as CSS selectors to obtain the necessary styling on elements with different semantics.

* The only Javascript bit that was required was related to handling <code>aria-selected</code> attribute between the list of tabs ([*accessibility_helper.js*](https://github.com/mozilla-b2g/gaia/blob/master/shared/js/accessibility_helper.js)). <code>AccessibilityHelper.setAriaSelected</code> would need to be called from the app code that is responsible for handling navigation between tabs.

As of right now, if an app implementation requires a *Tabs* widget, developers need to use the above markup, include the above CSS file as well as the [*accessibility_helper.js*](https://github.com/mozilla-b2g/gaia/blob/master/shared/js/accessibility_helper.js) file. And if they do, their users should be able to enjoy fully screen reader accessible *Tabs*.

yzen
