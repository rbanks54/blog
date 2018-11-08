---
title: 'PowerShell from SourceTree as a custom action'
date: 2015-05-04T15:08:00.001+10:00
draft: false
tags : [sourcetree, powershell, git, atlassian]
---

**Step 1:**  
Create a ps.bat file with one line:  
  
start powershell  
  
Save this file in an appropriate location. I saved mine to:  
C:\\CustomCommands  
  
  

[![](http://3.bp.blogspot.com/-opwkInnC_JA/VUb5rhIxPsI/AAAAAAAAHXA/n60XXhhFrgE/s400/screen1.png)](http://3.bp.blogspot.com/-opwkInnC_JA/VUb5rhIxPsI/AAAAAAAAHXA/n60XXhhFrgE/s1600/screen1.png)

  
  
**Step 2:**  
Add a custom action to SourceTree.  
  
You do this by going to  
  
Tools -> Options -> Custom Actions  
  

[![](http://4.bp.blogspot.com/-Kmv820imeuw/VUb66taYO4I/AAAAAAAAHXQ/rknJ6aUxK9A/s400/screen2.png)](http://4.bp.blogspot.com/-Kmv820imeuw/VUb66taYO4I/AAAAAAAAHXQ/rknJ6aUxK9A/s1600/screen2.png)

  

[![](http://3.bp.blogspot.com/-tng5msq3nH8/VUb7TOxhj7I/AAAAAAAAHXY/w7dtb7Wdy80/s400/screen3.png)](http://3.bp.blogspot.com/-tng5msq3nH8/VUb7TOxhj7I/AAAAAAAAHXY/w7dtb7Wdy80/s1600/screen3.png)

  

  
Click the 'Add' button and you will get another Window.  
  
On the 'Menu caption' type an identifier for PowerShell and on 'Script to run' navigate to the script you made in step 1 then click 'OK' and exit from the 'Options' Window.  
  

[![](http://1.bp.blogspot.com/-mYSjYPFD5Aw/VUb9BmMtJxI/AAAAAAAAHXk/y1RhsKx9Ero/s400/screen4.png)](http://1.bp.blogspot.com/-mYSjYPFD5Aw/VUb9BmMtJxI/AAAAAAAAHXk/y1RhsKx9Ero/s1600/screen4.png)

  

  

**Step 3:**

Test PowerShell.

  

[![](http://3.bp.blogspot.com/-E9Ac00467m0/VUb9ov7zwyI/AAAAAAAAHXs/UZK30aCZpWM/s400/screen5.png)](http://3.bp.blogspot.com/-E9Ac00467m0/VUb9ov7zwyI/AAAAAAAAHXs/UZK30aCZpWM/s1600/screen5.png)

  

  

  
  
  

[![](http://1.bp.blogspot.com/-A6WId6ekXME/VUb9oq_KCPI/AAAAAAAAHXw/2rwb5r2mcUc/s400/screen6.png)](http://1.bp.blogspot.com/-A6WId6ekXME/VUb9oq_KCPI/AAAAAAAAHXw/2rwb5r2mcUc/s1600/screen6.png)