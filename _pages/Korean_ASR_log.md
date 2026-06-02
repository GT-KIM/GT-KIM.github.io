---
 title: "Korean ASR · 프로젝트 로그"
 layout: archive
 permalink: /korean_asr/log/
---

OpenKoASR 개발 중 남기는 짧은 노트와 실험 기록입니다.

{% assign posts = site.categories.log %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
