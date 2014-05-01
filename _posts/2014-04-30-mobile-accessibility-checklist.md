---
layout: post
title: Mobile Accessibility Checklist
---

{{ page.title }}
================

<p class="meta">30 Apr 2014 - Toronto, ON</p>

*This is a concise checklist of accessibility requirements for mobile developers. It is intended to continuously evolve as more patterns arise.*
<br>
Colour
------

* Colour contrast **MUST** comply with [WCAG 2.0](http://www.w3.org/TR/WCAG/) AA Level requirement
    * Contrast ratio of 4.5:1 for normal text (less than 18 point or 14 point bold)
    * Contrast ratio of 3:1 for large text (at least 18 point or 14 point bold)
    * [Colour Checker](http://snook.ca/technical/colour_contrast/colour.html)
* Information conveyed via colour **MUST** be also available by other means (underlined text for links, etc)

<br>
Visibility
----------
* Hiding techniques such as zero opacity, z-index order and off-screen placement **MUST NOT** be used exclusively to handle visibility
* Everything other than the current visible screen **MUST** be *truly* invisible (especially relevant for single page apps with multiple *cards*)
    * **USE** ```hidden``` attribute or ```visibility``` or ```display``` style properties
    * Unless absolutely unavoidable, ```aria-hidden``` attribute **SHOULD NOT** be necessary

<br>
Focus
-----

* All activatable elements **MUST** be focusable
    * Standard controls such as links, buttons, form fields are focusable by default
    * Non standard controls **MUST** have an appropriate *role* attribute assigned to them: ```button, link, checkbox``` etc ([ARIA Roles](http://www.w3.org/TR/wai-aria/roles))
* Focus should be handled in a logical order and consistent manner

<br>
Text Equivalents
----------------

* Text equivalent **MUST** be provided for every non strictly presentational non-text element within the app
    * Use *alt* and *title* where appropriate (*UPDATE*: See Steve Faulkner's post about [Using the HTML title attribute](http://blog.paciellogroup.com/2013/01/using-the-html-title-attribute-updated/))
    * If the above attributes are not applicable use attributes such as ```aria-label, aria-labelledby or aria-describedby``` ([ARIA Properties](http://www.w3.org/WAI/PF/aria/states_and_properties#global_states_header))
* Images of text **MUST** be avoided
* All form controls **MUST** be labeled for the screen reader user

<br>
Handling State
--------------
* Standard controls such as radio buttons and checkboxes are handled by the operating system. However,
for other custom controls state changes must be provided via aria states: ```aria-checked, aria-disabled, aria-selected, aria-expanded, aria-pressed``` ([ARIA States](http://www.w3.org/TR/wai-aria/states_and_properties#attrs_widgets_header))

<br>
General Guidelines
------------------

* An app title **MUST** be provided
* Headings **MUST** not break hierarchical structure
    * ```
      <h1>Top level heading</h1>
        <h2>Secondary heading</h2>
        <h2>Another secondary heading</h2>
          <h3>Low level heading</h3>
      ```
* Aria landmarks **SHOULD** be used to describe an app or document structure: ```banner, complementary, contentinfo, main, navigation, search``` ([ARIA Landmark Roles](http://www.w3.org/TR/wai-aria/roles#landmark_roles_header))
* Touch event handlers **MUST** only be triggered on touchend event
* Touch targets **MUST** be large enough for the user to interact with ([BBC Mobile Accessibility Guidelines](http://www.bbc.co.uk/guidelines/futuremedia/accessibility/mobile/design/touch-target-size))
