---
title: 'Reboot DevOps (Part: III)'
date: 2018-08-14T17:47:00.002+10:00
draft: false
tags : [team work, devops, agile]
---

As alluded to in Part 1 and II it seems that DevOps has just become about CI/CD pipelines, provisioning infrastructure, and deploying applications. Today, we'll speak about CI/CD pipelines but more specifically the purpose they seek to provide.  
  
Firstly, I think the term CI/CD is counter-intuitive. It's not a descriptive term and I would prefer to use the far more boring term _release pipeline_ because it is self descriptive. Our primary concern is how does candidate code get from a local developer's machine all the way into production. Here we need to employ ToC (Theory of Constraints) thinking to really understand the reasoning of CI/CD in the first place.  
  

> the level of utilization of a non-bottleneck is not determined by its own potential, but by some other constraint in the system. - Dr Eli Goldratt

  
  
Within a software releasing paradigm the above suggests that there is little reason to optimise a step in your flow that's not the bottleneck. This can be anywhere from code reviewing, compiling and building, QA, legal, and deployment.  
  
Similarly, there's no point of optimising CI/CD if that part of your flow isn't the bottleneck. CI/CD in isolation isn't the finish line. It is simply a means towards getting to the finish line. Which is, to continue to make the delivery of software into production as smooth and sustainable as possible. This is a goal that's ever-receding. There's always room for improvement.  
  
Ask yourself the below questions.  

*   Does your package get stuck at a lower environment waiting QA before it gets deployed to production?
*   Does candidate code remain in long lived branches?
*   Does building your package take a long time?
*   Are there bugs that appear in some environments but not in production?

If you answered 'Yes' to any of the above. Then CI/CD will not be addressing the bottleneck. If we're not addressing the bottleneck then our primary concern of getting candidate code into production isn't getting the attention it needs. You're solving the wrong problem.  
  
If we're focusing on CI/CD only, a local efficiency, then we're not focusing on our entire flow. DevOps shouldn't be about CI/CD in isolation. DevOps should be about the bottlenecks that exist in releasing software. Several years ago, this may have meant the bottleneck exists at the infrastructure level. Today, it may be different things such as: security, QA, and poor branching strategies.  
  
DevOps is commonly seen as a joining of two sub-teams of a wider technical team (development and operations). The reason for this 'joining' is what we should take into our contemporary software industry not necessarily the act of it. That original reason was the involvement of several capabilities in order to release software as a single common team. Today, software is a lot more complicated and more people may be involved. These people include: security, legal, QA, development, and infrastructure.  
  
Building these capabilities across our teams is what will help us deliver software quicker. This may mean cross discipline engagement. Developers must speak to security, operations must speak to legal. The combinations are innumerable. It also means that we as technical people have to change our isolated way of working. We have to be patient and focus less on local efficiencies and more on common metrics that encompass the entire release life cycle. We need to engage all relevant teams and individuals to identify and utilise the bottlenecks in order to establish a sustainable release cadence.