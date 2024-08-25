---
layout: page
permalink: /publications/
title: Publications
description: Peer-reviewed publications from CLAMS members
years: [2024, 2023, 2022, 2020, 2019, 2018, 2013]
nav: false
nav_order:
---
<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
