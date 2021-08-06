---
layout: study
permalink: /study/
---

# What Matters in Learning from Offline Human Demonstrations for Robot Manipulation

The full paper can be found [here](https://arise-initiative.github.io/robomimic-web/assets/paper.pdf).

## Video Summary

<figure class="figure"><div class="figure__main">
<iframe width="560" height="315" src="https://www.youtube.com/embed/qg_IVo4rB8k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div></figure>

## Overview

- In [this paper](https://arise-initiative.github.io/robomimic-web/assets/paper.pdf), we conduct an extensive study of six offline learning algorithms for robot manipulation on five simulated and three real-world multi-stage manipulation tasks of varying complexity, and with datasets of varying quality. 
- Our study analyzes the most critical challenges when learning from offline human data for manipulation.
- Based on the study, we derive a series of lessons to guide future work, and also highlight opportunities in learning from human datasets, such as the ability to learn proficient policies on challenging, multi-stage tasks and easily scale to natural, real-world manipulation scenarios.
- **We have open-sourced our datasets and all algorithm implementations to facilitate future research and fair comparisons in learning from human demonstration data.**


<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/overview.png" class="postimagetwothird"/></p>
<figcaption>
In this study, we investigate several challenges of offline learning from human datasets and extract lessons to guide future work.
</figcaption>
</div></figure>

## Why is learning from human-labeled datasets difficult?

We explore five challenges in learning from human-labeled datasets.

<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/challenges.png" class="postimagetwothird"/></p>
</div></figure>

- **(C1) Unobserved Factors in Human Decision Making.** Humans are not perfect Markovian agents. In addition to what they currently see, their actions may be influenced by other external factors - such as the device they are using to control the robot and the history of the actions that they have provided.
<br><br>
- **(C2) Mixed Demonstration Quality.** Collecting data from multiple humans can result in mixed quality data, since some people might be better quality supervisors than others. 
<br><br>
- **(C3) Dependence on dataset size.** Policy learning is also sensitive to the state and action space coverage in the dataset.
<br><br>
- **(C4) Train Objective ≠ Eval Objective.** Unlike traditional supervised learning, where validation loss is a strong indicator of how good a model is, policies are usually trained with surrogate losses. This makes it hard to know which trained policy checkpoints are good without trying out each and every model directly on the robot -- a time consuming process.
<br><br>
- **(C5) Sensitivity to Agent Design Decisions.** Performance can be very sensitive to important agent design decisions, like the observation space and hyperparameters used for learning.

Next, we summarize the tasks (5 simulation and 3 real), datasets (3 different variants), algorithms (6 offline methods, including 3 imitation and 3 batch reinforcement), and observations spaces (2 main variants) that we explored in our study.

## Study Design: Tasks

<figure class="figure"><div class="figure__main">

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/task_lift.mp4" type="video/mp4">
  </video>
  <figcaption>
  Lift
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/task_can.mp4" type="video/mp4">
  </video>
  <figcaption>
  Can
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/task_tool_hang.mp4" type="video/mp4">
  </video>
  <figcaption>
  Tool Hang
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/task_square.mp4" type="video/mp4">
  </video>
  <figcaption>
  Square
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/task_lift_real.mp4" type="video/mp4">
  </video>
  <figcaption>
  Lift (Real)
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/task_can_real.mp4" type="video/mp4">
  </video>
  <figcaption>
  Can (Real)
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/task_tool_hang_real.mp4" type="video/mp4">
  </video>
  <figcaption>
  Tool Hang (Real)
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/task_transport.mp4" type="video/mp4">
  </video>
  <figcaption>
  Transport
  </figcaption>
</figure>

<figcaption>
We collect datasets across 6 operators of varying proficiency and evaluate offline policy learning methods on 8 challenging manipulation tasks that test a wide range of manipulation capabilities including pick-and-place, multi-arm coordination, and high-precision insertion and assembly.
</figcaption>

</div></figure>

## Study Design: Task Reset Distributions


<figure class="figure"><div class="figure__main">

<figure class="postfigurequarter">
  <img src="{{ site.baseurl }}/assets/videos/reset_lift.gif" class="postimage_unpadded"/>
  <figcaption>
  Lift
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <img src="{{ site.baseurl }}/assets/videos/reset_can.gif" class="postimage_unpadded"/>
  <figcaption>
  Can
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <img src="{{ site.baseurl }}/assets/videos/reset_tool_hang.gif" class="postimage_unpadded"/>
  <figcaption>
  Tool Hang
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <img src="{{ site.baseurl }}/assets/videos/reset_square.gif" class="postimage_unpadded"/>
  <figcaption>
  Square
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <img src="{{ site.baseurl }}/assets/videos/reset_lift_real.gif" class="postimage_unpadded"/>
  <figcaption>
  Lift (Real)
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <img src="{{ site.baseurl }}/assets/videos/reset_can_real.gif" class="postimage_unpadded"/>
  <figcaption>
  Can (Real)
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <img src="{{ site.baseurl }}/assets/videos/reset_tool_hang_real.gif" class="postimage_unpadded"/>
  <figcaption>
  Tool Hang (Real)
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <img src="{{ site.baseurl }}/assets/videos/reset_transport.gif" class="postimage_unpadded"/>
  <figcaption>
  Transport
  </figcaption>
</figure>

<figcaption>
We show the task reset distributions for each task. Initial states are sampled from this distribution at both train and evaluation time.
</figcaption>

</div></figure>


## Study Design: Datasets

<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/dataset_overview.png" class="postimagefourfifth"/></p>
<figcaption>
We collected 3 kinds of datasets in this study.
</figcaption>
</div></figure>

### Machine-Generated

These datasets consist of rollouts from a series of [SAC](https://arxiv.org/abs/1801.01290) agent checkpoints trained on Lift and Can. As a result, they contain random, suboptimal, and expert data. This kind of mixed quality data is common in offline RL works (e.g. [D4RL](https://github.com/rail-berkeley/d4rl/tree/master/d4rl), [RLUnplugged](https://github.com/deepmind/deepmind-research/tree/master/rl_unplugged)).


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_lift_rb_1.5k.mp4" type="video/mp4">
  </video>
  <figcaption>
  Lift (MG)
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_can_rb_3.9k.mp4" type="video/mp4">
  </video>
  <figcaption>
  Can (MG)
  </figcaption>
</figure>

<figcaption>
Lift and Can Machine-Generated datasets.
</figcaption>

</div></figure>


### Proficient-Human

These datasets consist of 200 demonstrations collected from a single proficient human operator using [RoboTurk](https://roboturk.stanford.edu/).

<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_lift_se.mp4" type="video/mp4">
  </video>
  <figcaption>
  Lift (PH)
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_can_se.mp4" type="video/mp4">
  </video>
  <figcaption>
  Can (PH)
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_square_se.mp4" type="video/mp4">
  </video>
  <figcaption>
  Square (PH)
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_transport_se_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Transport (PH)
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_tool_hang_se_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Tool Hang (PH)
  </figcaption>
</figure>

<figcaption>
Proficient-Human datasets generated by 1 proficient operator (with the exception of Transport, which had 2 proficient operators working together).
</figcaption>

</div></figure>


### Multi-Human

These datasets consist of 300 demonstrations collected from six human operators of varied proficiency using [RoboTurk](https://roboturk.stanford.edu/). Each operator falls into one of 3 groups - "Worse", "Okay", and "Better" -- each group contains two operators. Each operator collected 50 demonstrations per task. As a result, these datasets contain mixed quality human demonstration data. We show videos for a single operator from each group. 


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_lift_mh_worse_1.mp4" type="video/mp4">
  </video>
  <figcaption>
  Lift (MH) - Worse
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_lift_mh_okay_1.mp4" type="video/mp4">
  </video>
  <figcaption>
  Lift (MH) - Okay
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_lift_mh_better_1.mp4" type="video/mp4">
  </video>
  <figcaption>
  Lift (MH) - Better
  </figcaption>
</figure>

<figcaption>
Multi-Human Lift dataset. The videos show three operators - one that's "worse" (left), "okay" (middle) and "better" (right).
</figcaption>

</div></figure>


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_can_mh_worse_1_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Can (MH) - Worse
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_can_mh_okay_1_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Can (MH) - Okay
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_can_mh_better_1.mp4" type="video/mp4">
  </video>
  <figcaption>
  Can (MH) - Better
  </figcaption>
</figure>

<figcaption>
Multi-Human Can dataset. The videos show three operators - one that's "worse" (left), "okay" (middle) and "better" (right).
</figcaption>

</div></figure>


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_square_mh_worse_1_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Square (MH) - Worse
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_square_mh_okay_1_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Square (MH) - Okay
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_square_mh_better_1_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Square (MH) - Better
  </figcaption>
</figure>

<figcaption>
Multi-Human Square dataset. The videos show three operators - one that's "worse" (left), "okay" (middle) and "better" (right).
</figcaption>

</div></figure>


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_transport_mh_worse_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Transport (MH) - Worse-Worse
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_transport_mh_okay_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Transport (MH) - Okay-Okay
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_transport_mh_better_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Transport (MH) - Better-Better
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_transport_mh_worse_okay_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Transport (MH) - Worse-Okay
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_transport_mh_worse_better_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Transport (MH) - Worse-Better
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/playback_transport_mh_okay_better_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Transport (MH) - Okay-Better
  </figcaption>
</figure>

<figcaption>
Multi-Human Transport dataset. These were collected using pairs of operators with <a href="https://arxiv.org/abs/2012.06738">Multi-Arm RoboTurk</a> (each one controlled 1 robot arm). We collected 50 demonstrations per combination of the operator subgroups.
</figcaption>

</div></figure>


## Study Design: Algorithms

We evaluated 6 different offline learning algorithms in this study, including 3 imitation learning and 3 batch (offline) reinforcement learning algorithms.

<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/algo_overview.png" class="postimagefourfifth"/></p>
<figcaption>
We evaluated 6 different offline learning algorithms in this study, including 3 imitation learning and 3 batch (offline) reinforcement learning algorithms.
</figcaption>
</div></figure>

- **BC**: standard Behavioral Cloning, which is direct regression from observations to actions.
- **BC-RNN**: Behavioral Cloning with a policy network that's a Recurrent Neural Network (RNN), which allows modeling temporal correlations in decision-making.
- **HBC**: Hierarchical Behavioral Cloning, where a high-level subgoal planner is trained to predict future observations, and a low-level recurrent policy is conditioned on a future observation (subgoal) to predict action sequences (see [this paper](https://arxiv.org/abs/2003.06085) and [this paper](https://arxiv.org/abs/2012.06738) for more details).
- **BCQ**: Batch-Constrained Q-Learning, a batch reinforcement learning method proposed in [this paper](https://arxiv.org/abs/1812.02900).
- **CQL**: Conservative Q-Learning, a batch reinforcement learning method proposed in [this paper](https://arxiv.org/abs/2006.04779).
- **IRIS**: Implicit Reinforcement without Interaction, a batch reinforcement learning method proposed in [this paper](https://arxiv.org/abs/1911.05321).


## Study Design: Observation Spaces

We study two different observation spaces in this work -- low-dimensional observations and image observations.

<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/obs_overview.png" class="postimagefourfifth"/></p>
<figcaption>
We study two different observation spaces in this work.
</figcaption>
</div></figure>

### Image Observations

We provide examples of the image observations used in each task below.

<figure class="figure"><div class="figure__main">

<figure class="postfigurehalf">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/obs_can_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Most tasks have a front view and wrist view camera. The front view matches the view provided to the operator during data collection.
  </figcaption>
</figure>

<figure class="postfigurehalf">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/obs_tool_hang_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Tool Hang has a side view and wrist view camera. The side view matches the view provided to the operator during data collection.
  </figcaption>
</figure>

<figure class="postfigurefourfifths">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/obs_transport_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  Transport has a shoulder view and wrist view camera per arm. The shoulder view cameras match the views provided to each operator during data collection.
  </figcaption>
</figure>

</div></figure>


## Summary of Lessons Learned

In this section, we briefly highlight the lessons we learned from our study. See the paper for more thorough results and discussion.

### Lesson 1: History-Dependent Models are extremely effective.

<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/lesson_1.png" class="postimagefourfifth"/></p>
<figcaption>
Methods that make decisions based on history, such as BC-RNN and HBC, outperform other methods on human datasets.
</figcaption>
</div></figure>

### Lesson 2: Batch Offline RL struggles with suboptimal human data.

<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/lesson_2.png" class="postimagefourfifth"/></p>
<figcaption>
While Batch Offline RL methods are proficient at dealing with mixed quality machine-generated data, they struggle to deal with mixed quality human data.
</figcaption>
</div></figure>

<figure class="figure"><div class="figure__main">
<video autoplay loop muted playsinline controls class="postimagefourfifth">
  <source src="{{ site.baseurl }}/assets/videos/can_paired.mp4" type="video/mp4">
</video>
<figcaption>
To further evaluate methods in a simpler setting, we collected the Can Paired dataset, where every task instance has two demonstrations, one success and one failure. Even this simple setting, where each start state has exactly one positive and one negative demonstration, poses a problem.
</figcaption>
</div></figure>

### Lesson 3: Improving Offline Policy Selection is important.

<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/lesson_3.png" class="postimagefourfifth"/></p>
<figcaption>
The mismatch between train and evaluation objective causes problems for policy selection - unlike supervised learning, the best validation loss does not correspond to the best performing policy. We found that the best validation policy is 50 to 100% worse than the best performing policy. Thus, each policy checkpoint needs to be tried directly on the robot – this can be costly.
</figcaption>
</div></figure>

### Lesson 4: Observation Space and Hyperparameters play a large role in policy performance.

<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/lesson_4.png" class="postimagefourfifth"/></p>
<figcaption>
We found that observation space choice and hyperparameter selection is crucial for good performance. As an example, not including wrist camera observations can reduce performance by 10 to 45 percent
</figcaption>
</div></figure>

### Lesson 5: Using Human Data for manipulation is promising.

<figure class="figure"><div class="figure__main">
<img src="{{ site.baseurl }}/assets/images/lesson_5.png" class="postimagefourfifth"/>
<figcaption>
Studying how dataset size impacts performance made us realize that using human data holds much promise. For each task, the bar chart shows how performance changes going from 20% to 50% to 100% of the data. Simpler tasks like Lift and Can require just a fraction of our collected datasets to learn, while more complex tasks like Square and Transport benefit substantially from adding more human data, <b>suggesting that more complex tasks could be addressed by using large human datasets</b>.
</figcaption>
</div></figure>

### Lesson 6: Study Results transfer to Real World.

We collected 200 demonstrations per task, and trained a BC-RNN policy <b>using identical hyperparameters to simulation, with no hyperparameter tuning</b>. We see that in most cases, performance and insights on what works in simulation transfer well to the real world.

<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/raw_rollout_lift_eval_bright.mp4" type="video/mp4">
  </video>
  <figcaption>
  <b>Lift (Real).</b> 96.7% success rate. Nearly matches performance in simulation (100%).
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/can_eval_success_bright.mp4" type="video/mp4">
  </video>
  <figcaption>
  <b>Can (Real).</b> 73.3% success rate. Nearly matches performance in simulation (100%).
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/tool_hang_real_succ_bright.mp4" type="video/mp4">
  </video>
  <figcaption>
  <b>Tool Hang (Real).</b> 3.3% success rate. Far from simulation (67.3%) - the real task is harder.
  </figcaption>
</figure>

</div></figure>


Below, we present examples of policy failures on the Tool Hang task, which illustrate its difficulty, and the large room for improvement.


<figure class="figure"><div class="figure__main">

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/tool_hang_insert_miss_5x_bright.mp4" type="video/mp4">
  </video>
  <figcaption>
  Insertion Miss
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/tool_hang_fail_insert_5x_bright.mp4" type="video/mp4">
  </video>
  <figcaption>
  Failed Insertion
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/tool_hang_fail_tool_grasp_2_5x_bright.mp4" type="video/mp4">
  </video>
  <figcaption>
  Failed Tool Grasp
  </figcaption>
</figure>

<figure class="postfigurequarter">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/tool_hang_tool_drop_5x_bright.mp4" type="video/mp4">
  </video>
  <figcaption>
  Tool Drop
  </figcaption>
</figure>

<figcaption>
Failures which illustrate the difficulty of the Tool Hang task.
</figcaption>

</div></figure>

We also show that results from our observation space study hold true in the real world -- visuomotor policies benefit strongly from wrist observations and pixel shift randomization.


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/can_no_wrist_5x_bright.mp4" type="video/mp4">
  </video>
  <figcaption>
  <b>Can (no Wrist).</b> 43.3% success rate (compared to 73.3% with wrist).
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/can_no_rand_5x_bright.mp4" type="video/mp4">
  </video>
  <figcaption>
  <b>Can (no Rand).</b> 26.7% success rate (compared to 73.3% with randomization).
  </figcaption>
</figure>

<figcaption>
Without wrist observations (left) the success rate decreases from 73.3% to 43.3%. Without pixel shift randomization (right), the success rate decreases from 73.3% to 26.7%.
</figcaption>
</div></figure>


## Takeaways

<figure class="figure"><div class="figure__main">
<p><img src="{{ site.baseurl }}/assets/images/final_task_8.jpeg" class="postimagethird"/></p>
</div></figure>

1. Learning from large multi-human datasets can be challenging.<br><br>
2. Large multi-human datasets hold promise for endowing robots with dexterous manipulation capabilities.<br><br>
3. Studying this setting in simulation can enable reproducible evaluation and insights can transfer to real world.


## Additional Policy Evaluation Videos

In this section, we provide some additional policy rollout videos.


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_RNN_Transport_PH_im_epoch260_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC-RNN image agent on Proficient-Human Transport dataset. 72% success rate.
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_RNN_Transport_PH_im_epoch260_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC-RNN image agent on Multi-Human Transport dataset. 42% success rate.
  </figcaption>
</figure>

</div></figure>


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_RNN_Can_MH_im_epoch300_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC-RNN image agent on Multi-Human Can dataset. 96% success rate.
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_RNN_Square_MH_im_epoch280_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC-RNN image agent on Multi-Human Square dataset. 76.7% success rate.
  </figcaption>
</figure>

</div></figure>


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_Can_Worse_im_epoch460_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC image agent on MH-Worse Can dataset. 54.7% success rate.
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_RNN_Can_Worse_im_epoch140_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC-RNN image agent on MH-Worse Can dataset. 70% success rate.
  </figcaption>
</figure>

</div></figure>


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_Square_Worse_im_epoch400_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC image agent on MH-Worse Square dataset. 17.3% success rate.
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_RNN_Square_Worse_im_epoch180_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC-RNN image agent on MH-Worse Square dataset. 36.7% success rate.
  </figcaption>
</figure>

</div></figure>


<figure class="figure"><div class="figure__main">

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_Square_Worse_Better_im_epoch460_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC image agent on MH-Worse-Better Square dataset. 38.7% success rate.
  </figcaption>
</figure>

<figure class="postfigurethird">
  <video autoplay loop muted playsinline controls class="postimage_unpadded">
    <source src="{{ site.baseurl }}/assets/videos/rollouts/BC_RNN_Square_Worse_Better_im_epoch240_trim.mp4" type="video/mp4">
  </video>
  <figcaption>
  BC-RNN image agent on MH-Worse-Better Square dataset. 57.3% success rate.
  </figcaption>
</figure>

</div></figure>
