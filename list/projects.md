---
title: Projects
narrow: True
permalink: list/projects.html
show_profile: true
---
#### 2024

{% for project in site.projects_2024 %}
- [{{ project.title }}]({{ project.url }})
{% endfor %}

#### 2023

{% for project in site.projects_2023 %}
- [{{ project.title }}]({{ project.url }})
{% endfor %}

#### 2022

{% for project in site.projects_2022 %}
- [{{ project.title }}]({{ project.url }})
{% endfor %}

#### 2021

{% for project in site.projects_2021 %}
- [{{ project.title }}]({{ site.baseurl }}{{ project.url }})
{% endfor %}

#### 2020

{% for project in site.projects_2020 %}
- [{{ project.title }}]({{ site.baseurl }}{{ project.url }})
{% endfor %}




