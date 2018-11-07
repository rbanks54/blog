---
title: 'Reboot DevOps (Part: II)'
date: 2018-08-07T13:52:00.000+10:00
draft: false
tags : [devops, agile]
---

In the [Part I](https://blog.raph.ws/2018/07/reboot-devops.html) we discussed how DevOps isn't about solving application problems using infrastructure but about being able to deploy to our targets in a sustainable way. We spoke about how increasing confidence enables personnel to release more often as risks are hedged by having solid application packages.  
  

[![](https://3.bp.blogspot.com/-0lEj-37Cu68/W2fzH5tDW4I/AAAAAAAASzY/xaZqJvM0wSwqHw385xK-K-vlO9qxhcvdwCLcBGAs/s200/Magnifying_glass_01.svg.png)](https://3.bp.blogspot.com/-0lEj-37Cu68/W2fzH5tDW4I/AAAAAAAASzY/xaZqJvM0wSwqHw385xK-K-vlO9qxhcvdwCLcBGAs/s1600/Magnifying_glass_01.svg.png)

Magnifying glass source: Wikimedia commons

  
  
Today we will speak about how monitoring and observability can increase our confidence to enable us to release more often.  
  
Monitoring an application is the surfacing of the metrics that allow us to see whether a system is operable, not operable, or in an exhausted state. On a basic level, this may mean CPU usage, memory usage, network throughput, errors, and exceptions. What monitoring seeks to provide is whether a system (or service within it) is working or not at any one point in time. Having the ability to visualise this data in production builds confidence, as knowing that a system is working or not at any point after releasing is better than finding out through external sources.  
  
Monitoring is something done on a system, observability is something that the system is. You have to actively make the system observable. Where monitoring is seeing the metrics of the system, observability is raising the right metrics to the surface. This may mean a few things: does your centralised message brokering platform provide the ability to log? Are logs among your services formatted consistently? Which business actions are important enough to warrant making observable?  
  
Observability is about asking the right questions and by asking the right questions you will be able to know what your desired metrics are.  
  
For example:  
  
_Why does my CPU usuage go up between 2-3pm even though my orders go down?_  
  
In order to be able to answer the question above we will need to replicate the state as well as control and data flow of our application in production at that specific time. If we're able to replicate this, then we're able to debug issues easier, then fix them. However, it's not only about fixing issues, it's about fixing potential issues. This is where confidence is really built.  
  
Finally, monitoring and observability build confidence because we are able to take the uncontrolled aspects of a system and raise them to the surface. Enabling us to debug and replicate issues as they are in production to take the guesswork out of fixing issues.  
  
Thank you for reading! I hope to post part III in the next few weeks.