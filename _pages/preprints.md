---
layout: page
permalink: /preprints/
title: Preprints
description: Preprints from CLAMS members
years: [2025, 2024, 2023]
nav: false
nav_order:
---
<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f preprints -q @*[year={{y}}]* %}
{% endfor %}

</div>
