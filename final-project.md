---
layout: page
title: Final Project
permalink: /final-project/
---

<div>
  {% for final in site.finals %}
    <div>
      <h2><a href="{{ final.url | prepend: site.baseurl }}">{{ final.title }}</a></h2>
      <p>{{ final.description }}<p>
  {% endfor %}
<!---Note: Liquid syntax seems to close open tags without adding them--->