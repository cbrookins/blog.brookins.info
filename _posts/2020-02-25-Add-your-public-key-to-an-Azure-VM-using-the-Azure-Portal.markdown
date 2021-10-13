---
layout: post
title: Add your public key to an Azure VM using the Azure Portal
date: 2020-02-25
tags: ['azure','microsoft']
---

## Use case  
I had to use this when I lost the private key I used to manage a VM in Azure. This process allows you to add a new public key to the authorized_keys file on the server to regain access.

## Azure Portal 
Log into the Azure portal and select the VM that you need to add your public key to.  
Under **Operations** select **Run Command**.  
Select **RunShellScript** from the list of options.  
In the **Linux Shell Script** text box enter  
  
``printf "<YOUR PUBLIC KEY>" > /home/<yourserverusername>/.ssh/authorized_keys``  
  
Select **Run** and wait for it to complete.  
If you want to append an additional key to **authorized_keys** instead of overwriting the entire file, run the following instead  
  
``printf "\n<YOUR PUBLIC KEY>" >> /home/<yourserverusername>/.ssh/authorized_keys``  
  
You can then enter and run the following to verify the entry  
  
``cat /home/<yourserverusername>/.ssh/authorized_keys``  
  
The result should show the new public key, and you should be able to ssh into the box using the pubkeyauth again.
