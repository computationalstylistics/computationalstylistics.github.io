---
layout: page
title: People
permalink: /people/
description: Computational Stylistic Group is somewhat unofficial, and so is its membership. Nevertheless at least a few people have been associated with the Group for a while.
---

{% for person in site.people %}


{% if project.redirect %}
<div class="project">
    <div class="thumbnail">
        <a href="{{ project.redirect }}" target="_blank">
        {% if project.img %}
        <img class="thumbnail" src="{{ project.img | prepend: site.baseurl | prepend: site.url }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}    
        <span>
            <h1>{{ project.title }}</h1>
            <br/>
            <p>{{ project.description }}</p>
        </span>
        </a>
    </div>
</div>
{% else %}

<div class="person">
    <div class="thumbnail">
        <a href="{{ person.url | prepend: site.baseurl | prepend: site.url }}">
        {% if person.img %}
        <img class="thumbnail" src="{{ person.img | prepend: site.baseurl | prepend: site.url }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}    
        <span>
            <h1>{{ person.title }}</h1>
            <br/>
            <p>{{ person.description }}</p>
        </span>
        </a>
    </div>
</div>

{% endif %}

{% endfor %}
