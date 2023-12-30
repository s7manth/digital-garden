---
layout: page
title: Home
id: home
permalink: /
---

<div class="wrap">
<!-- {% assign latest_note = site.notes | sort: "publish_date" | reverse | first %} -->
<!-- <p class="mb0 muted font-ui">
  Latest
</p>
<div>
  <a class="internal-link plain" href="{{ site.baseurl }}{{ latest_note.url }}">
    <h2>{{ latest_note.title }}</h2>
    <div class="small muted pb">
      <time datetime="{{ latest_note.last_modified_at | date: '%Y-%m-%dT%H:%M:%S+00:00' }}">{{ latest_note.last_modified_at | date: "%B %e, %Y" }}</time>
    </div>
    <div class="small muted pb">
      {{ latest_note.summary | strip_html }}
    </div>
    <div class="small muted underline">
      Continue reading →
    </div>
  </a>
</div> -->

<!-- <hr class="mn2 ms2"> -->

<p class="muted font-ui">
  Living Documents
</p>
<div class="doclinks">
{% assign docs = site.ldocs %}
{% for p in docs %}
  {% if p.publish == true %}
  <a class="doclink plain internal-link" href="{{ site.baseurl }}{{ p.permalink }}">
    <h2 class="st sb">
      {{ p.title }}
    </h2>
  </a>
  {% endif %}
{% endfor %}
</div>

<p class="muted">
Have any suggestions? Reach out <a class="internal-link underline" href="mailto:syalamarty002@gmail.com?subject=Hey, Sumanth!">here</a>!
</p>

<hr class="mn2 ms2">

<p class="muted font-ui mb0">
  Past Musings
</p>
<div>
{% assign recent_notes = site.notes | sort: "publish_date" | reverse %}
<ul class="list-plain tabular-nums pt0">
{% for note in recent_notes %}
  <li>
    <a class="internal-link plain" href="{{ site.baseurl }}{{ note.url }}">
      <div class="flex align-baseline space-between">
        <h2>{{ note.title }}</h2>
        <div class="small muted ppl flex-shrink mh nowrap font-ui">
          <time datetime="{{ note.publish_date | date: '%Y-%m-%dT%H:%M:%S+00:00' }}">
            {{ note.publish_date | date: "%Y · %m" }}
          </time>
        </div>
      </div>
      <div class="small muted pb">
        {{ note.summary | strip_html }}
      </div>
    </a>
    </li>
{% endfor %}
</ul>
</div>
</div>
