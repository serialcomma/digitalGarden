---
layout: Post
title: By Date
permalink: /dates/
content-type: eg
---

<div>
  {%- assign postsByDay = site.posts | group_by_exp:"post", "post.date | date: '%d-%B-%Y'" -%}
  
  {%- for day in postsByDay -%}
    <h2 id="{{ day.name }}" class="bylink_h2">{{ day.name }}</h2>
        {%- for post in day.items -%}
          <li class="bylink">
            <a href="{{ post.url }}">{{ post.title }}</a>
          </li>
        {%- endfor -%}
  {%- endfor -%}

</div>