# Explainer for Scroll Promises

This proposal is an early design sketch by Blink Interactions Team to describe the problem below and solicit
feedback on the proposed solution. It has not been approved to ship in Chrome.

## Proponents
- Blink Interactions Team

## Participate
- https://github.com/explainers-by-googlers/promisify-scroll/issues
- https://github.com/w3c/csswg-drafts/issues/1562

## Table of Contents [if the explainer is longer than one printed page]

<!-- Update this table of contents by running `npx doctoc README.md` -->
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Introduction](#introduction)
- [Goals](#goals)
- [Non-goals](#non-goals)
- [Use cases](#use-cases)
<!--
- [[Potential Solution]](#potential-solution)
  - [How this solution would solve the use cases](#how-this-solution-would-solve-the-use-cases)
    - [Use case 1](#use-case-1-1)
    - [Use case 2](#use-case-2-1)
- [Detailed design discussion](#detailed-design-discussion)
  - [[Tricky design choice #1]](#tricky-design-choice-1)
  - [[Tricky design choice 2]](#tricky-design-choice-2)
- [Considered alternatives](#considered-alternatives)
  - [[Alternative 1]](#alternative-1)
  - [[Alternative 2]](#alternative-2)
- [Stakeholder Feedback / Opposition](#stakeholder-feedback--opposition)
- [References & acknowledgements](#references--acknowledgements)
-->

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Introduction

Web developers currently have no way to know when a programmatic [smooth-scroll](https://drafts.csswg.org/cssom-view/#concept-smooth-scroll) has completed.  A solution to the problem that has already been resolved in the CSS WG: make the programmatic scroll methods return `Promise` objects that get resolved on scroll completion.  This explainer provides details of the solution, for spec updates and implementation.

## Goals

We have six scroll methods available through both [`Element`](https://drafts.csswg.org/cssom-view/#extension-to-the-element-interface) and [`Window`](https://drafts.csswg.org/cssom-view/#extensions-to-the-window-interface) interfaces.  These methods return immediately with the value `undefined`, which was fine during the early days of the web when scroll was assumed to be instant.  This behavior no longer seems adequate from a web developer's perspective today: there is widespread support for `smooth-scroll` (see [browser_compatibility](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-behavior#browser_compatibility) for the CSS property), and it is not easy for the developers to determine when a particular call for a smooth-scroll has completed.

This explainer elaborates how to make those methods return `Promise` objects to solve this problem, as per the CSS WG resolution in https://github.com/w3c/csswg-drafts/issues/1562.

## Non-goals

- Details of smooth-scroll behavior or chaining of nested scrollers.
- Alternatives to returning `Promise` objects.

## Use cases

### Disabled UI during smooth-scroll

Imagine a custom scroller that relies on programmatic scroll and that its buttons get disabled while a smooth-scroll is ongoing.

## Solution

The CSS WG resolution in https://github.com/w3c/csswg-drafts/issues/1562 proposes that the scroll methods available in [`Element`](https://drafts.csswg.org/cssom-view/#extension-to-the-element-interface) and [`Window`](https://drafts.csswg.org/cssom-view/#extensions-to-the-window-interface) interfaces return `Promise` objects (instead of `undefined`).  This would modify the spec IDLs as follows:
```IDL
partial interface Window {
  Promise<undefined> scrollIntoView(optional (boolean or ScrollIntoViewOptions) arg = {});
  Promise<undefined> scroll(optional ScrollToOptions options = {});
  Promise<undefined> scroll(unrestricted double x, unrestricted double y);
  Promise<undefined> scrollTo(optional ScrollToOptions options = {});
  Promise<undefined> scrollTo(unrestricted double x, unrestricted double y);
  Promise<undefined> scrollBy(optional ScrollToOptions options = {});
  Promise<undefined> scrollBy(unrestricted double x, unrestricted double y);
}

partial interface Element {
  Promise<undefined> scrollIntoView(optional (boolean or ScrollIntoViewOptions) arg = {});
  Promise<undefined> scroll(optional ScrollToOptions options = {});
  Promise<undefined> scroll(unrestricted double x, unrestricted double y);
  Promise<undefined> scrollTo(optional ScrollToOptions options = {});
  Promise<undefined> scrollTo(unrestricted double x, unrestricted double y);
  Promise<undefined> scrollBy(optional ScrollToOptions options = {});
  Promise<undefined> scrollBy(unrestricted double x, unrestricted double y);
}
```

### How this solution would solve the use cases

[If there are a suite of interacting APIs, show how they work together to solve the use cases described.]

#### Use case 1

```JS
  element.scrollBy({top: 500, behavior: "smooth"}).then(() => {
     // Do something at the end of the scroll.
  });
```



<!--
## Detailed design discussion

### [Tricky design choice #1]

[Talk through the tradeoffs in coming to the specific design point you want to make.]

```js
// Illustrated with example code.
```

[This may be an open question,
in which case you should link to any active discussion threads.]

### [Tricky design choice 2]

[etc.]
-->

<!--
## Considered alternatives

[This should include as many alternatives as you can,
from high level architectural decisions down to alternative naming choices.]

### [Alternative 1]

[Describe an alternative which was considered,
and why you decided against it.]

### [Alternative 2]

[etc.]
-->

<!--
## Stakeholder Feedback / Opposition

[Implementors and other stakeholders may already have publicly stated positions on this work. If you can, list them here with links to evidence as appropriate.]

- [Implementor A] : Positive
- [Stakeholder B] : No signals
- [Implementor C] : Negative

[If appropriate, explain the reasons given by other implementors for their concerns.]
-->

<!--
## References & acknowledgements

[Your design will change and be informed by many people; acknowledge them in an ongoing way! It helps build community and, as we only get by through the contributions of many, is only fair.]

[Unless you have a specific reason not to, these should be in alphabetical order.]

Many thanks for valuable feedback and advice from:

- [Person 1]
- [Person 2]
- [etc.]
-->
