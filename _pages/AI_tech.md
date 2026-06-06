---
 title: "AI Tech"
 layout: archive
 permalink: /ai_tech/
---

모델 학습·추론·분산 처리 등 AI 엔지니어링 실전 노트입니다.

{% assign posts = site.categories.ai_tech %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% if posts.size == 0 %}_아직 공개된 글이 없습니다. 곧 채워집니다._{% endif %}