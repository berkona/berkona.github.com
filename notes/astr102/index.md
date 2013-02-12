---
layout: note-index
title: ASTR 102
title_detail: Notes from ASTR102 - Stars Spring 2013
syllabus: syllabus.html
---

{% for post in site.categories.astr102 %}
{% include note-list-item.html %}
{% endfor %}
