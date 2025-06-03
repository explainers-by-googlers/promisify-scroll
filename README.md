# Explainer for Scroll Promises

**Instructions for the explainer author: Search for "todo" in this repository and update all the
instances as appropriate. For the instances in `index.bs`, update the repository name, but you can
leave the rest until you start the specification. Then delete the TODOs and this block of text.**

This proposal is an early design sketch by Blink Interactions Team to describe the problem below and solicit
feedback on the proposed solution. It has not been approved to ship in Chrome.

TODO: Fill in the whole explainer template below using https://tag.w3.org/explainers/ as a
reference. Look for [brackets].

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
<!--
- [User research](#user-research)
-->
- [Use cases](#use-cases)
  - [Use case 1](#use-case-1)
  - [Use case 2](#use-case-2)
<!--
- [[Potential Solution]](#potential-solution)
-->
  - [How this solution would solve the use cases](#how-this-solution-would-solve-the-use-cases)
    - [Use case 1](#use-case-1-1)
    - [Use case 2](#use-case-2-1)
<!--
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

Web developers currently have no way to know when a programmatic [smooth-scroll](https://drafts.csswg.org/cssom-view/#concept-smooth-scroll) has completed.  A solution to the problem that has already been resolved in the CSS WG (https://github.com/w3c/csswg-drafts/issues/1562): make the programmatic scroll methods return `Promise` objects that get resolved on scroll completion.  This explainer provides details of the solution for spec updates and implementation.

## Goals

We have six scroll methods available through both [`Element`](https://drafts.csswg.org/cssom-view/#extension-to-the-element-interface) and [`Window`](https://drafts.csswg.org/cssom-view/#extensions-to-the-window-interface) interfaces.  These methods return immediately with the value `undefined` because these method signatures were developed when scroll was assumed to be instant.  Currently there is widespread support for smooth-scroll, which can be specified using a [`ScrollBehavior`](https://drafts.csswg.org/cssom-view/#enumdef-scrollbehavior) entry in [`ScrollOptions`](https://drafts.csswg.org/cssom-view/#dictdef-scrolloptions) parameter passed to those methods.  This explainer elaborates how to make those methods return `Promise` objects (instead of `undefined`) that get resolved at the completion of the scoll, providing an easy way to do things at scroll completion as follows:
```JS
  element.scrollBy({top: 500, behavior: "smooth"}).then(() => {
     // Do something at the end of the scroll.
  });
```

## Non-goals

This explainer does not cover smooth-scroll behavior or chaining of nested scrollers.

<!--
## User research

N/A
-->

## Use cases

TODO: user-focused examples.

[Describe in detail what problems end-users are facing, which this project is trying to solve. A
common mistake in this section is to take a web developer's or server operator's perspective, which
makes reviewers worry that the proposal will violate [RFC 8890, The Internet is for End
Users](https://www.rfc-editor.org/rfc/rfc8890).]

### Use case 1

### Use case 2

<!-- In your initial explainer, you shouldn't be attached or appear attached to any of the potential
solutions you describe below this. -->

<!--
## [Potential Solution]

[For each related element of the proposed solution - be it an additional JS method, a new object, a new element, a new concept etc., create a section which briefly describes it.]

```js
// Provide example code - not IDL - demonstrating the design of the feature.

// If this API can be used on its own to address a user need,
// link it back to one of the scenarios in the goals section.

// If you need to show how to get the feature set up
// (initialized, or using permissions, etc.), include that too.
```

[Where necessary, provide links to longer explanations of the relevant pre-existing concepts and API.
If there is no suitable external documentation, you might like to provide supplementary information as an appendix in this document, and provide an internal link where appropriate.]

[If this is already specced, link to the relevant section of the spec.]

[If spec work is in progress, link to the PR or draft of the spec.]

[If you have more potential solutions in mind, add ## Potential Solution 2, 3, etc. sections.]

### How this solution would solve the use cases

[If there are a suite of interacting APIs, show how they work together to solve the use cases described.]

#### Use case 1

[Description of the end-user scenario]

```js
// Sample code demonstrating how to use these APIs to address that scenario.
```

#### Use case 2

[etc.]
-->

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
