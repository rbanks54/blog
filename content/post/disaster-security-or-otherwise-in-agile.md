---
title: 'Disaster (security or otherwise) in an agile (scrum) environment'
date: 2015-08-31T14:49:00.001+10:00
draft: false
tags : [security, scrum, disaster, agile, product owner]
---

When a disaster occurs in a system. Be that security, data or accidental the first thing that occurs in the psyche of the whole scrum team is:  

  

_Something, unusual has happened. Something different has happened. What do we do? What are the next steps._

The very definition of disaster in the [Macquarie Dictionary](https://www.macquariedictionary.com.au/) alludes to this.

  

_disaster_

_ Pronunciation of disaster /dəˈzastə/ (say duh'zahstuh)_

_noun 1.  any unfortunate event, especially a sudden or great misfortune._  

In my opinion, if a critical disaster has occurred, it is enough for the Product Owner to stop the sprint - declare it as unfinished and focus on the restoration of the system at hand.

  

At this stage, we move into disaster recovery. Hopefully in a self-organising team the processes in place to restore are picked up promptly by team members. In addition, the restoration processes should be able to be completed well under the SLA as promised by the system.

  

These activities may include: 

1.  Putting the system in maintenance, read-only mode. Or even taking it offline completely.
2.  Restoring system data, the database to another environment.
3.  Deploying the system binaries to the other environment.
4.  Changing DNSs to point to different environments.

The above may be done automatically. But sometimes they need to be done manually (due to necessary investigations), and this is when a more critical disaster occurs. This could happen because

1.  Malicious code in a certain version of the package.
2.  Security breach as a side affect to anther feature.
3.  Architecture failure.

### Disaster Decision Making

When a system falls into disaster. It is important that the subsequent states of the system (up until and including full recovery) are defined and triggered clearly by one person. The reason for this is to ensure that clear and prompt decisions are made. The Product Owner is a perfect candidate to take on this responsibility, as the Product Owner's job is to ensure the well-being of the system in the first place.

  

The Product Owner also has the responsibility to gather information and make a levelled and considered decision. He/she does this by ensuring proper consultation is made prior to officially changing the state of the system. For example: adequate tests are performed on the system before it is returned to a _fully functional and restored state_.

### Fitting into Scrum

[The scrum guide says](http://www.scrumguides.org/scrum-guide.html#events-sprint)

_Only the Product Owner has the authority to cancel the Sprint, although he or she may do so under influence from the stakeholders, the Development Team, or the Scrum Master._

So, even if the sprint is cancelled. **The scrum team does not cease to be a scrum team.** A team simply does not go from being a scrum team, to _not_ being a scrum team because a sprint is cancelled. The cancellation of a sprint is fully compatible event within scrum. Albeit one that is rare.

### Resumption of BAU (Business as Usual) Processes

Cancelling a sprint tires people, uses resources and wastes development time. So, it is often difficult to organically return to BAU processes when a cancellation has occurred. 

  

When a sprint is stopped, and technical disaster processes are taken. It is simply not enough to resume a sprint by starting _sprint planning_ once again.

  

It is an error of judgement if a disaster is rectified and not inspected to find why the disaster occurred in the first place. As such, it is **essential that the root cause of the disaster is investigated** in order for it not to occur again. Only after this investigation is it viable for the scrum team to resume their BAU processes.  

### Concussion

While Scrum is focussed on delivering a new increment of a product, it is does not mean that emergency processes do not fit within the Scrum framework. Scrum itself is not an excuse to ignore disaster recovery processes and mechanisms. On the contrary, the scrum framework is perfectly compatible with these processes by ensuring decisions regarding the disaster status of a product are made by the Product Owner who is able to communicate to both the stakeholders and the development team.