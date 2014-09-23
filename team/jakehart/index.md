---
layout: page
author: jakehart
title: JakeHart - aka Jake Hartnell
---
{% assign posts = site.posts | where: "author", "jakehart" %}

Jake works at Hypothes.is.

{% include posts_list.html %}
