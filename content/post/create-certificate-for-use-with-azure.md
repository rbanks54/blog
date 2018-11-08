---
title: 'Create certificate for use with Azure PowerShell cmdlets'
date: 2015-04-17T14:53:00.000+10:00
draft: false
tags : [.net, alm, azure, devops, powershell]
---

There are two ways to access your Azure subscription from PowerShell(PS). The first is to use Add-AzureAccount and subsequently be greeted with a login. The other way is to use Set-AzureSubscription and use certificates.  
  
  
Below is the method of using certificates for more fluid scripts.  

  

1.  Open visual studio command prompt as an administrator. This is located under your Visual Studio family of applications.   
    
    [  
    ](http://1.bp.blogspot.com/-emL1VZtsNSQ/VTCP4jFr1YI/AAAAAAAAHOU/hEPLEReEMAQ/s1600/uploadToAzure.png)[![](http://3.bp.blogspot.com/-VBgTLVG4mKU/VTCIzMxlFDI/AAAAAAAAHNk/Lha5fjEslGk/s1600/VSCommandPromt.png)](http://3.bp.blogspot.com/-VBgTLVG4mKU/VTCIzMxlFDI/AAAAAAAAHNk/Lha5fjEslGk/s1600/VSCommandPromt.png)
    
2.  run this command (replacing <NameOfYourCert> with a name)  
    makecert -sky exchange -r -n "CN=<NameOfYourCert>" -pe -a sha1 -len 2048 -ss My "<NameOfYourCert>.cer"
3.  Run certmr.msc by searching it on your start menu.
4.  Navigate to Personal -> Certificates and find your certificate. Right click your certificate and click 'Export...'[![](http://4.bp.blogspot.com/-gQLXuUkN_Lk/VTCNZO9hIpI/AAAAAAAAHNw/_t85fgeBFTQ/s1600/export1.png)](http://4.bp.blogspot.com/-gQLXuUkN_Lk/VTCNZO9hIpI/AAAAAAAAHNw/_t85fgeBFTQ/s1600/export1.png)
5.  Run through the wizard selecting all default options. Do not export your private key and save your certificate anywhere on your desktop
    
    [![](http://2.bp.blogspot.com/-h-k48IwRjSs/VTCOWY9YzNI/AAAAAAAAHN4/n5gokhu49kA/s1600/export2.png)](http://2.bp.blogspot.com/-h-k48IwRjSs/VTCOWY9YzNI/AAAAAAAAHN4/n5gokhu49kA/s1600/export2.png)
    
    [![](http://4.bp.blogspot.com/-DiDsDoadPTo/VTCOlmZWClI/AAAAAAAAHOA/mNWoxGSg7oY/s1600/export3.png)](http://4.bp.blogspot.com/-DiDsDoadPTo/VTCOlmZWClI/AAAAAAAAHOA/mNWoxGSg7oY/s1600/export3.png)
    
    [![](http://1.bp.blogspot.com/-w_P2AUEWpG4/VTCO4vTyyPI/AAAAAAAAHOI/6dwk_BQWNPQ/s1600/export4.png)](http://1.bp.blogspot.com/-w_P2AUEWpG4/VTCO4vTyyPI/AAAAAAAAHOI/6dwk_BQWNPQ/s1600/export4.png)
    
6.  Log into Azure go to Settings and Import your certificate  
    [![](http://1.bp.blogspot.com/-emL1VZtsNSQ/VTCP4jFr1YI/AAAAAAAAHOU/hEPLEReEMAQ/s1600/uploadToAzure.png)](http://1.bp.blogspot.com/-emL1VZtsNSQ/VTCP4jFr1YI/AAAAAAAAHOU/hEPLEReEMAQ/s1600/uploadToAzure.png)  
    [![](http://4.bp.blogspot.com/-7UNGXB7Yi-A/VTCQbx2pEZI/AAAAAAAAHOc/bEHkFHAJYt4/s1600/uploadToAzure2.png)](http://4.bp.blogspot.com/-7UNGXB7Yi-A/VTCQbx2pEZI/AAAAAAAAHOc/bEHkFHAJYt4/s1600/uploadToAzure2.png)
7.  Once uploaded you should see your management certificate appear and you will be able to run the PowerShell script below. You should be able to see the SubscriptionId and Thumbprint from the first screenshot from step 6.  
    Set-AzureSubscription -SubscriptionId "<YourSubscriptionIdFromAzure>" -Certificate (Get-Item "Cert:\\CurrentUser\\my\\$<YourCertificateThumbprint>")