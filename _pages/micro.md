---
title: "micro"
layout: archive
permalink: /micro
author_profile: true
---


{% assign posts = site.categories.micro %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
