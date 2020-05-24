---
title: "Gillespedia"
permalink: /categories/
layout: archive
author_profile: true
---


Aaron's Public Knowledge Wiki.  
[See Simple List]({{siteurl}}/gillespedia/){: .btn .btn--primary}

{% for member in site.data.gillespediatags %}
<section id="{{ member.tag | slugify | downcase }}" class="taxonomy__section">
![tag doodle]({{member.image}}){:height="100px" width="300px"}
<h2 class="archive__subtitle">{{member.tag | upcase}}</h2>
<ul>
{% assign sorted = (site.gillespedia | sort: 'date') | reverse %}
  {% for item in sorted %}
    {% for tag in item.categories %}
      {% if tag == member.tag %}
        <li><a href="{{site.url}}{{site.baseurl}}{{item.url}}">{{ item.title }}</a></li>
      {% endif %}
    {% endfor %}
  {% endfor %}
</ul>
</section>
{% endfor %}
