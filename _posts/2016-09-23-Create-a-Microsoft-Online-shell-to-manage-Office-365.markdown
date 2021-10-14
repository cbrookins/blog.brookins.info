---
bg: "windows.gif"
layout: post
title: Create a Microsoft Online shell to manage Office 365
date: 2016-09-23
tags: ['microsoft','office 365','windows']
---

## Install Module
*Installing modules must be done with an administrator Powershell window*  
``install-module msonline``  
``install-module azuread``  


## Create MSOnlineStartup.ps1 without credential file
*This options will prompt you for a password each time you launch the shortcut*

``$UserCredential = Get-Credential``  
``Connect-MsolService -Credential $UserCredential``

## Create MSOnlineStartup.ps1 that uses a credential file
*This option will auto log you in using your O365 credntials*

``$UserCredential = Import-CliXML -path ".\credentials.creds"``  
``Connect-MsolService -Credential $UserCredential``

## Create credential file
``$password = ConvertTo-SecureString -string "<your password>" -AsPlainText -Force``  
``New-Object System.Management.Automation.PSCredential("<user name>", $password) | Export-CliXml -path "$env:userprofile\Scripts\MSOnline\credentials.creds"``

## Create Shortcut
powershell.exe -noexit import-module msonline; .\msonlinestartup.ps1

The startup folder should be the path to the folder where you saved msonlinestartup.ps1 file.
