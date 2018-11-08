---
title: 'Git breaking? Get off the UI'
date: 2018-01-08T09:24:00.000+11:00
draft: false
tags : [team work, git]
---

Git is perhaps the best VCS I've used in my life. However, some of the things I always hear when people are trying to learn Git, or have used it for a while but never in larger teams are:  
"something stuffed up my Git"
"my Git is broken"
In my experience, Git is probably the most predictable, deterministic tool I've ever used (thankfully, considering it does version your code!).  
  

![](https://1.bp.blogspot.com/-DvFpe5e5p3Y/WlKdoabWtXI/AAAAAAAAPcU/nZb9JM9I85M4JKc5KRthW-Suh98YROILACLcBGAs/s320/512px-Git-logo.svg%255B1%255D.png)

*git logo. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/Main_Page)*

About 9 times out of 10 the people saying things like the above are those who are relying on a GUI abstraction-tool of Git, whether they be GitExtentions, SourceTree, Visual Studio Team Explorer or others. Whilst I don't think these GUI abstractions are bad in and of themselves (in fact, I like using GitExtensions to visualise graphs and diffs). They don't allow you to understand the more intricate details of Git such as: branching, rebasing, cherry-picking, ref-logs, remotes, branch tracking, tagging, and squashing.  
  
Going back to the breakages that are complained about above. These occur when: people pulling a main-line (master) branch into their feature branch, committing into the main-line (master) branch instead of a feature branch, or a bunch of merge conflicts because a sync hasn't been done for a while. These 'breakages' more often than not can be avoided if there is a more intimate understanding of Git.

Using the command line allows you to have this more intimate understanding of Git as no commands are abstracted away. Two more advantages to the command line are: Having a history of the operations that have been made on your repository. So if something has broken, you can have a rough idea of where it broken. And secondly, wider community support and reach when you do need to do a web search and get help.

In conclusion, if you find yourself struggling with your Git repository and fiddling too much. I suggest that you uninstall your GUI abstraction tool. Start using Git on the command line, then slowly introduce helper tools, if you don't know where to start simply try git --help. If I can learn the command-line. I'm more than confident you can too! The Git documentation is really easy to read and often a git status on your repository tells you exactly what you need to do to achieve what you want.

Thank you for reading