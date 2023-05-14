---
layout: Post
title: By Tag
permalink: /tags/
content-type: eg
---

<div>

{%- comment -%}
The site.tags variable that is available to you in Jekyll templates is an interesting structure. If you access it like a dictionary (or dict, or hash, depending on your language of choice), – e.g. site.tags["nematodes"] – you will receive a list of the posts that have that tag. If you loop through site.tags directly, each item can work as a tuple: (tag name, list of posts with this tag)
See -- https://www.assertnotmagic.com/2017/04/25/jekyll-tags-the-easy-way/
{%- endcomment -%}

{%- assign taglist = "" -%}
{%- for tag in site.tags -%}
	{%- assign ttag = tag[0] | append:',' -%}
	{%- assign taglist = taglist | append:ttag -%}
{%- endfor -%}
{%- assign taglist = taglist | split:',' | sort_natural -%}

{%- for tag in taglist -%}
  {%- if tag != 'Favorite' -%}
    <h2 id="{{ tag }}" class="bylink_h2">{{ tag }}</h2>
    {%- for stag in site.tags -%}
      {%- if stag[0] == tag -%}
        {%- for post in stag.last -%} 
          <li class="bylink">
            <a href="{{post.url}}">{{ post.title }}</a>
          </li>
        {%- endfor -%}
      {%- endif -%}
    {%- endfor -%}
  {%- endif -%}
{%- endfor -%}
</div>