---
layout: blank
title: Translation Concordance
---

An automatically-generated list of page translation relationships across this site.

{% assign original_pages = site.pages | where_exp: "item", "item.name != 'redirect.html'" | where_exp: "item", "item.name != 'redirects.json'" | where_exp: "item", "item.name != 'index.md'" | where_exp: "item", "item.original == nil" %}

<table>
  <tr>{% for l in site.data.snippets.language-list %}
    <th>{{ l }}</th>{% endfor %}
  </tr>
  {% for p in original_pages %}
  {% assign reverse_p = p.name | split: "." | first %}
  {% assign translated_pages = site.pages | where: "original", reverse_p %}
  {% assign page_versions =  p | concat: translated_pages %}
  <tr>
    {% for l in site.data.snippets.language-list %}
    {% assign sp = page_versions | where: "lang", l | first %}
    <td><a href="{{sp.url}}">{{ sp.title }}</a></td>
    {% endfor %}
  </tr>
{% endfor %}
</table>
