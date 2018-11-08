---
title: 'Have You Ever Produced Negative Value in a System!?'
date: 2017-11-24T08:50:00.002+11:00
draft: false
tags : [software engineering philosophy, software engineering]
---

As developers we encourage our product owners to order the priority of their backlog in order of value. However, every time a new feature is implemented by a development team, there is a certain degree of risk associated with the introduction of that new code. Namely, risk of breaking another part of the product and maintenance cost. When a development team pulls in a new feature to implement there is a certain acceptance of this risk. In many cases, the risks that arise due to additional code complexity doesn't justify the value added by the new feature itself, so the development team can start implementing it.

Are there scenarios where the value added to a software product can be negative though?  

The short answer is: _yes_. As touched on previously, any code that is introduced into a system increases complexity (even if it is a little bit) and risks breaking something else. If a feature is wanted by a product owner, that we can be certain will never be used by our users, then it is in effect introducing negative value into the code base. The more complexity the unneeded feature introduces, the more negative value has been introduced into the system. What makes this **even worse than technical debt** is that it is something that can't be paid off, because it is something that was explicitly requested by the product owner or business and something they don't want removed.

I had found myself in the above scenario, being forced to provide negative value to a system. I was forced to accept that I needed to introduce a certain feature to a system that our data showed will never be used.   

So how do we address this issue? Firstly it's important to educate business on system complexity. Make it clear as soon as you can that anything introduced into a code base has a risk of breaking another feature. Be clear with them, that the only system with no risk of not breaking anything is one with no features to begin with - this is an extreme but it stands true. It is similar to the proposition that the only secure system on the internet is one that's not on the internet - an extreme, but it stand true. Sometimes, you will be forced to introduce this kind of negative value into a code-base and if you do I suggest you do the following: Highlight the risks honestly and explaining complexity as I've attempted above.

To hedge these risks from a technical perspective you have to be sure you have good testing practices. Especially TDD in both feature development **and bug fixes.**

If all that fails and you still get forced to do something like this, just remember - I understand how you feel, have been there and felt the pain!

Once again thank you for reading my blog. Any comments, suggestions, or feedback are more than welcome.