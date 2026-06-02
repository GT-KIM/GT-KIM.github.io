---
 title: "Korean ASR Leaderboard Project"
 layout: archive
 permalink: /korean_asr/
---

한국어 ASR 모델을 동일한 평가 파이프라인으로 비교하는 OpenKoASR 프로젝트의 기록입니다.
방법론과 분석을 다루는 **본격 시리즈**, 그리고 짧은 개발 노트인 **프로젝트 로그**로 나뉩니다.

- [Live Leaderboard](https://gt-kim.github.io/open-korean-automatic-speech-recognition/)
- [GitHub Repository](https://github.com/GT-KIM/open-korean-automatic-speech-recognition)

{% assign posts = site.categories.korean_asr %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
