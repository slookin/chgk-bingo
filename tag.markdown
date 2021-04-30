---
layout: default
title: По тегам
permalink: tags
in_top_menu: True

---
# Site tag
{% assign ttags = "" %}
{% assign rawtags = "" %}
{% for xpage in site.pages %}
	{% assign ttags = xpage.tags | split: " " | join:'|' | append:'|' %}
	{% assign rawtags = rawtags | append:ttags %}
{% endfor %}
{% assign tags = "" %}

{% assign rawtags = rawtags | split: '|' %}

{% for tag in rawtags %}
	{% if tag != "" %}
		{% if tags == "" %}
			{% assign tags = tag | split:'|' %}
		{% endif %}
		{% unless tags contains tag %}
			{% assign tags = tags | join:'|' | append:'|' | append:tag | split:'|' %}
		{% endunless %}
	{% endif %}
{% endfor %}

<ul>
{% for tag in tags %}
{%- if tag != "стандартные_ходы" -%}
<li><b>{{tag}}</b><ul>
{%- for xpage in site.pages -%}
{%- if xpage.tags contains tag -%}
{%- capture xlinks -%}[{{xpage.title}}]({{site.url}}{{xpage.url}}){%- endcapture -%}
<li>{{xlinks|markdownify}}</li>
{%- endif -%}
{%- endfor -%}
{%- endif -%}
</ul>
{% endfor %}
</ul>