---
layout: Post
type: Post
status: ⚠️ Draft
date: 2023-05-14
created: 2023-05-14
title: Blockquote Test
subtitle: To Verify the Blockquote Markdown
theme: Tech
tags: 
inspiration: https://tomcritchlow.com/2022/04/27/triple-entry-blogging/
---

This is just some text. I need to type a lot more so that I can see how it looks with longer paragraphs on either side of the blockquote.

[[I got this idea from this website. I also need to see how the blockquote looks with multiple lines.^^Tom Critchlow^^Triple Entry Blogging (and sometimes the title of the citation could be especially long)^^https://tomcritchlow.com/2022/04/27/triple-entry-blogging/::bq]]

That's it. Hope it works!! This ended up taking a few hours to debug. The big problem with this template is there are lots of styles with high specificity that override local selections.

1. one
2. two
3. three

```CSS
code {
  font-family: 'JetBrains Mono', Menlo, Monaco, Consolas, monospace;
  font-weight: 400;
  display: inline-block;
  overflow: auto !important;
  white-space: pre-line !important;
  word-wrap: break-word !important;
  padding: 2px;
  vertical-align: middle;
  border: 1px solid var(--secondary-border-color);
  border-radius: 5px;
}
```