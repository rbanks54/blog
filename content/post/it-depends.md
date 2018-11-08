---
title: 'It depends'
date: 2018-07-02T12:33:00.000+10:00
draft: false
tags : [team work, consulting, agile]
---

A few months ago I wrote a post [I Don’t Know](https://blog.raph.ws/2018/01/i-dont-know.html). It was a post that explained why being honest about things you don’t know is important, as it builds trust amongst team members. I also explained why saying you don’t know something and following it up with a desire to actually take action, in order to gain that knowledge, is important. Today, I will talk about the words “it depends”.

![](https://upload.wikimedia.org/wikipedia/commons/7/79/Recurrent_ann_dependency_graph.png)

*Dependency Diagram for a recurrent artificial neural network. Source: Wikimedia Commons*


Consultants are accused of overusing this phrase and rightly so. You see, if someone is asked a question and the response is “it depends”. Neither is the question answered nor is the information necessary to answer the question supplied, or a request for more information communicated.  

When being consulted on a certain subject matter there is the reasonable expectation that the consultation will result in an answer or be directed to an answer. As such, I have been trying to follow up the words “it depends” with context on what the dependencies are. You see, a lot of the time I’m not lying when I say “it depends”. To stop at "it depends" though is not helpful, what is more helpful is following up this phrase with a request for context or a statement on dependencies. For example:

Question: “Should we run UI tests before merge into master”
Answer: “It depends, how long do the tests take to run?”

Question: “Is it worth having failover into another region”
Answer: “It depends, what is the consequence of downtime?”

What I found after months of actively follow up the words "it depends", is that at times, I’ve completely eliminated the requirement to say “it depends” all together. Let’s try the above examples again:

Question: “Should we run UI tests before merge into master”

Answer: “How long do the tests take to run? If they don’t take too long it may be a good idea. We can try it and see whether the slight increase in feedback time annoys developers”

Question: “Is it worth having failover into another region”

Answer: “What is the consequence of downtime? From my understanding we are a phone call away from all users of the system. Taking this into consideration in addition to our small user base, it may be a bit of an overkill to have failover.”

The above examples try to provide direction from the request of consultation. In many cases though, it is up to the person who's consulted me to eventually make the decision. I can only give my opinion, the facts as I see them, and seek clarifications on dependencies.

If someone has asked me a question it means they value my opinion. For me to simply respond back with “it depends” without actually providing clarification on those dependencies would not actually achieve anything. It’s OK to not be able to answer a question straight away and ask for further clarification, it's even OK to say [you don't know](https://blog.raph.ws/2018/01/i-dont-know.html)!  Either way, not leaving the question hanging is the key to actually getting it answered.