---
bg: "script.gif"
layout: post
title: Set up a push mirror on Codeberg
date: 2023-06-27
tags: ['workflow','script','git']
---

I made the move to Codeberg, but still wanted to keep a presence on GitHub. I decided to set up a mirror on Codeberg that automatically send over to GitHub when commits were pushed. This writing assumes you already have a functional git repo on Codeberg that you want to mirror to GitHub.

### GitHub
On **GitHub** create a new, empty, repository.  
Grab the **HTTPS** URL from the **Quick setup** page, you will need this once we switch to Codeberg  
![github quick setup](https://github.com/cbrookins/tech.brookins.info/raw/main/assets/images/codeberg_mirror_01.png "github quick setup")  
Now head to the top right corner of GitHub and select your username  
Select **Settings** from the menu  
On the left hand menu of your profile page select **Developer Settings**  
Select **Personal access tokens** > **Fine-grained tokens**
Select **Generate new token**  
Fill out the token form    
![github fine-grained](https://github.com/cbrookins/tech.brookins.info/raw/main/assets/images/codeberg_mirror_02.png "github fine-grained")  
I believe the expiration is capped at one year  
You can provide repository access to all repositories but I recommend you make an access token for each indvidual mirror  
Now under **Permissions** > **Repository permissions** > **Contents** select **Read and write**  
Select **Generate token**  
Copy the token that is generated you will need this for Codeberg  

### Codeberg
Now on **Codeberg** open the repository you want to mirror  
Select **Settings** and scroll down to **Mirror Settings**  
![codeberg mirror](https://github.com/cbrookins/tech.brookins.info/raw/main/assets/images/codeberg_mirror_03.png "codeberg mirror")  
Paste the **HTTPS URL** into the **Git Remote Repository URL** field  
Drop down **Authorization**  
Enter your **GitHub username** for **Username**  
Enter the **Generated token from GitHub** for the password  
Select the checkbox for **Syn when commits are pushed**  
Set the **Mirror interval** how you like, I left the default  
Select **Add Push Mirror** button  
Select the **Synchronize Now** button to test your new mirror