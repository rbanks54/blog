---
title: 'Why unit testing is still very relevant'
date: 2017-12-23T12:01:00.001+11:00
draft: false
tags : [testing, alm, agile]
---

In this age of in-memory test servers and databases, multi tenancy-first design, and increased performance it's easy to simply dismiss unit testing as a practice of the past. Whilst I myself have increased my dependance on integration testing in new applications that I write. Unit testing still has its place.  

[![](https://2.bp.blogspot.com/-26Q5U7T1vlE/Wj2qQfPwbUI/AAAAAAAAO9I/KqCAZ_W9hiwZjf11J6q_s6EOC1bAO9VIwCLcBGAs/s320/Yebisu_Beer_Museum_tasting_set%255B1%255D.JPG)](https://2.bp.blogspot.com/-26Q5U7T1vlE/Wj2qQfPwbUI/AAAAAAAAO9I/KqCAZ_W9hiwZjf11J6q_s6EOC1bAO9VIwCLcBGAs/s1600/Yebisu_Beer_Museum_tasting_set%255B1%255D.JPG)

*A set of beer-units about to be tested | source: [WikiMedia Commons](https://commons.wikimedia.org/)*


In 2017, I've gave a few talks about testing more and mocking less. I still stand by this. An excess of mocking actually negates one of the largest advantages of unit testing: **understanding dependencies and helping organise code better into single responsibilities**. The practice of testing (no matter at what level) is to validate your code-proper, edge cases, replicate issues that have occured in production, and act as a safety net so that code-proper doesn't break into the future.

TDD unit testing in particular has the added advantage of helping organise code into single-responsibility dependencies, smaller methods, and better named classes. Why? because production code is consumed (or called) prior to it being written, meaning that you have to understand the dependencies of your unit-under-test.

Whilst it may be tempting to have an integration test heavy application and completely discard unit testing, especially with new technologies coming through. I would suggest that your testing strategy be seen not only from the prism of code validation only but also code organisation.  

Thank you for reading