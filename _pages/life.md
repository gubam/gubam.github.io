---
title: "categoires"
layout: archive
permalink: /life
---


{% assign posts = site.categories.programming %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
