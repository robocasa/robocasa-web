---
layout: main
title: RoboCasa
subtitle: 
project_tagline: "Large-Scale Simulation of Household Tasks for Generalist Robots"
videoId: 
---

![pull figure]({{ 'assets/images/gallery_logo.png' | absolute_url }})

**RoboCasa** is a large-scale simulation framework for training generalist agents in household environments. It features realistic and diverse scenes with a focus on kitchen environments which we enhance we the help of AI generation tools. In addition we provide over 1000 3D assets across 83 object categories and dozens of intractable appliances. These assets support diverse behaviors and we propose a set of 75 tasks, including tasks representing complex activities that we generated with the guidance of large language models. We include a set of high-quality demonstrations for each task and explore the use of robot data generation tools to significantly expand the scope of our dataset at little additional cost.

# Video Overview

<figure class="figure"><div class="figure__main">
<video autoplay loop muted playsinline controls class="postimagefullwidth">
  <source src="{{ site.baseurl }}/assets/robomimic_video.mp4" type="video/mp4">
</video>
</div></figure>

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
