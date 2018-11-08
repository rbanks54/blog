---
title: 'More than just a build/release pipeline'
date: 2016-08-19T16:42:00.000+10:00
draft: false
tags : [devops, culture]
---

You've setup your build server, have continuous integration/delivery. Setup your release service, have continuous deployment. Your team are following proper branching strategy. Good yeah?  

  

**However...**  
Code PRs are carelessly merged, builds are always broken and you're 3 sprints behind.

What's the problem?
An initial examination will show that your team are following all the rules. However, further examination will show that they aren't being professional in other things. Many leads will simply suggest adding **more rules.** However, many rules should be the trigger that something is not going right in the first place.  
  
So, what is it that we can do to rectify some of the above issues.

## Explain 'why?'

Explain to your developers, why you actually have these things in place. For example:

**Continuous Integration**: To ensure that you haven't broken the build or tests. As a broken build or test hinders other developer's work. In addition, the longer a tests fail, the harder they are to fix, meaning a higher chance of bugs appearing in your product or even the software product not doing what it's supposed to do.

  

**Continuous Delivery:** To ensure that the build is always able to be deployed. So we don't have to waste time at the end of the sprint patching together the build.


**Continuous Deployment:** To provide a mechanism to request quick feedback to testers and stakeholders.

  

## Speak to individual members
The above problems often revolve either around a maturing culture. Or even worse, a bad culture. It often only takes one or two people to build a good culture, at the same time, it can take one or two people to destroy a culture. 

  

So it's important to identify key individuals. Both the good-culture building individuals as well as the destroyers. Encourage those who are positive, and talk to those who are negative to see what's wrong. Be sure to practice empathy to ensure that you can help individuals that are in need of it.  
  

## Finally...
**_Be patient_**. Positive cultural changes involve slow change of bad habits. Focus on one of these habits first, when your team see the difference one small positive change can make, the next change will be easier.

  

these include:

- Proper value given to code reviews.
- Proper respect given to the build status.
- Proper response to feedback.