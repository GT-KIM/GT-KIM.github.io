---
title: "한국어 글"
layout: archive
permalink: /ko/
author_profile: true
header:
  overlay_image: /assets/images/hero-starfield.jpg
  overlay_filter: "rgba(8, 15, 48, 0.45)"
sidebar:
    nav: "sidebar-category"
---

한국어로 작성한 글 모음입니다. 영어 글은 상단 **English** 탭에서 볼 수 있습니다.

{% assign ko_posts = site.posts | where: "lang", "ko" %}
<div class="entries-list">
{% for post in ko_posts %}{% include archive-single.html type="list" %}{% endfor %}
</div>
{% if ko_posts.size == 0 %}_아직 글이 없습니다._{% endif %}
