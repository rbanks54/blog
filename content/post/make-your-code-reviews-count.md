---
title: 'Make your code review requests count'
date: 2018-02-16T17:24:00.001+11:00
draft: false
tags : [software engineering philosophy, software engineering]
---


The value in PRs (or code reviews in general) is more than just ensuring good code is pushed into the main-line branch. There's more to a PR in my opinion. This includes  
  
- Learning from others  
- Sharing learning, understanding, and the architecture of your system  

[![](https://1.bp.blogspot.com/-9Z0l1ixrzq4/WoZ43KE5aHI/AAAAAAAAQq0/ak0aDnoOIRIH7a2XLkmuprepdH6Mj4GGgCLcBGAs/s320/Code_Review_photo-1%255B1%255D.jpg)](https://1.bp.blogspot.com/-9Z0l1ixrzq4/WoZ43KE5aHI/AAAAAAAAQq0/ak0aDnoOIRIH7a2XLkmuprepdH6Mj4GGgCLcBGAs/s1600/Code_Review_photo-1%255B1%255D.jpg)

*Someone doing a code review. Source: [WikiMedia Commons](https://commons.wikimedia.org/wiki/)*


Have you ever received a code review request where someone has ran a tool over the file and changed formatting, spacing, or convention? Or where someone wished to create a new line after every dot, or change brackets? There’s nothing wrong with these types of requests in isolation.

What is wrong is when the request is sent with valuable code changes. That is, a combination of formatting changes and valuable code are pushed together. In these scenarios, the formatting change is often much more than the valuable code change.

The attention of the reviewer now must be shared between actual code change and noisy, unnecessary formatting changes. Therefore, important things such as new architecture and concepts may be missed or subconsciously ignored. As well as picking up on legitimate issues with the code being reviewed.

I suggest that you don’t undervalue your requests for code review. If you really want to make formatting changes, submit one request with the higher quality code, and submit another with the formatting changes.