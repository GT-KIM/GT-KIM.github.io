---
 title: "Python"
 layout: archive
 permalink: /python/
---

개발 환경 설정과 Python 활용 팁을 정리합니다.

{% assign posts = site.categories.python %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% if posts.size == 0 %}_아직 공개된 글이 없습니다. 곧 채워집니다._{% endif %}