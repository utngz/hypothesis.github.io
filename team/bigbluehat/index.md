---
layout: page
author: bigbluehat
title: BigBlueHat - aka Benjamin Young
---
{% assign posts = site.posts | where: "author", "bigbluehat" %}

Benjamin works as the Developer Advocate at Hypothes.is.

Writes codes, blogs, and emails.

Drinks :coffee:.

{% include posts_list.html %}
