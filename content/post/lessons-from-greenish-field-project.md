---
title: 'Lessons from a greenish-field project'
date: 2016-01-21T15:18:00.001+11:00
draft: false
tags : [entity framework, alm, projects]
---

As consultants most of our work involves either PoCs or going into brownfield projects. However, recently I had the opportunity to go into a greenfield project, and below are the lessons I learnt.

## Don't over engineer
The stack that I was using was pretty standard. Entity Framework + MVC5. However, at the end of the project I found that the architecture that I have created was overly complicated when it need not be. Using an ORM such as Entity framework means that you already have a pretty solid data access layer in-place. What I had done was abstract this data access layer away from the business layer so that the business layer is not calling any Entity Framework code at all. I found this design to be too complicated, because the layer that abstracts EF was basically a wrapper that pipes into EF. **Next time, I would simply call EF from my business tier**. There is nothing wrong with this as EF already implements a repository pattern.  

## Don't prematurely optimise
Another error I fell into was that I had optimised too early. The result of the added optimisation meant that some of the code wasn't as readable as it should have been. Because this code was added early on in the solution it meant that it can potentially become code latter on that no one touches because no one really understands and is too scared to refactor (legacy? :P ). This is the type of code we do not want in any code-base.  
  

## Performance tests and logging
Entity Framework makes it quite difficult to do bulk deletes and bulk updates without doing any round trips, so I tried to optimise for this earlier on (as stated in the previously, I wouldn't do this if I started another project). I believe there is more value in creating performance tests than there is spending time doing premature optimisations. Why? because performance tests give you an initial benchmark to compare against, so that _when and if_ optimisations are needed we have the right benchmarks to compare against. A leader who has numbers on the product he/she leads is a leader who knows the software product well.