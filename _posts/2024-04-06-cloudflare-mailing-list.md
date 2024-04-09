---
bg: "server_.gif"
layout: post
title: Cloudflare mailing list
date: 2024-04-06
tags: ['email','cloudflare','workers']
---

I have used **Google Domains** for the past five years or so.  One of the weirdest things about their email service was that if you wanted a mailing list you had to set up a **Google Group**.  When Google Domains decided to shut down I made the jump to **Cloudflare**.  At the time you could not set up mailing lists with Cloudflare, so I just forwarded the email address to that same Google Group.  Recently Cloudflare introduced **Email Workers**, which I found could do what I needed of a mailing list.

### Email Workers
Cludflare email workers ***"allow you to create custom scripts and process your emails according to your specific requirements"***.

### Create an Email Worker
Creating an email worker is pretty straight forward.  From the Cloudflare dashboard, select **Websites** > **your domain** > **Email** > **Email Workers** tab.

Now select the **Create** button.

![none](https://github.com/cbrookins/tech.brookins.info/raw/main/assets/images/cloudflare_email_worker_01.png "none")

![none](https://github.com/cbrookins/tech.brookins.info/raw/main/assets/images/cloudflare_email_worker_02.png "none")

![none](https://github.com/cbrookins/tech.brookins.info/raw/main/assets/images/cloudflare_email_worker_03.png "none")

The following is the code I used

```
export default {
  async email(message, env, ctx) {
    const forwardList = ["user1@email.domain","user2@email.domain"];
    for(const email of forwardList){
      await message.forward(email);
    }
  }
}
```

Once that is completed you need to create a ***Email route***.  Here you determine the email address you want to use and email sent to that address will go to your Email Worker.

![none](https://github.com/cbrookins/tech.brookins.info/raw/main/assets/images/cloudflare_email_route_01.png "none")

That is it.  Now mail sent to the email address of the route will go to the worker and then forward to the addresses in your forwardList.