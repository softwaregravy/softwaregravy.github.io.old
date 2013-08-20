---
layout: page
title: Accumulating Knowledge
tagline: Thoughts on coding and business
---
{% include JB/setup %}

<div>
  {% for post in site.posts limit:3 %}
    <span>{{ post.date | date_to_string }}</span>
    <h1><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h1>
    {{ post.content | markdownify }}
    <br />
  {% endfor %}
</div>



