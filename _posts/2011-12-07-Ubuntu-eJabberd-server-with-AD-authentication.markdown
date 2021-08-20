---
layout: post
title: Ubuntu eJabberd server with AD authentication
date: 2011-12-07
---

*ejabberd is a Jabber/XMPP instant messaging server, licensed under GPLv2 (Free and Open Source), written in Erlang/OTP. Among other features, ejabberd is cross-platform, fault-tolerant, clusterable and modular.* - <a href="http://www.ejabberd.im/" title="eJabberd" target="_blank">eJabberd</a>  

This tutorial covers the installation of eJabberd, using Ubuntu Server 10.04.3, and configuring it to integrate with Active Directory authentication.  This same setup will work with just about any other LDAP server with very few, if any, changes.  

  
The first thing is to install Ubuntu Server 10.04.  

You will want to update your server before getting started  
`sudo aptitude update && sudo aptitude safe-upgrade`  


Install ejabberd  
`sudo aptitude install ejabberd`  


Configure ejabberd  
`sudo nano /etc/ejabberd/ejabberd.cfg`  


Edit the **%%Hostname** section to match your environment  

    %% Hostname  
    {hosts, ["localhost", "domain.local"]}.  
    
    
    Configure the LDAP settings as needed  
    
    %% Authentication using LDAP  
    {auth_method, ldap}.  
    %%  
    %%  
    %% List of LDAP servers:  
    {ldap_servers, ["dc02.domain.local", "dc01.domain.local"]}.  
    %%  
    %%  
    %% LDAP manager:  
    {ldap_rootdn, "cn=test user,ou=people,dc=domain,dc=local"}.  
    %%  
    %% Password to LDAP manager:  
    {ldap_password, "5up3rs3cr3+p455w0rd"}.  
    %%  
    %% Search base of LDAP directory:  
    {ldap_base, "dc=domain,dc=local"}.  
    %%  
    %% LDAP attribute that holds user ID:  
    {ldap_uids, [{"sAMAccountName", "%u"}]}.  
    %%  
    %% LDAP filter:  
    {ldap_filter, "(memberOf=CN=jabberusers,OU=groups,OU=domain,OU=local)"}.  


**Note: You can use a * in the ldap_filter to include all domain users.**  

Configure the Access Control List  

    %%% ====================  
    %%% ACCESS CONTROL LISTS  
    %%  
    %% Admin user  
    {acl, admin, {user, "administrator", "localhost"}}.  
    {acl, admin, {user, "administrator", "domain.local"}}.  


Save the configuration  
**ctrl+x** to exit nano  
**y** to save the changes  

Now restart ejabberd  
`sudo /etc/init.d/ejabberd restart`  


You should now have a working Jabber server.  Configure your Jabber client of choice with the server name, or IP, and your domain crendentials and chat away.  

ejabberd has a lot more options than the ones I covered in this tutorial, but these are the basics to get your Jabber server authenticating against Active Directory.  You may want to look at the documentation provided by the <a href="http://www.ejabberd.im/" title="eJabberd" target="_blank">eJabberd</a> project for other tweaks and configuration options.
