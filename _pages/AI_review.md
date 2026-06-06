---
 title: "AI Review"
 layout: archive
 permalink: /ai_review/
---

직접 읽고 정리한 AI·딥러닝 논문 리뷰입니다.

{% assign posts = site.categories.ai_review %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% if posts.size == 0 %}_아직 공개된 글이 없습니다. 곧 채워집니다._{% endif %}