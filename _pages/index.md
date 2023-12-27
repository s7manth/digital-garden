---
layout: page
title: Home
id: home
permalink: /
---

<div class="wrap">
<p class="muted font-ui">
    Latest
</p>
<div>
  {% assign latest_note = site.notes | sort: "last_modified_at_timestamp" | reverse | first %}
  <a class="internal-link plain" href="{{ site.baseurl }}{{ latest_note.url }}">
    <h2>{{ latest_note.title }}</h2>
    <div class="muted small pb font-ui">
      <time datetime="{{ latest_note.last_modified_at | date: '%Y-%m-%dT%H:%M:%S+00:00' }}">{{ latest_note.last_modified_at | date: "%B %e, %Y" }}</time>
      <span></span>
    </div>
    <div class="small muted">
      {{ latest_note.content | strip_html | truncatewords: 5, "...Keep reading →" }}
    </div>
  </a>
</div>

<hr class="mn2 ms2" />
<p class="muted font-ui">
    Writing
</p>
<ul class="list-plain tabular-nums">
  {% assign recent_notes = site.notes | sort: "last_modified_at_timestamp" | reverse %}
  {% for note in recent_notes %}
    <li>
        <a class="internal-link plain" href="{{ site.baseurl }}{{ note.url }}">
            <flex class="align-baseline">
                <span class="muted ppr flex-shrink small mh nowrap font-ui">{{ note.last_modified_at | date: "%Y &#183; %m" }}</span>
                <u>{{ note.title }}</u>
            </flex>
        </a>
    </li>
  {% endfor %}
</ul>
</div>