---
 title: "Home"
 layout: archive
 permalink: /home
---

{% assign posts = site.categories %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}