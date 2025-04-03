---
layout: portfolio
title: Portfolio
permalink: /clear/
display_categories: ["Computer Science", "Electronics", "Mechanical Engineering"]

subcategory_order:
  Computer Science:
    - Artificial Intelligence
    - Software Development
    - Cybersecurity
    - DevOps and Automation
    - Documentation
    - Data Engineering
    - Firmware Development

  Electronics:
    - Signal and Image Processing
    - PCB Design
    - PCB Reverse Engineering
    - Digital Electronics
    - Digital System Design
    - PCB Repair
    - Power Electronics

  Mechanical Engineering:
    - Control Systems
    - Automation
    - Mechanical Design
    - Analysis and Simulation
    - Materials and Mechanics of Materials
    - Fluid Mechanics

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
