---
layout: portfolio
title: Portfolio
permalink: /clear/
display_categories: ["Electronics", "Computer Science", "Mechanical Engineering"]

subcategory_order:
  Computer Science:
    - Firmware Development
    - Cybersecurity
    - Software Development
    - Data Engineering
    - DevOps and Automation
    - Artificial Intelligence
    - Documentation
  Electronics:
    - PCB Design
    - Digital System Design
    - PCB Reverse Engineering
    - Digital Electronics
    - Power Electronics
    - Signal and Image Processing
    - PCB Repair
  Mechanical Engineering:
    - Mechanical Design
    - Analysis and Simulation
    - Fluid Mechanics
    - Materials and Mechanics of Materials
    - Control Systems
    - Automation
---
{% assign about = site.abouts | first %}
{{ about.content }}

<!-- pages/projects.md -->
<div class="projects">
{%- if site.enable_project_categories and page.display_categories %}
  <!-- Parcours des catégories -->
  {%- for category in page.display_categories %}
    {%- assign categorized_projects = site.projects | where: "category", category -%}

    {%- if categorized_projects.size > 0 %}
      
      <!-- Récupération de l'ordre des sous-catégories définies -->
      {%- assign ordered_subcategories = page.subcategory_order[category] -%}

      {%- for subcategory in ordered_subcategories %}
        {%- assign filtered_projects = categorized_projects | where: "subcategory", subcategory | sort: "importance" %}
        
        {%- if filtered_projects.size > 0 %}
          {%- for project in filtered_projects -%}
            {% include projects_portfolio.html %}
          {%- endfor %}
        {%- endif %}
      {%- endfor %}
      
    {%- endif %}
  {% endfor %}

{%- else -%}
  <!-- Affichage sans catégories -->
  {%- assign sorted_projects = site.projects | sort: "importance" -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
{%- endif -%}
</div>

---