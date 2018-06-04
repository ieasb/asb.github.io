---
layout: page
title: Tags
comments: false
permalink: /tags/
---

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
<!-- site_tags: {{ site_tags }} -->
{% assign tag_words = site_tags | split:',' | sort %}
<!-- tag_words: {{ tag_words }} -->
 
<div id="tags">
  <ul class="tag-box inline">
  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
    <li><a href="#{{ this_word | cgi_escape }}">{{ this_word }} - <span>{{ site.tags[this_word].size }} Post(s)</span></a></li>
  {% endunless %}{% endfor %}
  </ul>

  <hr>
 
  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
  <h2 id="{{ this_word | cgi_escape }}">{{ this_word }}</h2>
  <ul class="posts">
    {% for post in site.tags[this_word] %}{% if post.title != null %}

    {% assign month = post.date | date: "%-m" | minus: 1 %}
    {% assign day_part = post.date | date:'%d' %}
    {% assign month_part = site.data.locale.months[month] %}
    {% assign year_part = post.date | date:'%Y' %}
    {% assign post_formatted_date = day_part | append: " " | append: month_part | append: ", " | append: year_part %}

    <li itemscope>
      <span class="entry-date">
        <time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post_formatted_date }}</time>
      </span> &raquo;
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
    {% endif %}{% endfor %}
  </ul>
  <hr>
  {% endunless %}{% endfor %}

</div>
