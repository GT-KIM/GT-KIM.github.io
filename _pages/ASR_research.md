---
title: "ASR 연구"
layout: archive
permalink: /asr_research/
---

음성 인식(ASR)을 둘러싼 연구 노트와 단상을 모으는 공간입니다. 멀티모달 LLM 시대에 음성 인식의 자리, 평가와 한계, 그리고 떠오르는 질문들을 자유로운 형식으로 다룹니다. 기술의 발전사를 체계적으로 따라가는 글은 [ASR의 진화 시리즈](/asr_evolution/)에 있습니다.

{% assign posts = site.categories.asr_research %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
