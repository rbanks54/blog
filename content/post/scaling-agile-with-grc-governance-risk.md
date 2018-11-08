---
title: 'Scaling Agile with GRC (Governance, Risk, and Compliance)'
date: 2018-05-10T10:11:00.000+10:00
draft: false
tags : [agile, scale]
---

In the 21st Century, software is at the forefront of our lives. Our insurance, money, communication is all done via software. As such, the importance of GRC is becoming ever more apparent as more and more sensitive information is being stored and viewed by a range of people. We as software practitioners have the responsibility to ensure we store data securely, encrypt communication, output data in a legal and compliant format, and make everything accessible to the general public. At the same time we want to be able to make changes to our platforms as quickly as possible to interact with market conditions.  
  

[![](https://3.bp.blogspot.com/-PzVvCrHDEHE/WvONnTHvsXI/AAAAAAAARtQ/vYovNT5rrxUnVWpovEsUdhrG_uHK24TtQCLcBGAs/s200/480px-Referee-with-yellow-card.svg%255B1%255D.png)](https://3.bp.blogspot.com/-PzVvCrHDEHE/WvONnTHvsXI/AAAAAAAARtQ/vYovNT5rrxUnVWpovEsUdhrG_uHK24TtQCLcBGAs/s1600/480px-Referee-with-yellow-card.svg%255B1%255D.png)

A yellow card warning. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/Main_Page)

  
GRC has always been something of an awkward conversation when it comes to agile delivery. There's no questioning the value of end-to-end delivery that includes the delivery of GRC related activities such as: security, accessibility, and financial reporting. GRC should be a function of delivery, not an afterthought. At the same time, the value in having independent auditing in areas of accessibility and security is also paramount, as independent auditors will be free of unconscious bias towards the application as opposed to people who've been part of the creation of an application.  
  
  
  
  
GRC comes in many forms, the first ones that come to my head are outlined below. It is not within the scope of this post to explain each one in detail and the list isn't exhaustive. However I have supplied relevant links if you wish to learn more. Feel free to skip below and go directly to Delivery if you have a relevant background in GRC.  
  

### GRC

#### Security

Ensuring the application in development has minimal exposure to malicious attacks. This includes things such as secure communication, storage of sensitive data, transfer of sensitive data, and who has access to sensitive data. GRC activities may include: [penetration testing](https://en.wikipedia.org/wiki/Penetration_test), [PCI-DSS](https://en.wikipedia.org/wiki/Payment_Card_Industry_Data_Security_Standard), and [OWASP standards](https://en.wikipedia.org/wiki/OWASP)  

#### Reporting Standards

Certain regulated industries have requirements to report on fees and services in a standardised format. An example of this is private health insurance in Australia which requires all providers to display information in a [Standard Insurance Statement](https://www.privatehealth.gov.au/faq/sisguide.htm) format. Another example is [superannuation](https://en.wikipedia.org/wiki/Superannuation_in_Australia) reporting. Each Superannuation provider must display certain information on their website such as their ABN (Australian Business Number) and SPIN (Superannuation Identification Number).

#### Accessibility

Many private and government organisations require their websites to be accessible to people with impairments or disabilities. On websites this can take the form of [WCAG](https://www.w3.org/WAI/intro/wcag) or ADA compliance.

  

### Delivery

What I've found is that there are two competing approaches on how to approach GRC. The first is the audit mentality and the other is the single piece flow mentality where GRC forms part of delivery. Both have their advantages and disadvantages. However, they shouldn't be seen as mutually exclusive. Rather they should be used in parallel with each other.  
  

#### Cross Functional Teams

Scalable agile involves multiple teams delivering software in iterations that may or may not sync with each other. In this scenario there should be capacity that GRC subject matter experts are embedded into delivery teams to ensure that increments of software are delivered with GRC in mind.  
  
Keeping GRC as a function of delivery will ensure vertical iterations such as "WCAG Sprints" or "Security Sprints" where GRC related work is piled up does not occur. Performing GRC related work independently of the rest of the application causes a few problems. The first is that as an application is developed and GRC is ignored, it becomes harder to comply to certain standards. An example of this is accessibility. A site could be build out with a specific colour scheme and HTML components created that follow a specific pattern. All of this may have to be redeveloped if no accessibility is taken into consideration earlier on in the development of an application. Another example is security. If improper security practices are developed such as poor salting of passwords then the whole registration and user management portion of an application may need to be re-developed.  
  

#### Communities of Practice

GRC communities of practice such as: security, accessibility, and legal should have a prominence in scalable organisations. These communities of practice have the responsibility to learn from each other, but also to dedicate time to continuous improvement of systems under development. Cross pollination across applications, people, and teams should occur in an audit capacity. For example: The content management team may be audited by a security expert on the public facing website team and the public facing website team would be audited by a security expert on the content management team. This will enable sufficiently independence audits to occur to ensure maximal compliance, limited risk, and proper governance. This independence will not occur if audits are done by members of the delivery team in charge of the section of the application under audit. Ideally, these audits will occur independently of delivery iterations to entrench their independence from delivery. 

  

### Continuous Deployment

Please note: continuous deployment is different than continuous delivery. Where continuous delivery is about ensuring that a piece of software is able to be delivered into an environment per commit. Continuous deployment is actually deploying software into a live environment.  
  
The practice of continuous deployment will ensure the latest packages are audited, automated tests run in a deployed environment, and teams fix issues when they are still new (and easier to fix). Continuous deployments increases the ease of GRC by automating tests such as cross site scripting (for security), running some basic WCAG tests (such as colour and font size), and ensuring the site is sufficiently formatted to conform to legal requirements.  
  
Of course many GRC activities will not be able to be automated in the immediate. Either because they're too human specific (such as accessibility requirements) or because laws keep on changing (such as taxes or presenting information in a standard format). Either way, having continuous deployment environments available will ensure that something is available for manual checks as soon as possible.  In the end, it's about capturing and closing issues early by reducing GRC feedback loops.  
  

### Final thoughts

Having an ideological view on how to deliver GRC is often counter productive to actually protecting our customers and users. It is just as important to deliver GRC as a piece of delivery as it is to actually audit. As such, auditing as well as delivering, shouldn't be seen as mutually exclusive but activities that support each other. From a practical perspective, using automation testing with continuous deployment to reduce feedback loops ensures GRC doesn't build up and becomes a burden. Rather, the goal should be that GRC forms part of a continuous improvement culture that teams take pride in, as an element of a high quality software delivery practice