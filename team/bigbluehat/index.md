---
layout: default
author: bigbluehat
title: BigBlueHat - aka Benjamin Young
---
{% assign posts = site.posts | where: "author", "bigbluehat" %}

## {{ page.title }}

Benjamin works as the Developer Advocate at Hypothes.is.

Writes codes, blogs, and emails.

Drinks :coffee:.

#### Posts

{% include posts_list.html %}
