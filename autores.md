---
layout: page
title: Autores
comments: false
permalink: /autores/
---

<div id="authors">
{% for author in site.data.authors %}
<h3 id="{{ author[1].username }}">{{ author[1].name }}</h3>
{% if author[1].assets %}
  <amp-img width="100" height="100" class="author-thumb-post" layout="responsive" src="{{ author[1].assets | relative_url }}" alt="{{ author[1].name }}"></amp-img>
{% endif %}
<p class="mb4 px3" align="justify">{{author[1].bio}}</p>
<p>Publicaciones:</p>
<ul class="posts">
{% for post in site.posts %}
{% if author[1].username == post.author %}
{% if post.title != null %}
<li itemscope>
  <span class="entry-date">
    <time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post.date | date: "%B %d, %Y" }}</time>
  </span>
  &raquo;
  <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
</li>
{% endif %}
{% endif %}
{% endfor %}
</ul>
<hr>
{% endfor %}
</div>
