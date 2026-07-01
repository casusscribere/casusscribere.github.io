---
layout: page
title: Projects
---

Standalone tools and experiments deployed alongside this site. Each lives in its
own repository and runs at its own address under this domain.

{% for p in site.data.projects %}
### [{{ p.title }}]({{ p.url }}){% if p.year %} · {{ p.year }}{% endif %}

{{ p.description }}
{% if p.repo %}[source]({{ p.repo }}){% endif %}
{% endfor %}
