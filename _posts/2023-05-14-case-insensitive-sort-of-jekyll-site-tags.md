---
layout: Post
type: Post
status: ⚠️ Draft
date: 2023-05-16
created: 2023-05-16
title: Case Insensitive Sort of Jekyll Site Tags
subtitle: 
theme: Tech
tags: Jekyll Liquid
inspiration: 
---

For the [[By Tag]] page on this site, I wanted to sort the tags alphabetically without regard to case. The solution, while ultimately not difficult, was not obvious.

Jekyll stores all the tags from across the site in a variable named, aptly, `site.tags`. The tags are stored in an order that I assume is based on ISO codes&mdash;all capital letters appear in the sort order before the lower case letters, so 'Zebra' appears before 'anteater'.

There is a Jekyll filter called `sort_natural` that sorts items alphabetically without regard to case. A simple solution, I thought&mdash;but wrong. Sorting `site.tags` with the `sort_natural` filter resulted in a jumbled mess of output. Clearly, I did not understand the structure of `site.tags`.

An [internet search](https://www.assertnotmagic.com/2017/04/25/jekyll-tags-the-easy-way/) disclosed `site.tags` to be an array of tuples, with each tuple consisting of the tag name and the lists of posts containing that tag:

```
tag[0]
  [0] TagName0
  [1] Post0, Post1, ...
tag[1]
  [0] TagName1
  [1] Post0, Post1, ...
...
```

The solution I found is to extract the tag names, sort them into an array in the desired order, then loop back through `site.tags` looking for each tag name in the order of the sorted tag name array.

The other challenge is that Liquid does not allow an array to be populated directly. The standard way to work around that limitation is to create one string with delimiters separating the items and then split the string at the delimiters.

Here is the Liquid code to implement this algorithm (comments are not in Liquid's comment format for brevity):

{% raw %}
```
{%- assign taglist = "" -%} <-- initialize the variable that will hold the tag names
{%- for tag in site.tags -%} <-- loop through the tag tuples in the site variable site.tags
  {%- assign ttag = tag[0] | append:',' -%} <-- extract the tag name from the tuple and append a comma
  {%- assign taglist = taglist | append:ttag -%} <-- append the tag name and comma to the string of comma separated tag names
{%- endfor -%}
{%- assign taglist = taglist | split:',' | sort_natural -%} <-- split the string of comma separated tag names into an array of individual tag names sorted in 'natural' order, meaning case insensitive

{%- for tag in taglist -%} <-- loop through the array of sorted tag names
  {%- if tag != 'Favorite' -%}
    <h2 id="{{ tag }}" class="bylink_h2">{{ tag }}</h2>
    {%- for stag in site.tags -%} <-- loop through the tag tuples in the site variable site.tags
      {%- if stag[0] == tag -%} <-- look for the matching tuple in the site tags
        {%- for post in stag.last -%} <-- list the posts in the matching tuple
          <li class="bylink">
            <a href="{{post.url}}">{{ post.title }}</a>
          </li>
        {%- endfor -%}
      {%- endif -%}
    {%- endfor -%}
  {%- endif -%}
{%- endfor -%}
```
{% endraw %}