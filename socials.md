---
layout: page
title: "Socials"
crawlertitle: "Socials"
summary: ""
active:
---

{% if site.twitter_username %}
[@{{site.twitter_username}}](https://twitter.com/{{site.twitter_username}})
{% endif %}

{% if site.github_username %}
[{{site.github_username}}](https://github.com/{{site.github_username}})
{% endif %}

{% if site.mastodon_username %}
[{{site.mastodon_username}}]({{site.mastodon_url}}){:rel="me"}
{% endif %}
