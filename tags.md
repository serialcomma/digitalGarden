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

By default, the tags are ordered in hexcode order, which means the capital letters are sorted before the lower case letters. The first code block sorts the tag names in a case-insensitive order.
* The first line initializes the variable that will hold the tag names
* The second line loops through the tag tuples in the site variable site.tags
* The third line extracts the tag name from the tuple and appends a comma
* The fourth line appends the tag name and comma to the string of comma separated tag names
* The fifth line ends the loop
* The sixth line splits the string of comma separated tag names into an array of individual tag names sorted in 'natural' order, meaning case insensitive

The second code block loops through the array of sorted tag names, then looks for the matching tuple in the site tags (if stag[0] == tag), then lists the posts in the matching tuple.
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