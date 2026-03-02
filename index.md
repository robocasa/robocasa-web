---
layout: main
subtitle: 
project_tagline: "Large-Scale Simulation Framework for Training and Benchmarking Generalist Robots"
image: assets/images/Robocasa_web_logo.svg
videoId: 
---

<div id="robocasa365-release"></div>

<figure class="figure rc-release-figure">
  <div class="figure__main">
    <video controls autoplay loop muted playsinline preload="metadata" class="rc-release-video">
      <source src="{{ site.baseurl }}/assets/videos/release.mp4" type="video/mp4">
    </video>
  </div>
</figure>

**RoboCasa** is a large-scale simulation framework for training generally capable robots to perform everyday tasks. It features realistic and diverse human-centered environments with a focus on kitchen scenes. We create these environments with the aid of generative AI tools, such as large language models (LLMs) and text-to-image/3D generative models. Together with the simulated tasks, we offer a dataset of high-quality human demonstrations and leverage automated trajectory generation techniques to significantly expand the amount of training data with little additional cost.

We're excited to announce [**RoboCasa365**]({{ site.baseurl }}/assets/robocasa365_iclr26.pdf), the latest release built on the RoboCasa platform: 365 everyday tasks across 2,500 diverse kitchen environments, with 600+ hours of human demonstration data and 1,600+ hours of synthetically generated demonstrations. RoboCasa365 is designed for systematic benchmarking across key settings, including multi-task learning, foundation model training, and lifelong learning. It supports popular policy learning models, such as Diffusion Policy, π₀, and GR00T.

<hr>

## Realistic and Diverse Scenes

<figure class="figure rc-scene-collage">
  <div class="figure__main">
    <video autoplay loop muted playsinline class="postimagefullwidth">
      <source src="{{ site.baseurl }}/assets/videos/scene_collage.mp4" type="video/mp4">
    </video>
  </div>
</figure>

To capture the complexity and diversity of real-world environments, we consult numerous architecture and home design magazines and compile a collection of kitchen layouts and styles reflecting the vast diversity of kitchens in homes around the world. We model these kitchens according to standard size and spatial specifications and fit them with a large repository of interactable furniture and appliances spanning cabinets, stoves, sinks, microwaves, and more.

**RoboCasa365** significantly expands this foundation: from the original 100 scenes we scale to **2,500** unique kitchen environments for large-scale training. We introduce 50 new layouts based on real-world homes, paired with 50 additional styles that vary fixtures, appliances, and textures.

## Cross-Embodiment Support

The simulator supports mobile manipulators of diverse form factors, such as single-arm mobile platforms, humanoid robots, and quadruped robots with arms.

<div class="video-grid-2x2">
  {% for video in site.static_files %}
    {% if video.path contains '/assets/videos/robot_grid/' %}
      <div class="video-item">
        <video class="lazy" autoplay loop muted playsinline>
          <source data-src="{{ site.baseurl }}{{ video.path }}" type="video/mp4">
        </video>
      </div>
    {% endif %}
  {% endfor %}
</div>

## Interactable Furniture and Appliances

<div class="video-grid-2x2">
  {% for video in site.static_files %}
    {% if video.path contains '/assets/videos/appliance_grid/' %}
      <div class="video-item">
        <video class="lazy" autoplay loop muted playsinline>
          <source data-src="{{ site.baseurl }}{{ video.path }}" type="video/mp4">
        </video>
      </div>
    {% endif %}
  {% endfor %}
</div>

Each kitchen scene is equipped with a selection of interactable furniture and appliances. Several types of interactable objects are articulated; for example, a robot can open and close doors on microwaves and twist knobs on stoves. Other types of interactable objects can undergo state changes; for example, when a knob on the stove is turned, the corresponding burner turns on.

<br>

<hr>

## Augmenting Scene Diversity with Text-to-Image Models

<figure class="figure">
  <div class="figure__main">
    <video autoplay loop muted playsinline class="postimagefullwidth">
      <source src="{{ site.baseurl }}/assets/videos/ai_textures.mp4" type="video/mp4">
    </video>
  </div>
</figure>

Each scene can be customized by replacing textures from a large selection of high-quality AI-generated textures created using the popular text-to-image models from <a href="https://docs.midjourney.com/docs/model-versions">MidJourney</a>. We provide 100 textures for walls, 100 for the floor, 100 for counters, and 100 for cabinet panels, respectively. These textures can be used as a form of realistic domain randomization to increase the visual diversity of our training datasets substantially.

## Creating Diverse Object Assets with Text-to-3D Models

We curate a repository of 3,200+ objects across more than 150 categories, spanning a variety of fruits, vegetables, packaged foods, and receptacles. They are sourced from <a href="https://objaverse.allenai.org/">Objaverse</a> 1.0, <a href="https://www.lightwheel.ai/">LightWheel AI</a>, and the remaining are AI-generated from <a href="https://lumalabs.ai/">Luma AI</a>.


<figure class="figure">
  <div class="figure__main">
    <video autoplay loop muted playsinline class="postimagefullwidth">
      <source src="{{ site.baseurl }}/assets/videos/objects.mp4" type="video/mp4">
    </video>
  </div>
</figure>


## Training Foundational Robot Skills

We focus on ten foundational skills as the basic building blocks to scaffold long-horizon manipulation behaviors for the majority of household activities: (1) Pick and place, (2) Opening and closing doors, (3) Opening and closing drawers, (4) Twisting knobs, (5) Turning levers, (6) Pressing buttons, (7) Insertion, (8) Navigation, (9) Sliding Racks, and (10) Closing/Opening Lids. RoboCasa365 includes 65 atomic tasks for systematically training and benchmarking these skills.


<div class="video-slide-wrapper">
  <div class="slide-button-left"></div>
  <div class="slide-button-right"></div>
  <div class="video-slide">
    <div>
      <video class="lazy" autoplay loop muted playsinline>
        <source data-src="{{ site.baseurl }}/assets/videos/basic_skills/pnp.mp4" type="video/mp4">
      </video>
      <div class="video-caption">
        <h3>Pick and Place</h3>
      </div>
    </div>
    <div>
      <video class="lazy" autoplay loop muted playsinline>
        <source data-src="{{ site.baseurl }}/assets/videos/basic_skills/door.mp4" type="video/mp4">
      </video>
      <div class="video-caption">
        <h3>Opening and Closing Doors</h3>
      </div>
    </div>
    <div>
      <video class="lazy" autoplay loop muted playsinline>
        <source data-src="{{ site.baseurl }}/assets/videos/basic_skills/lever.mp4" type="video/mp4">
      </video>
      <div class="video-caption">
        <h3>Turning Levers</h3>
      </div>
    </div>
    <div>
      <video class="lazy" autoplay loop muted playsinline>
        <source data-src="{{ site.baseurl }}/assets/videos/basic_skills/knob.mp4" type="video/mp4">
      </video>
      <div class="video-caption">
        <h3>Twisting Knobs</h3>
      </div>
    </div>
    <div>
      <video class="lazy" autoplay loop muted playsinline>
        <source data-src="{{ site.baseurl }}/assets/videos/basic_skills/button.mp4" type="video/mp4">
      </video>
      <div class="video-caption">
        <h3>Pressing Buttons</h3>
      </div>
    </div>
  </div>
</div>


## Generating Composite Tasks with LLM Guidance

Composite tasks involve sequencing skills to solve semantically meaningful activities, from restocking kitchen supplies to brewing coffee. Our goal in creating these tasks is to capture realistic and diverse tasks that reflect the ecological statistics of real-world household activities in the human-centered world. We use the guidance of large language models (LLMs), <a href="https://openai.com/index/gpt-4-research/">GPT-4</a> particularly, to define our tasks, as they encapsulate a vast amount of common sense and world knowledge of the human world and can thus effectively provide task candidates based on the environments and the robot's skills.

<div class="video-slide-wrapper">
  <div class="slide-button-left"></div>
  <div class="slide-button-right"></div>
  <div class="video-slide">
    <div>
      <video class="lazy" autoplay loop muted playsinline>
        <source data-src="{{ site.baseurl }}/assets/videos/composite_tasks/steaming_veg.mp4" type="video/mp4">
      </video>
      <div class="video-caption">
        <h3>Steaming Vegetables</h3>
      </div>
    </div>
    <div>
      <video class="lazy" autoplay loop muted playsinline>
        <source data-src="{{ site.baseurl }}/assets/videos/composite_tasks/restock.mp4" type="video/mp4">
      </video>
      <div class="video-caption">
        <h3>Restocking Kitchen Supplies</h3>
      </div>
    </div>
    <div>
      <video class="lazy" autoplay loop muted playsinline>
        <source data-src="{{ site.baseurl }}/assets/videos/composite_tasks/brewing_coffee.mp4" type="video/mp4">
      </video>
      <div class="video-caption">
        <h3>Brewing Coffee</h3>
      </div>
    </div>
  </div>
  <br>
</div>

<br>
<hr>

# Team

{% include members.html %}

# Citation

[**RoboCasa365**]({{ site.baseurl }}/assets/robocasa365_iclr26.pdf) (paper):

```bibtex
@inproceedings{robocasa365,
  title={RoboCasa365: A Large-Scale Simulation Framework for Training and Benchmarking Generalist Robots},
  author={Soroush Nasiriany and Sepehr Nasiriany and Abhiram Maddukuri and Yuke Zhu},
  booktitle={International Conference on Learning Representations (ICLR)},
  year={2026}
}
```

**RoboCasa (Original Release):**

```bibtex
@inproceedings{robocasa2024,
  title={RoboCasa: Large-Scale Simulation of Everyday Tasks for Generalist Robots},
  author={Soroush Nasiriany and Abhiram Maddukuri and Lance Zhang and Adeet Parikh and Aaron Lo and Abhishek Joshi and Ajay Mandlekar and Yuke Zhu},
  booktitle={Robotics: Science and Systems (RSS)},
  year={2024}
}
```

<script>
  var video_slides = document.getElementsByClassName("video-slide-wrapper");
  var buttons = [null, null];
  var disabled = [false, false];
  var first = true;
  for (let slide_wrapper of video_slides) {
    let slide = slide_wrapper.getElementsByClassName("video-slide").item(0);
    buttons[0] = slide_wrapper.getElementsByClassName("slide-button-left").item(0);
    buttons[1] = slide_wrapper.getElementsByClassName("slide-button-right").item(0);
    for (let i = 0; i < 2; i++) {
      buttons[i].addEventListener("click", function (e) {
        if (disabled[i] === true) return;
        var width = slide.children[0].offsetWidth;

        // Fix for mobile - not sure why but it allows an extra scroll to the right without this
        if (i == 1 && slide.scrollLeft > width * (slide.children.length - 1)) return;

        disabled[i] = true;

        slide.scrollBy({
          left: width * (i === 0 ? -1 : 1),
          behavior: 'smooth'
        });

        let position = null
        const checkIfScrollIsStatic = setInterval(() => {
          if (position === slide.scrollLeft) {
            clearInterval(checkIfScrollIsStatic)
            disabled[i] = false;
          }
          position = slide.scrollLeft
        }, 20);
      });
    }
  }

  document.addEventListener("DOMContentLoaded", function() {
    var lazyVideos = [].slice.call(document.querySelectorAll("video.lazy"));

    if ("IntersectionObserver" in window) {
      var lazyVideoObserver = new IntersectionObserver(function(entries, observer) {
        entries.forEach(function(video) {
          if (video.isIntersecting) {
            for (var source in video.target.children) {
              var videoSource = video.target.children[source];
              if (typeof videoSource.tagName === "string" && videoSource.tagName === "SOURCE") {
                videoSource.src = videoSource.dataset.src;
              }
            }

            video.target.load();
            video.target.classList.remove("lazy");
            lazyVideoObserver.unobserve(video.target);
          }
        });
      });

      lazyVideos.forEach(function(lazyVideo) {
        lazyVideoObserver.observe(lazyVideo);
      });
    }
  });
</script>