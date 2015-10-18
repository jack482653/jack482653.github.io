---
layout: index
title: Xian's note
tagline:
---
{% include JB/setup %}

{% for post in site.posts limit:10 %}
  <section class="section">
    <article>
      <div class="page-header">
        <h1>
          <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
        </h1>
      </div>
      <div class="date">
        <span>{{ post.date | date_to_long_string }}</span>
      </div>
      <div class="note post-info">
        分類: <a href="categories.html#{{ post.category }}-ref">{{ post.category }}</a>
      </div>

      {% if post.content contains "<!-- more -->" %}
        {{ post.content | split: "<!-- more -->" | first % }}
      {% else %}
        {{ post.content | strip_html | truncatewords:100 }}
      {% endif %}

      <div class="read-more">
        <a class="btn " href="{{ BASE_PATH }}{{ post.url }}">Read more...</a>
      </div>
    </article>
  </section>
{% endfor %}
