---
layout: main
title: RoboCasa
subtitle: 
project_tagline: "Large-Scale Simulation of Household Tasks for Generalist Robots"
videoId: 
---

<!-- Grid of Videos -->
<div class="video-grid-3x3">
  {% for video in site.static_files %}
    {% if video.path contains '/assets/videos/env_grid/' %}
      <div class="video-item">
        <video autoplay loop muted playsinline>
          <source src="{{ site.baseurl }}{{ video.path }}" type="video/mp4">
        </video>
      </div>
    {% endif %}
  {% endfor %}
</div>

<!-- <figure class="figure">
  <div class="figure__main">
    <video autoplay loop muted playsinline class="postimagefullwidth">
      <source src="{{ site.baseurl }}/assets/videos/env_grid.mp4" type="video/mp4">
    </video>
  </div>
</figure> -->

**RoboCasa** is a large-scale simulation framework for training generalist agents in household environments. It features realistic and diverse scenes with a focus on kitchen environments which we enhance we the help of AI generation tools. In addition we provide over 1000 3D assets across 83 object categories and dozens of intractable appliances. These assets support diverse behaviors and we propose a set of 75 tasks, including tasks representing complex activities that we generated with the guidance of large language models. We include a set of high-quality demonstrations for each task and explore the use of robot data generation tools to significantly expand the scope of our dataset at little additional cost.

## AI Generated Textures

<figure class="figure">
  <div class="figure__main">
    <video autoplay loop muted playsinline class="postimagefullwidth">
      <source src="{{ site.baseurl }}/assets/videos/ai_textures.mp4" type="video/mp4">
    </video>
  </div>
</figure>

Each scene can be customized by replacing textures from a large selection of high-quality AI-generated textures, created using the popular text-to-image AI-generation tool MidJourney. There are 100 textures for walls, 100 for the floor, 100 for counters, and 100 for cabinet panels. These textures can be used as a form of domain randomization to significantly increase the visual diversity of our training datasets.

## Interactable Appliances
<div class="video-grid-2x2">
  {% for video in site.static_files %}
    {% if video.path contains '/assets/videos/appliance_grid/' %}
      <div class="video-item">
        <video autoplay loop muted playsinline>
          <source src="{{ site.baseurl }}{{ video.path }}" type="video/mp4">
        </video>
      </div>
    {% endif %}
  {% endfor %}
</div>

The **RoboCasa** simulation framework comes with dozens of appliances. Several types of appliances are articulated. For example, a robot can open and close doors on microwaves and twist knobs on stoves. These appliances additionally can undergo state changes, e.g., when a knob on the stove is turned, the corresponding burner turns on.

## Diverse Robots
<div class="video-grid-2x2">
  {% for video in site.static_files %}
    {% if video.path contains '/assets/videos/robot_grid/' %}
      <div class="video-item">
        <video autoplay loop muted playsinline>
          <source src="{{ site.baseurl }}{{ video.path }}" type="video/mp4">
        </video>
      </div>
    {% endif %}
  {% endfor %}
</div>

**RoboCasa** supports mobile manipulators of diverse form factors, such as single-arm mobile manipulators, humanoids, and quadruped robots.


## Foundational Robot Skills
<div class="video-slide">
  <div>
    <video autoplay loop muted playsinline>
      <source src="{{ site.baseurl }}/assets/videos/basic_skills/pnp.mp4" type="video/mp4">
    </video>
    <div class="video-caption">
      <h3>Pick and Place</h3>
    </div>
  </div>
  <div>
    <video autoplay loop muted playsinline>
      <source src="{{ site.baseurl }}/assets/videos/basic_skills/door.mp4" type="video/mp4">
    </video>
    <div class="video-caption">
      <h3>Opening and Closing Doors</h3>
    </div>
  </div>
  <div>
    <video autoplay loop muted playsinline>
      <source src="{{ site.baseurl }}/assets/videos/basic_skills/lever.mp4" type="video/mp4">
    </video>
    <div class="video-caption">
      <h3>Turning Levers</h3>
    </div>
  </div>
  <div>
    <video autoplay loop muted playsinline>
      <source src="{{ site.baseurl }}/assets/videos/basic_skills/knob.mp4" type="video/mp4">
    </video>
    <div class="video-caption">
      <h3>Twisting Knobs</h3>
    </div>
  </div>
  <div>
    <video autoplay loop muted playsinline>
      <source src="{{ site.baseurl }}/assets/videos/basic_skills/button.mp4" type="video/mp4">
    </video>
    <div class="video-caption">
      <h3>Pressing Buttons</h3>
    </div>
  </div>
</div>

**RoboCasa** focuses on a set of eight foundational skills that form the basis for the majority of household activities: (1) Pick and place, (2) Opening and closing doors, (3) Opening and closing drawers, (4) Twisting knobs, (5) Turning levers, (6) Pressing buttons, (7) Insertion, and (8) Navigation.

## Composite Tasks
<div class="video-slide">
  <div>
    <video autoplay loop muted playsinline>
      <source src="{{ site.baseurl }}/assets/videos/composite_tasks/steaming_veg.mp4" type="video/mp4">
    </video>
    <div class="video-caption">
      <h3>Steaming Vegetables</h3>
    </div>
  </div>
  <div>
    <video autoplay loop muted playsinline>
      <source src="{{ site.baseurl }}/assets/videos/composite_tasks/restock.mp4" type="video/mp4">
    </video>
    <div class="video-caption">
      <h3>Restocking Kitchen Supplies</h3>
    </div>
  </div>
  <div>
    <video autoplay loop muted playsinline>
      <source src="{{ site.baseurl }}/assets/videos/composite_tasks/brewing_coffee.mp4" type="video/mp4">
    </video>
    <div class="video-caption">
      <h3>Brewing Coffee</h3>
    </div>
  </div>
</div>

Composite tasks involve sequencing skills to solve semantically meaningful activities such as cooking and cleaning. The goal of creating these tasks is to capture diverse tasks that reflect the ecological statistics of real-world household activities, using the guidance of large language models (LLMs) to define our tasks. LLMs encapsulate diverse sources of human knowledge and can thus effectively communicate diverse ideas grounded in the real world.

# Team

## Core Developers

{% include members.html %}

## Project Advisors

{% include advisors.html %}

# Citation

```bibtex
@inproceedings{robocasa2024,
  title={RoboCasa: Large-Scale Simulation of Household Tasks for Generalist Robots},
  author={Soroush Nasiriany and Abhiram Maddukuri and Lance Zhang and Adeet Parikh and Aaron Lo and Abhishek Joshi and Ajay Mandlekar and Yuke Zhu},
  booktitle={arXiv preprint arXiv:...},
  year={2024}
}
```
