---
title: "Python"
layout: archive
permalink: /python
author_profile: true
---


{% assign posts = site.categories.python %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
