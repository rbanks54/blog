---
title: 'Using SBAR in code reviews'
date: 2018-03-22T08:49:00.001+11:00
draft: false
tags : [software engineering philosophy, software engineering]
---

After the end of a messy sprint everyone was excited and scared to attend the sprint retro. The topic we were dreading the most came up - pull requests. It had been a sprint where few pull requests went through smoothly and everyone was picking up issues with every pull request. Stylistic things came up, whole features needed to be redeveloped, people were clearly annoyed, and you could sense the tension in the room.  

  

Then, a suggestion by our non-technical product owner (who was a nurse and who had never been a product owner before) _Why don't you use something like the SBAR technique?_

[![](https://2.bp.blogspot.com/-hIAsC0ydDL8/WrI5r7h5b1I/AAAAAAAARDY/LVo37RVG7nsHWK2JSCiALpUT1ciJBePJACLcBGAs/s320/sbar%255B1%255D.png)](https://2.bp.blogspot.com/-hIAsC0ydDL8/WrI5r7h5b1I/AAAAAAAARDY/LVo37RVG7nsHWK2JSCiALpUT1ciJBePJACLcBGAs/s1600/sbar%255B1%255D.png)

Source: [Jessica Chang's Blog](http://nursejess.com/)

  
SBAR stands for 'Situation, Background, Awareness, Recommendation'. It's an acronym that started out in the military, but became very popular in medicine. 

  

Following SBAR in code reviews can allow smoother communication and understanding, as recommendations are made while outlining reasons why. For example:

  

Instead of

  

_Change this to constructor initialisers instead of property initialisers_

you could say

  

_There are two ways to initialise these properties \[**Situation**\], however when we started this project, C# didn't have property initialisers \[**Background**\]. I know that property initialisers are a newer feature \[**Awareness**\] but for the sake of consistency, can we initialise these properties from the constructor \[**Recommendation**\]_

Another example, instead of

  

_Can we make this method accept an IList instead of an IEnumerable_

you could say

  

_This method is called by a consumer of this library and it's been setup to accept an IEnumerable \[**Situation**\], this means that the enumeration of the collection is deferred in the code that we control rather than the responsibility of the consumer\[**Background**\]. Making this method accept both an IList or IEnumerable will probably work in a similar way \[**Awareness**\] however, we want to know that the collection that is passed to us is able to be enumerated successfully to ease debugging and separate out concerns regarding what our library does and what the responsibility of the consumer is \[**Recommendation**\]_

Following SBAR will slow you down in giving recommendations on code reviews. This is positive, as what I have found this does for me is that it makes me think twice about whether I'm correct in giving a recommendation or not.

  

It's important to note though that in many cases SBAR can be an overkill (factors include: culture, maturity, trust of teams). However, I have found that using this technique where I'm new to a team or where a team is new to code reviews really helps with being able to communicate my ideas. In the end though, it's always important to make a recommendation and follow up with reasoning. The SBAR technique is there to serve you and not designed to constrain your communication.