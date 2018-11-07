---
title: 'Azure SDK 2.4 to 2.5 upgrade. Error: "''Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment'' exists in both ''Microsoft.WindowsAzure.ServiceRuntime.dll'' and ''Microsoft.WindowsAzure.ServiceRuntime.dll"'
date: 2015-03-11T09:51:00.001+11:00
draft: false
---

If you're getting this error while calling the type 'RoleEnvironments' then there is probably something wrong with the Visual Studio migration of Azure 2.4 to 2.5.  
  
To fix this issue simply remove then add references to the DLL Microsoft.WindowsAzure.ServiceRuntime.dll to the project that's calling 'RoleEnvironments'.