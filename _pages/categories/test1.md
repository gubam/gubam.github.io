---
title: "test1"
layout: archive
permalink: categories/programming
author_profile: true
types: posts
---

{% assign posts = site.categories['programming']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
