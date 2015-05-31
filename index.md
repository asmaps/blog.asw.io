---
layout: page
title: ASW Blog
tagline: Supporting tagline
---
{% include JB/setup %}

{% for post in site.posts %}
<h2>
<a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
<small><em><span>{{ post.date | date_to_string }}</span></em></small>
</h2>
<div>
{{ post.content | truncatewords:35 }}
</div>
<div>
</div>
{% if forloop.last != true %}
<hr>
{% endif %}
{% endfor %}
