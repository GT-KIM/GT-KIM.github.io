---
 title: "Daily"
 layout: archive
 permalink: /daily/
---

연구와 개발을 하며 남기는 짧은 일상 기록입니다.

{% assign posts = site.categories.daily %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% if posts.size == 0 %}_아직 공개된 글이 없습니다. 곧 채워집니다._{% endif %}