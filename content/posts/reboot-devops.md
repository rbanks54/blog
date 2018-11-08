---
title: 'Reboot DevOps'
date: 2018-07-24T09:54:00.000+10:00
draft: false
tags : [devops, agile]
---

In an ideal scenario a large organisation would have DevOps capabilities spread across their various teams. There would be no need to lean on an operations team to do any deployment, scaling, or observing of applications. Engineers would understand the inside and outside of infrastructure, security, logging, and message brokering.


The world isn't ideal though, that's not an excuse not to strive for the ideal.

[![](https://1.bp.blogspot.com/-XcftbaimgWo/W1ZrlVdh5QI/AAAAAAAASg4/O_S_U48Nuyg1LtcWEG4WGJ1H2m6CKLXdgCLcBGAs/s400/800px-Too_Busy_To_Improve_-_Performance_Management_-_Square_Wheels%255B1%255D.png)](https://1.bp.blogspot.com/-XcftbaimgWo/W1ZrlVdh5QI/AAAAAAAASg4/O_S_U48Nuyg1LtcWEG4WGJ1H2m6CKLXdgCLcBGAs/s1600/800px-Too_Busy_To_Improve_-_Performance_Management_-_Square_Wheels%255B1%255D.png)

*Fixing problems in the wrong way. Source: Wikimedia Commons*

This blog post will be the first on a series of posts examining my thoughts on the current state of DevOps and what I think we can do to improve.  

If we do a quick seek search on [DevOps](https://www.seek.com.au/DevOps-jobs) you'd notice that most advertisements focus on infrastructure, some may mention message brokering, and surprisingly some advertisements mention "Strong exposure to Blockchain/Crypto world".  

What's a surprise to me is that none of these advertisements actually mention anything related to application level problems. One of the most important elements of DevOps is the ability to release changes to our users sustainably and regularly. That is, releasing enough that they are able to experiment but not too much that we may anger them.  

A large part of this release cadence is _confidence_. Confidence is the ability to release software with a minimal amount of risk. This risk changes depending on the product. An important (but not exclusive metric) is releasing without causing too many bugs. Reducing bugs isn't the sole metric of confidence though. The more we drive, the more confident we become that we'll not crash. Similarly the more we release, the more confident we become that we're able to release in the future.  

A proficient way to gain confidence is to spend time on test automation. I find there's little point setting up a sophisticated CI/CD pipeline that does post-deploy test runs, build-time test runs, test which are divided into different sub-sets, or scheduled tests on a live environment when our test suite is insufficient to start with.  

An insufficient test suite is something that has nothing to do with infrastructure, networking, or release pipelines. Test suites must strike a balance of several things (not exclusive to):  


1.  Deterministic
2.  Coverage
3.  Speed of execution
4.  User simulated coverage (usually done through slower 'UI Tests')

  
There is not one size fits all for test suites. So I'm not going to preach on test coverage metrics, the percentage of unit, integration, or UI tests. Instead, I'd encourage you to ask yourself the following questions:  


-   How _confident_ are we that our quicker-running tests provide enough coverage?
-   How _confident_ are we that our test suite is maintainable for the future?
-   How _confident_ are we that we can measure coverage metrics across and within the test suite?
-   How _confident_ are we that we can run a subset of tests on a live environment without the need for manual testing?

Like automated testing, application resilience also has little to do with infrastructure, networking, or release pipelines. Whether we have a microservice or monolithic architecture, our application has to be resilient. If our application is reliant on external storage, caching services, or external APIs. If any of these dependencies are down, the whole application must not crash completely. It must be resilient enough to still operate in the areas that don't require those dependencies. 

Not only must the application be resilient, but the application must know how to log properly. Which brings me to the next post that I will write on in this series: observability and monitoring.

Sufficient test coverage and resilience have a common theme. That is, not solving application problems with infrastructure. If your SQL queries are slow, paying for an upgraded VM size will not solve the root cause problem and may mean that the problem rises to the surface once more in the future. This is not an ideal situation. Basically, DevOps is not an excuse to divert focus away from the quality of your application-level code.