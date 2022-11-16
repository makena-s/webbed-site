---
title: coolpages
---
# coolpages

<ul>
  {% for coolpage in site.coolpages %}
    <li>
      <h2><a href="{{ coolpage.url | relative_url }}">{{ coolpage.title }}</a></h2>
      <p>{{ coolpage.content | markdownify }}</p>
      <!-- convert markdown string to HTML, though i doubt it matters since i changed this page to markdown -->
    </li>
  {% endfor %}
</ul>
