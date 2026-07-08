---
layout: page
title: Projects
---

Standalone tools and experiments deployed alongside this site. Each lives in its
own repository and runs at its own address under this domain.

Every project here was built independently with AI assistance. Where noted, each
entry lists roughly *how* AI was used and what it cost to make — the model(s), an
approximate token count, and the time involved — so you can gauge what building
something like it might take.

{% for p in site.data.projects %}
### [{{ p.title }}]({{ p.url }}){% if p.year %} · {{ p.year }}{% endif %}

{{ p.description }}
{% if p.repo %}[source]({{ p.repo }}){% endif %}

{% if p.ai_use %}- **How AI was used:** {{ p.ai_use }}
{% endif %}{% if p.models %}- **Model(s):** {{ p.models }}
{% endif %}{% if p.tools %}- **AI tool:** {{ p.tools }}
{% endif %}{% if p.tokens %}- **Approx. tokens:** {{ p.tokens }}
{% endif %}{% if p.cost %}- **Approx. cost:** {{ p.cost }}
{% endif %}{% if p.time %}- **Build time:** {{ p.time }}
{% endif %}{% if p.sessions %}- **Sessions:** {{ p.sessions }}
{% endif %}{% if p.prompts %}- **Prompts / turns:** {{ p.prompts }}
{% endif %}{% if p.human_role %}- **Human's role:** {{ p.human_role }}
{% endif %}{% if p.stack %}- **Built with:** {{ p.stack }}
{% endif %}{% if p.ai_assist %}- **AI-written share:** {{ p.ai_assist }}
{% endif %}{% if p.difficulty %}- **Difficulty:** {{ p.difficulty }}
{% endif %}{% if p.status %}- **Status:** {{ p.status }}
{% endif %}{% if p.lessons %}- **Takeaway:** {{ p.lessons }}
{% endif %}
{% endfor %}
