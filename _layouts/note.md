---
layout: default
---

<div class="note-content">

<h1 class="content-title">
{{ page.date | date: "%x" }}

{% if page.title %}
 | {{ page.title }}
{% endif %}

</h1>

{{ content }}

<div>
