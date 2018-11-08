---
title: 'Tips to Automate Yourself Out of a Job'
date: 2018-04-05T07:33:00.001+10:00
draft: false
tags : [software engineering philosophy, devops, automation]
---

Providing tools, processes, and platforms that automate everything, including yourself out of a job should be the goal of everyone in IT. It's something people rant about on Twitter, speak about on YouTube, and attempt to inspire on LinkedIn. Everyone seems to be telling us we _should_ automate our jobs, not many are telling us _how_. Today I have a few practical things you can do to actualise this goal.  
  
  

Business Control of Release Pipeline
------------------------------------

Creating build and release pipelines should be a given in 2018. To go that step further, we need to provide the necessary tooling to hand control of release pipelines to business individuals.The challenge here is twofold. First, how do we as IT give enough tooling for Business to do their job of simply promoting and deploying, while, keeping security tight enough to ensure pipelines aren't broken. Second, how do we as IT start the psychological change necessary for Business to start taking more control of the delivery of software.

  

In my experience, the first challenge is easy, the second challenge is the more difficult. For many in Business this will be a disruption, a forced internal disruption. The potential increase of power, responsibility, and to a lesser degree skill means that there will be a combination of emotions from individuals within business. This includes fear and excitement. Depending on how communication and training is done by IT, Business will either accept or reject this proposition. A common argument against this proposition will likely come from individuals who feel that there isn't a separation between IT and Business. This isn't a valid argument against this as this is exactly what we want! The two practices (IT and Business) should be coming together (reasons of which aren't part of this post but for a post in the future). 


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Policies On Pull Requested Code
-------------------------------

A process of pull requests should be in place in any organisation. This process should include policies which build and test candidate production code. To further automate the process of pull requesting and code reviewing, it's a good idea to add code analysis to these policies so that the code reviewer doesn't need to review low-value stylistic or convention rules that can be automated. Below are some tools I've used in the past to help automate this.  

### .editorconfig

Placing an [.editorconfig](http://editorconfig.org/) in your code-base automates preferences of conventions. .editorconfig files allow you to set conventions for a code base on a text file (encoding, spacing) with different levels (info, warning, and error). As it is a file, just like any other in your repository, the history of conventions is source controlled.

  

If you're a .NET developer, .editorconfig will soon be integrated into Roslyn, meaning rules that you specify on .editorconfig will throw compile time errors or warnings.

### NDepend

[NDepend](https://www.ndepend.com/) is a static code analyser which is flexible enough to allow you to set rules yourself as well as having predefined rules. My personal favourites are: Cyclomatic complexity, number of lines of code, and depth of inheritance tree. It can be run as part of your PR build policies that fail if a certain metric on a rule isn't satisfied and blocks integration with your main-line branch.

### NCover

NCover is a tool that reports on code coverage by tests. Similar to NDepend above, it can be run as part of build policies that fail if a certain level of coverage isn't met.  
  
Warning:  
Code coverage, cyclomatic complexity, and inheritance levels are all code-quality metrics that have to be interpreted within context. There is no _right_ level of coverage, inheritance levels, or cyclomatic complexity. These are all metrics that are used in combination with other indicators to highlight overall code quality.

Feature Flagging
----------------

An initial upfront investment in developing architecture that allows for feature flagging will allow businesses to control which features they want in production and which they do not want without actually having to have to do a deployment. Feature flagging is similar to my first point about handing control of release pipelines to business, however, feature flagging can be seen as a bit more mature. It allows businesses to try and test a combinations of features to validate their hypothesis in production with a much shorter feedback time.  
  

Failover AND Failback
---------------------

When production goes down. It's stressful. Stressful for Business, IT, and most importantly for our customers. To prevent this stress by all parties, it's important to automate failover and failback. While failover is important, we must ensure that failback occurs, so that if a disaster does occur once more, we are able to failback again. While I don't think we strictly need to revert back to our previous infrastructure state, it's important to ensure that after a failover, if a disaster is to occur again, then all the necessary pieces are in place in a reasonable amount of time to be able to failover once more. In summary, IT needs to develop an end-to-end disaster recovery strategy where the system is always in a state, where it is able to handle repeated failovers automatically.

  

Conclusion
----------

Automation isn't the sole domain of IT. It should be spread across all departments in an organisation. IT's role isn't to automate their jobs only but to automate all repetitive tasks in an entire organisation to allow for greater creativity and collaboration. This allows people more time to validate hypothesis, learn, adjust, and deliver useful software for customers.