---
 title: "Korean ASR · 본격 시리즈"
 layout: archive
 permalink: /korean_asr/series/
---

한국어 ASR 평가 방법론과 모델 분석을 깊이 다루는 본격 시리즈입니다.

{% assign posts = site.categories.series %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
