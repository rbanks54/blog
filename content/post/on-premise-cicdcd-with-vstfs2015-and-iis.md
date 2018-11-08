---
title: 'On premise CI/CD/CD with VSTFS2015 and IIS'
date: 2016-08-01T17:30:00.004+10:00
draft: false
tags : [VSTFS2015, devops, IIS]
---

Many clients I visit are still not on the cloud and are still not using VSTS (Visual Studio Team Services) online and Azure.

Meaning, they still have on premise infrastructure for their applications. Now, I don't want this blog post to turn into a defence of cloud (more specifically PaaS). Rather, I want to quickly show you how you can setup a CI/CD/CD  (Continuous Integration/Delivery/Deployment) delivery pipeline with an on-premise instance of VSTFS 2015 deploying to machines with IIS .  
  
Basically, if you're still on premise! It's not an excuse to disregard DevOps practices!!  

## Build
The first step is to setup your builds. To do this navigate to the build tab in your Visual Studio Team Foundation Server 2015 collection and create a new build definition:

[![](https://1.bp.blogspot.com/-nvPiSNeZ9ZM/V56NpxUuUSI/AAAAAAAAKkg/vx9_hYa2wBYqYfCb3DxneGYjTu7IsDapQCLcB/s640/2016-08-01%2B09_44_41-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://1.bp.blogspot.com/-nvPiSNeZ9ZM/V56NpxUuUSI/AAAAAAAAKkg/vx9_hYa2wBYqYfCb3DxneGYjTu7IsDapQCLcB/s1600/2016-08-01%2B09_44_41-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.jpg)

Follow the wizard and be sure to **tick the box 'Continuous Integration'**. By ticking this box you ensure that on every commit (or checkin if you're using TFS-VC) your code will compile.

[![](https://4.bp.blogspot.com/-BHW4n9BP5qg/V56OWeEVdWI/AAAAAAAAKks/-Fum6z9Agn0gIevJw_x151yEhmKgpfW9wCLcB/s400/2016-08-01%2B09_48_31-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://4.bp.blogspot.com/-BHW4n9BP5qg/V56OWeEVdWI/AAAAAAAAKks/-Fum6z9Agn0gIevJw_x151yEhmKgpfW9wCLcB/s1600/2016-08-01%2B09_48_31-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.jpg)

[![](https://4.bp.blogspot.com/-MpxYw7rnuiI/V56OKKHfH0I/AAAAAAAAKkk/VITNnKiicfM-UETcPDik11bJKKn1kIkRwCLcB/s400/2016-08-01%2B09_47_26-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.png)](https://4.bp.blogspot.com/-MpxYw7rnuiI/V56OKKHfH0I/AAAAAAAAKkk/VITNnKiicfM-UETcPDik11bJKKn1kIkRwCLcB/s1600/2016-08-01%2B09_47_26-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.png)

In the 'NuGet restore' and 'Build Solution' steps. Be sure to explicitly specify the solution file. In the 'Build Solution' step. Enter the following msbuild.exe argument: **'/p:DeployOnBuild=true /p:WebPublishMethod=Package  /p:PackageLocation=$(build.stagingDirectory)'. **

[![](https://3.bp.blogspot.com/-VXagVAPh65I/V574fXZ1csI/AAAAAAAAKng/ow7eBwMtEQ4-WXgQwWNf3X4qqImAjk3IQCLcB/s640/2016-08-01%2B17_21_12-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://3.bp.blogspot.com/-VXagVAPh65I/V574fXZ1csI/AAAAAAAAKng/ow7eBwMtEQ4-WXgQwWNf3X4qqImAjk3IQCLcB/s1600/2016-08-01%2B17_21_12-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.jpg)

Save the build definition and trigger a build

[![](https://2.bp.blogspot.com/-JYrjxetkqzI/V56errt2_uI/AAAAAAAAKlI/Zd0DdaEZaY8nat87FykxAAnGrCQzbK1FwCLcB/s640/2016-08-01%2B10_58_13-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://2.bp.blogspot.com/-JYrjxetkqzI/V56errt2_uI/AAAAAAAAKlI/Zd0DdaEZaY8nat87FykxAAnGrCQzbK1FwCLcB/s1600/2016-08-01%2B10_58_13-Microsoft%2BVisual%2BStudio%2BTeam%2BServices.jpg)

  

## Install Relevant VSIX extentions

On your VSTFS2015 instance you will need to install some extensions. These are the IIS Extensions and can be found here:

  

https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.iiswebapp

## Release

Go to the release tab and create a new 'Release Definition'. Follow the wizard and be sure to tick 'Continuous Deployment'

[![](https://1.bp.blogspot.com/-mmpS-DjJ-AU/V56m-8VkQ6I/AAAAAAAAKlc/qeiWWYtqFq0oVTixja-a8PeoIJp7-8aKwCLcB/s320/2016-08-01%2B11_32_10-Explorer%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://1.bp.blogspot.com/-mmpS-DjJ-AU/V56m-8VkQ6I/AAAAAAAAKlc/qeiWWYtqFq0oVTixja-a8PeoIJp7-8aKwCLcB/s1600/2016-08-01%2B11_32_10-Explorer%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)

  

[![](https://1.bp.blogspot.com/-ULbPaAto89A/V56m-9DhVXI/AAAAAAAAKlY/O4Wk6Nd9YLEgd9Mf8szVzofD2p8KuzUkQCLcB/s320/2016-08-01%2B11_32_51-Explorer%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://1.bp.blogspot.com/-ULbPaAto89A/V56m-9DhVXI/AAAAAAAAKlY/O4Wk6Nd9YLEgd9Mf8szVzofD2p8KuzUkQCLcB/s1600/2016-08-01%2B11_32_51-Explorer%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)

If your artifacts have not linked. Be sure to go to the artifact tab and link your artifact from the build definition we just created.

[![](https://2.bp.blogspot.com/-fi0I0twlBlA/V56ngzqhkmI/AAAAAAAAKlg/VWv_P1uYMxwnRhueQpTwuNkokq9R3BnSwCLcB/s640/2016-08-01%2B11_35_55-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://2.bp.blogspot.com/-fi0I0twlBlA/V56ngzqhkmI/AAAAAAAAKlg/VWv_P1uYMxwnRhueQpTwuNkokq9R3BnSwCLcB/s1600/2016-08-01%2B11_35_55-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)


Go to the environment tabs and add 3 tasks

1. Copy Windows Machine File Copy
2. WinRM - IIS Web App Management
3. WinRM - IIS Web App Deployment

#### [![](https://4.bp.blogspot.com/-r6HaR1w5NlE/V56pF3q4Q5I/AAAAAAAAKlw/rqpae0_wmAUojeowukuanHK8P0sBFgG4QCLcB/s640/2016-08-01%2B11_41_36-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://4.bp.blogspot.com/-r6HaR1w5NlE/V56pF3q4Q5I/AAAAAAAAKlw/rqpae0_wmAUojeowukuanHK8P0sBFgG4QCLcB/s1600/2016-08-01%2B11_41_36-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)  
  

Copy files to remote machine(s)

The first step is selecting the source of your drops. The target machine name, target machine credentials and the location where the drops should go on the target machine. Notice, I've made these variables because they will be used in the other two build steps.

  

[![](https://2.bp.blogspot.com/-eGUI06gegZs/V57a1RVbk_I/AAAAAAAAKmA/NJH0O4BnHhQncmG_xD52CsXIatrS3lAzwCLcB/s400/2016-08-01%2B15_12_11-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://2.bp.blogspot.com/-eGUI06gegZs/V57a1RVbk_I/AAAAAAAAKmA/NJH0O4BnHhQncmG_xD52CsXIatrS3lAzwCLcB/s1600/2016-08-01%2B15_12_11-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)

  

[![](https://4.bp.blogspot.com/-MwiXkcoGZ90/V57cyc76IrI/AAAAAAAAKmY/1sUOEaj19GUtnDuNn7qu_QiPNijiuM_hgCLcB/s640/2016-08-01%2B15_23_18-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://4.bp.blogspot.com/-MwiXkcoGZ90/V57cyc76IrI/AAAAAAAAKmY/1sUOEaj19GUtnDuNn7qu_QiPNijiuM_hgCLcB/s1600/2016-08-01%2B15_23_18-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)

  

You can set these variables on an environment or on the release definition itself. I set them on the environment. 

  

[![](https://3.bp.blogspot.com/-M-zPiFt4f3k/V57bXByfALI/AAAAAAAAKmI/a2D2WhS-N38_gpzL5gzBCV3lwy0MyQ1eACLcB/s400/2016-08-01%2B15_17_14-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://3.bp.blogspot.com/-M-zPiFt4f3k/V57bXByfALI/AAAAAAAAKmI/a2D2WhS-N38_gpzL5gzBCV3lwy0MyQ1eACLcB/s1600/2016-08-01%2B15_17_14-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)

[![](https://1.bp.blogspot.com/-eA-fMyzJWKs/V57iOOoiezI/AAAAAAAAKnQ/S37MQdhH1ikjyq4hiO7JY2dkHS_WwEVcACLcB/s640/2016-08-01%2B15_46_06-ReleaseDef%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://1.bp.blogspot.com/-eA-fMyzJWKs/V57iOOoiezI/AAAAAAAAKnQ/S37MQdhH1ikjyq4hiO7JY2dkHS_WwEVcACLcB/s1600/2016-08-01%2B15_46_06-ReleaseDef%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)

  

#### Manage IIS App

Because we've stored the connection and website settings from the previous step as variables. What we can do is simply enter them into the second step. Be sure to tick both 'Create or Update Website' and 'Create or Update Application Pool'

  

[![](https://1.bp.blogspot.com/-tGGqcUOX30o/V57eu1ustoI/AAAAAAAAKms/a7_-i-VIol0nLLhPYtG7CwenhBtuqtSsQCLcB/s640/2016-08-01%2B15_29_27-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://1.bp.blogspot.com/-tGGqcUOX30o/V57eu1ustoI/AAAAAAAAKms/a7_-i-VIol0nLLhPYtG7CwenhBtuqtSsQCLcB/s1600/2016-08-01%2B15_29_27-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)

  

#### Deploy IIS App

Likewise in the last step. All the variables have already been set as part of the environment. The 'Web Deploy Package' is the location of the zip file generated from our build. This is the file in the folder that was set in the first step of the release definition.

[![](https://1.bp.blogspot.com/-_r05yxIbTOI/V57fVvAHYWI/AAAAAAAAKm0/MWMrXzgzkAooccfyAXjbv-LDVJFYbLSdgCLcB/s640/2016-08-01%2B15_33_52-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://1.bp.blogspot.com/-_r05yxIbTOI/V57fVvAHYWI/AAAAAAAAKm0/MWMrXzgzkAooccfyAXjbv-LDVJFYbLSdgCLcB/s1600/2016-08-01%2B15_33_52-New%2BEmpty%2BDefinition%2B01-Aug%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)

  

  

  

  

## Setting release conditions for Continuous Deployment

The final step is setting the release conditions for continuous deployment.

  

[![](https://1.bp.blogspot.com/-1id-2UrQwMg/V57gZgtXzKI/AAAAAAAAKnE/WUqxqwBOX0U1BRwAAvdXp9qWOYdqX7_mQCLcB/s640/2016-08-01%2B15_37_37-ReleaseDef%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://1.bp.blogspot.com/-1id-2UrQwMg/V57gZgtXzKI/AAAAAAAAKnE/WUqxqwBOX0U1BRwAAvdXp9qWOYdqX7_mQCLcB/s1600/2016-08-01%2B15_37_37-ReleaseDef%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)

  

[![](https://4.bp.blogspot.com/-dDA_GsBLZTo/V57gZoaG6DI/AAAAAAAAKnA/Ne9NZepAY7AKPXjf0gbjJH9uRuJTMDxzgCLcB/s640/2016-08-01%2B15_38_27-ReleaseDef%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)](https://4.bp.blogspot.com/-dDA_GsBLZTo/V57gZoaG6DI/AAAAAAAAKnA/Ne9NZepAY7AKPXjf0gbjJH9uRuJTMDxzgCLcB/s1600/2016-08-01%2B15_38_27-ReleaseDef%2B-%2BVisual%2BStudio%2BTeam%2BServices.jpg)