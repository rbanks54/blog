---
title: 'Quality and Pragmatism '
date: 2018-09-27T17:10:00.002+10:00
draft: false
tags : [agile]
---

  
  
Pragmatism and quality are two things that are often pitted against each other when delivering software. When I think of pragmatism, I think what things can be avoided in order to deliver software to our customer sooner. When I think quality, I think a whole range of things including: maintainability, scalability, and interoperability of a system to name a few. It may also mean things that may not directly relate to the system for example: documentation, support, and user customisation.  

[![](https://upload.wikimedia.org/wikipedia/commons/thumb/2/27/Seesaw_%28712%29_-_The_Noun_Project.svg/500px-Seesaw_%28712%29_-_The_Noun_Project.svg.png)](https://upload.wikimedia.org/wikipedia/commons/thumb/2/27/Seesaw_%28712%29_-_The_Noun_Project.svg/500px-Seesaw_%28712%29_-_The_Noun_Project.svg.png)

Seesaw Source: Wikimedia

  
  
At times we need to strike a balance between quality and delivery. This is called pragmatism. The art of striking this balance is difficult. Each software engineer’s experience is different, many engineers have been burnt by similar things. Some have been burnt by different things. As a team, it’s hard to be pragmatic because of these varying experiences.  
  
  
Deciding which aspects of quality to keep and which to remove must be based on a series of other questions and driven by factors which include:  the demography of users, expected modifications, and composition of the team. Achieving pragmatism is about asking the right questions to help us make the right decisions.  
  

User Demography
---------------

### Volume of users

Whilst technological purity suggests that we have to make a system scalable. We have to assess whether this is worth it in the first place. Pragmatic development would ask the question of what is the volume of users to begin with, prior to actually putting in the effort to making an application scalable. There's no point of catering for 100,000,000 requests a second when there will only ever be 50 concurrent users in an hour. Ask yourself:  
• Do I know who my users are?  
• Is the system limited by another identity provider? What is the maximum user-base of this identity provider?  
• What is the load for similar systems in my ecosystem?  

### Geo-location

The geo-location of users is also important. This often drives things like: localisation, deployment strategies, and legislation driven features like monetary transactions or reporting. In certain systems there is a certainty that most users will be within a limited location. For example: Tax software (whilst some might logon from overseas, this is the exception rather than the rule). In cases like this where we know that our users are within a specific location. We can ask ourselves questions like:  
• What time would be the ideal deployment?  
• Do we even need zero-downtime and A/B or red/green deployment if we're certain our users belong to a subset of time zones?  
  

Future Modifications
--------------------

### Expected Requirements changes

Whilst we shouldn't build software with speculation of requirements. It's still important to ask to what extent we must generalise and abstract our code. For example: having sections of our code-base which satisfies legislation that hasn't changed much in the last few years would suggest that the generalisation and abstraction of code can be quite limited. However, having a part of the code-base that sends emails and SMS would need to be generalised as things change quite often for example: the body of the message, message protocol type, and even provider that's used to send messages.  
  
Feature flagging is another technique that can be used to flag whether certain behaviours are floated to our users. The overhead associated with building the architecture for feature flagging increases and it's important to ask questions on the different combinations of features we want to deliver to which users for which tenant. A high quality product would have an architecture that can handle feature flags, however, if the expected future modifications are so low it may not be worth implementing it in the first place.  

### Content modification

Having a class of user who is a 'content editor/creator' can create a certain level of complexity in a software application. Sometimes the requirement for editing content can expand to such a degree that we've found ourselves in a situation where we're building entire content management systems (CMSs). This can be a dangerous path to go down as it creates inconsistencies across environments and places a degree of trust in this class of users to not break the current site.  
  
Like other situations, it's important here to ask the right questions. For example:  
• How often will the content change?  
• What content will change most often?  
  

Nature of the Development Team
------------------------------

The composition and nature of your development team can also affect certain decisions. For example if the nature of the team is one filled with contractors coming in and out, we may need to increase the effort and value that's placed upon documentation.  
  
Monitoring and notifications may have to increase if the composition of the development team is unstable. We may need to increase the breadth of who is notified in order that issues are raised to the relevant people quicker. These are just some considerations to take when developing with quality in mind in relation to the nature and composition of the development team.  

  
Conclusion
-------------

Quality is something that is difficult to define and different for different people. So being pragmatic about quality is a difficulty before we even start considering other environmental factors. Nevertheless, asking the right questions about the right things will help us devise an appropriate solution to the problem to be solved. I do not pretend to understand nor know all possible influencing factors, but trying to understand a certain level of context is important.  
  
Pragmatism in delivery is something that I believe is quite important, a huge part of this is striking a balance of actually delivering software versus the value that quality provides. I hope to write more about this topic in the future. Thank you for reading.