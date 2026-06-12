---
title: "ASR의 진화 시리즈"
layout: archive
permalink: /asr_evolution/
---

고전 음성인식에서 Speech LLM, 그리고 On-device ASR까지 — 음성인식 기술의 큰 흐름을 책 한 권 분량으로 따라가는 장기 연재 시리즈입니다.

{% assign posts = site.categories.asr_evolution %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
