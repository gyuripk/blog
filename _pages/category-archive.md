---
title: "Posts by Category"
layout: categories
permalink: /categories/
author_profile: true
---
{% include group-by-array collection=site.posts field="categories" %}
{% for category in group_names %}
  {% assign posts = group_items[forloop.index0] %}
{% endfor %}
