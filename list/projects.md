---
title: Projects
narrow: True
permalink: list/projects.html
show_profile: true
---

#### Research Projects

{% for project in site.projects %}
- [{{ project.title }}]({{ site.baseurl }}{{ project.url }})
{% endfor %}

#### Industrial Projects

{% for project in site.projects_industry %}
- [{{ project.title }}]({{ site.baseurl }}{{ project.url }})
{% endfor %}



