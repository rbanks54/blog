---
title: 'Delete/Redeploy Azure Websites at specific times within a TeamCity and Octopus Deploy CI/CD pipeline'
date: 2015-05-29T09:53:00.002+10:00
draft: false
tags : [ci, devops, agile, cd]
---

### Problem

Many clients request that specific environments be only available certain times during a day.  
  
This is often due to the high cost associated with keeping environments that are not in use.  
  
The problem here can be divided into two.  
  
1\. How do we make the environment unavailable?  
2\. How do we make the environment available once more?  
  
Microsoft will charge Azure services per compute time. Meaning that even if you stop your Azure Website it will still incur costs. **This is the crux of the problem**. It means that we have to deploy and **delete the deployment** of the Websites in order to minimise cost effectively.  
  
Now if we have our project building, testing and deploying in a TeamCity and Octopus deploy pipeline. Ideally the Undeploy and Re-Deploy should be tunneled through the appropriate stage in the pipeline.  
  
The reason why we should do this is to ensure that redeployment goes through the same processes as a normal deployment, and that environment states (such as version number, failed/passed) all have one source of truth - The CI/CD pipeline.  
  
  
  

### A Solution

This solution assumes:

1.  That TeamCity is setup 
2.  Octopus Deploy is setup and deploying. Either with custom PowerShell scripts or the build-in Octopus ones.

There are three steps to the solution which I will show below.

1.  Write a PowerShell script that calls the Octopus REST API that simply re-deploys the latest release.
2.  Write a PowerShell script that _deletes_ the deployment on the environments.
3.  Set triggers on TeamCity and call these scripts.

#### Step 1 - Deploy script

I assume that you've already got Octopus deploying successfully.

  

The next step is to create a PowerShell script that **calls the Octopus API** and deploys your application from Octopus. The logic is:

1.  Find the environment
2.  Get the **_current deployed release_** on that specific environment
3.  Redeploy this release

An example of this script can be found [here](https://github.com/RaphHaddad/DeleteRedeployAzureWebsites/blob/master/Deploy-From-Octopus.ps1).  
  
Basically this script 'redeploys' the latest release on a given environment. The reason why we have parametised the environment is that many organisations have more that one testing environment they need taken down during non-operational hours.

#### Step 2 - Undeploy/delete script

As I stated previously, we need to actually delete an environment in this case, because of the way Azure has priced its services.

  

We opted to use the Azure cmdlets to do this. An example can be found [here](https://github.com/RaphHaddad/DeleteRedeployAzureWebsites/blob/master/Delete-Deployment.ps1).

  

#### Step 3 - TeamCity triggers

Now, the final step is to setup your TeamCity triggers to execute the above scripts at the appropriate times.  
  
_Typically_, the deploy script (from step 1) will be executed in the morning and the updeploy/delete script (from step 2) will be executed in the evening.  
  
What I prefer doing is having two build configurations for each of the above. A deploy configuration and an undeploy.  
  

[![](http://4.bp.blogspot.com/-uzCwRWSh9Gk/VVV_NuC3-yI/AAAAAAAAHyE/5guQnH9waZo/s1600/2015-05-15%2B15_07_12-Projects%2B%E2%80%94%2BTeamCity.png)](http://4.bp.blogspot.com/-uzCwRWSh9Gk/VVV_NuC3-yI/AAAAAAAAHyE/5guQnH9waZo/s1600/2015-05-15%2B15_07_12-Projects%2B%E2%80%94%2BTeamCity.png)

  

Setup each of the build configuration. Then go to build steps and add the powershell script.

  

[![](http://1.bp.blogspot.com/-dgCccYEb_uM/VWepCyBH58I/AAAAAAAAIRI/Q-MjPb1EtpE/s640/tc.png)](http://1.bp.blogspot.com/-dgCccYEb_uM/VWepCyBH58I/AAAAAAAAIRI/Q-MjPb1EtpE/s1600/tc.png)

Then go to triggers and add a 'schedule trigger'.  

[![](http://3.bp.blogspot.com/-MPmK7SMoFKc/VWeqBIRRuQI/AAAAAAAAIRU/1rmw7JFP7hA/s640/tc1.png)](http://3.bp.blogspot.com/-MPmK7SMoFKc/VWeqBIRRuQI/AAAAAAAAIRU/1rmw7JFP7hA/s1600/tc1.png)

  
And that's it! You're done.  
  

#### Summary

1\. Create deploy script using Octopus API.

2\. Create delete deployment script using Azure cmdlets.

3\. Use TC as script runner and schedule scripts.