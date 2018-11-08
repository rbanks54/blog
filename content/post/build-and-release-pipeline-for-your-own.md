---
title: 'Build and Release Pipeline for Your Own Custom VSTS Tasks'
date: 2018-03-27T16:14:00.002+11:00
draft: false
tags : [vsts, devops]
---

Anyone can create their own custom VSTS tasks and put them on the VSTS [marketplace](https://marketplace.visualstudio.com/). There are tons of these custom tasks and they can be published publicly into the marketplace or privately into your own instance of VSTS. This blog post will demonstrate how to setup a build and release pipeline for these custom tasks (using custom VSTS tasks!).

There are many reasons to create your own tasks on an instance of VSTS. You could be part of a DevOps capability that wants to share common platforms, standardisation, or integrations. Generally though the reasoning is to avoid common steps that are duplicated across different build and release pipelines.

## Prerequisites and gotchas

Before actually setting up your own pipeline for custom tasks. You'll need to be able to create them locally first. I find the best tool for this is the tfx-cli that can be found [here](https://github.com/Microsoft/tfs-cli). It scaffolds your task folder structure and provides a mechanism to publish into VSTS. My personal preference is to write my custom tasks with PowerShell and as such I need to include the [VstsTaskSdk](https://github.com/Microsoft/vsts-task-lib) in my source. The following structure is the result:

  
```
icon.png 

sample.ps1   

task.json  

ps_modules  

└───VstsTaskSdk  

    │

    └───Strings 

        └───resources.resjson
```

## Setting up the pipeline
### Install Dependencies
The first thing we need to do is install tfx-cli as a local dependency if we haven't already done so:

```
npm init
npm install tfx-cli
```

### Generate PAT

After you've done this, you'll need to generate a[ personal access token](https://docs.microsoft.com/en-us/vsts/accounts/use-personal-access-tokens-to-authenticate#create-personal-access-tokens-to-authenticate-access) from your account. To be extra secure only give this token access to the scopeMarketplace (publish) (if you want to push into the VSTS marketplace) and/or Agent Pools (read, manage) (if you want to push into your own VSTS instance).  
  
  

[![](https://1.bp.blogspot.com/-Mm19_VuVObA/Wrmbh2n7j3I/AAAAAAAARHg/HhG5HDPyX8UKofeo5exJA_MFm0iLAvkLQCLcBGAs/s400/pat.jpg)](https://1.bp.blogspot.com/-Mm19_VuVObA/Wrmbh2n7j3I/AAAAAAAARHg/HhG5HDPyX8UKofeo5exJA_MFm0iLAvkLQCLcBGAs/s1600/pat.jpg)


Take note of this Personal Access Token as we'll need it in a bit.

###

### Create the Build Definition

Go to your instance of VSTS. Create an empty build definition, select your source location, and save the definition:  

[![](https://3.bp.blogspot.com/-9c59Mxm4Wh8/WrXu9NSKdDI/AAAAAAAARGE/8XZBOSJYimA571-rZpQwbUTySpddiu32wCLcBGAs/s640/source.jpg)](https://3.bp.blogspot.com/-9c59Mxm4Wh8/WrXu9NSKdDI/AAAAAAAARGE/8XZBOSJYimA571-rZpQwbUTySpddiu32wCLcBGAs/s1600/source.jpg)

After you've done this, you'll need to add a custom variable to your definition. Add your pat (which you created previously) as a secret variable:  
  

[![](https://2.bp.blogspot.com/-Cift6q-4FRU/WrmcgX0QgRI/AAAAAAAARHs/PoT3gJvqbRcRkp1ak2i2ZRJqqB_oxcroACLcBGAs/s640/add_variable.jpg)](https://2.bp.blogspot.com/-Cift6q-4FRU/WrmcgX0QgRI/AAAAAAAARHs/PoT3gJvqbRcRkp1ak2i2ZRJqqB_oxcroACLcBGAs/s1600/add_variable.jpg)

  
  

Security Warning:  
As you'll be adding your PAT to this definition, anyone with permission to modify this build definition will be able to execute commands with the permissions that this PAT has on your behalf. 

Make sure that the Build number format in the options tab is empty:

[![](https://1.bp.blogspot.com/-LTQHu-sXDh4/Wrmd5e-2bKI/AAAAAAAARH4/r7Ypfnz3yTM0JwgqXDBoFg-DbPbkMQ14wCLcBGAs/s400/empty_build_number.jpg)](https://1.bp.blogspot.com/-LTQHu-sXDh4/Wrmd5e-2bKI/AAAAAAAARH4/r7Ypfnz3yTM0JwgqXDBoFg-DbPbkMQ14wCLcBGAs/s1600/empty_build_number.jpg)

### Add Build Number Tokens

In the code for your Custom Task. Open up your task.json file. In version:Patch replace the number with #{BUILD_BUILDNUMBER}# This token will eventually be replaced in the pipeline with the VSTS build number.  
  
  

[![](https://2.bp.blogspot.com/-Y8DGudIgC-k/WrmidAj5V5I/AAAAAAAARIE/SqtRxesHlW4ACw11zdXxQ_um36iPWtZ4wCLcBGAs/s320/token.jpg)](https://2.bp.blogspot.com/-Y8DGudIgC-k/WrmidAj5V5I/AAAAAAAARIE/SqtRxesHlW4ACw11zdXxQ_um36iPWtZ4wCLcBGAs/s1600/token.jpg)

  
  

### Add steps in Build Definition

You will need three steps in the build definition  
_1\. Install TFX on the build agent_  
Add a npm task with the command install  

[![](https://1.bp.blogspot.com/-lNUcafIlJmI/WrmkHEDZVlI/AAAAAAAARIQ/5ZwZF1zGlM0PBYU4Xpc-wpQSJl2hye-IACLcBGAs/s640/task_npm.jpg)](https://1.bp.blogspot.com/-lNUcafIlJmI/WrmkHEDZVlI/AAAAAAAARIQ/5ZwZF1zGlM0PBYU4Xpc-wpQSJl2hye-IACLcBGAs/s1600/task_npm.jpg)

  
_2\. Replace tokens from task.json with the build number_  
Add a [Replace Tokens Task](https://github.com/qetza/vsts-replacetokens-task#readme) that will automatically replace the build number from VSTS pre-defined environment variables. I like to explicitly define the files where the tokens exist. In our case: task.json  

[![](https://2.bp.blogspot.com/-efOW92Ape8c/WrmkvP_1RMI/AAAAAAAARIY/7LNDEtnx8uUa2UBsHtfVNseaiCV3VTa8QCLcBGAs/s640/task_replace_tokens.jpg)](https://2.bp.blogspot.com/-efOW92Ape8c/WrmkvP_1RMI/AAAAAAAARIY/7LNDEtnx8uUa2UBsHtfVNseaiCV3VTa8QCLcBGAs/s1600/task_replace_tokens.jpg)

  

_3\. Push the Task to VSTS_

Create a command line Task with node as the tool and the following arguments:

```
.\node\_modules\tfx-cli\ build tasks upload --task-path ./ --service-url https://{YOUR\_INSTANCE}.visualstudio.com/DefaultCollection --token $(pat)
```

[![](https://4.bp.blogspot.com/-Z7ebyC4JQ4Y/Wrna9cGpmII/AAAAAAAARIw/pRuAYHQfRyIJ3MRr8bs7fcaGJuJ-4eU2gCLcBGAs/s640/push.jpg)](https://4.bp.blogspot.com/-Z7ebyC4JQ4Y/Wrna9cGpmII/AAAAAAAARIw/pRuAYHQfRyIJ3MRr8bs7fcaGJuJ-4eU2gCLcBGAs/s1600/push.jpg)


## Conclusion

The above is a very simple example on how we can create a pipeline for our custom tasks. However, there are various things that can be done to minimise chances of error and noise. These things include:

- Creating separate pipelines for build (npm install and update build number) and release (Push)
- As part of building including the PowerShell Task SDK.

The above improvements and others can be made depending on your specific team organisation and preferences. I'll leave that up to you! Thanks for reading.