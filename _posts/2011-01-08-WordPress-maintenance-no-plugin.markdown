---
layout: post
title: WordPress maintenance no plugin
date: 2011-01-08
---

I have been using this for a while on some of the Wordpress sites that I run, but when you havent done it in a while and you forget finding it again seems to be a problem. Instead of relying on Google, I am posting this here so that I can find it easily in the future.  

I came across this on someone elses blog some time ago and it was very handy for what I needed done. This simple php allows you to put your Wordpress site into maintenance mode with no need for any plugins.  

All you need to do is create a file named .maintenance  

Add the following code to the file  

  
<pre> $value ) {  
        if ( stristr($cookie, 'wordpress_logged_in_') )  
            $loggedin = true;  
    }  
    return $loggedin;  
}  
if ( ! stristr($_SERVER['REQUEST_URI'], '/wp-admin') && ! stristr($_SERVER['REQUEST_URI'], '/wp-login.php') && ! is_user_logged_in() )  
    $upgrading = time();  
else  
    $upgrading = 0;  
?&gt;</pre>  

   

Then upload it into the root folder of your Wordpress site. Simple as that. This will allow you admin access to your site but visitors will see a maintenance screen. This is a basic setup, but you can make modifications to the file and customize it to your liking.  

If you would like additional information or help taking this to the next level you can check out the source of this article using the links below.  

<a href="http://sivel.net/2009/06/wordpress-maintenance-mode-without-a-plugin/" target="_blank">Wordpress Maintenance Mode without a Plugin, Part 1</a>  

<a href="http://sivel.net/2009/06/wordpress-maintenance-mode-without-a-plugin-part-2/" target="_blank">Wordpress Maintenance Mode without a Plugin, Part 2</a>  

<a href="http://sivel.net/2009/10/wordpress-maintenance-mode-without-a-plugin-part-3/" target="_blank">Wordpress Maintenance Mode without a Plugin, Part 3</a>",
