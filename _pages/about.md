---
permalink: /
title: "About me"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

I am a robotics system engineer in a robotics start up and got my Ph.D. degree from the Department of Computer Science and Engineering at UC San Diego. I have the privilege of conducting my research in the [Cognitive Robotics Lab](https://www.cogrob.org/), under the esteemed guidance of [Prof. Henrik I. Christensen](https://www.hichristensen.com/). 

Previous Research Topics
======
My primary research during my Phd career revolves around task and motion planning for mobile robots, with a particular emphasis on home service robots. For more detail, I am maintainly focus on the following topics to build the mobile robot system better.

### 1. Foliation Planning (Constrained Motion Planning in Foliated Manifolds)
    
My research focuses on leveraging foliated manifold structures to model manipulation tasks with greater precision and to design efficient motion planning algorithms for identifying feasible solutions. This approach enhances task representation compared to traditional multi-modal motion planning methods, offering improved precision. Furthermore, unlike reinforcement learning (RL), our algorithms provide guarantees of completeness and generalization, making them robust for a wide range of applications. I am now planning to incorporate parallelism using GPU acceleration to further enhance the efficiency of the planning process. By leveraging the computational power of GPUs, foliated planning can provide even more effciency in terms of planning time to acheive industry need.

### 2. Rearrangement Planning for Mobile Robot

My research focuses on generating efficient plans for indoor object rearrangement problems based on a specified desired arrangement. Indoor rearrangement is a complex, NP-hard problem due to object dependencies and the limited space available for buffer allocation. This complexity is further exacerbated when the robot must frequently relocate itself for each manipulation because it cannot access all objects from a single position. Unlike most existing approaches that rely on learning-based methods to estimate the desired arrangement, my work emphasizes planning efficiency for given start and goal configurations, while also providing guarantees of completeness.

Publications
======

<div style="display: flex; align-items: flex-start; gap: 16px;">
  <img src="/images/gpu_motion_planning.png" alt="GPU Motion Planning" style="width:180px; height:auto; border-radius:6px; box-shadow: 0 2px 6px rgba(0,0,0,0.07);">
  <div>
    Jiaming Hu, Jiawei Wang, Henrik I. Christensen (2025). <b>cpRRTC: GPU-Parallel RRT-Connect for Constrained Motion Planning</b>. Workshop on Motion Planning and Control via Parallelization, Robotics: Science and Systems (RSS).
  </div>
</div>

Jiaming Hu, Jan Szczekulski, Sudhansh Peddabomma, Henrik I. Christensen(2025). <b>Planning for Tabletop Object Rearrangement</b>. IEEE International Conference on Robotics and Automation (ICRA).

Jiaming Hu<sup>*</sup>, Shrutheesh Raman Iyer<sup>*</sup>, Jiawei Wang and Henrik I. Christensen (2024). <b>Motion Planning in Foliated Manifolds using Repetition Roadmap</b>. Robotics: Science and Systems (RSS).

Shrutheesh Raman Iyer, Anwesan Pal, Jiaming Hu, Akanimoh Adeleye, Aditya Aggarwal and Henrik I. Christensen (2023). <b>Household navigation and manipulation for everyday object rearrangement tasks</b>. International Conference on Robotic Computing (IRC).

Jiaming Hu , Zhao Tang , Henrik I. Christensen (2023). <b>Multi-modal planning on re-grasping for stable manipulation</b>. International Conference on Intelligent Robots and Systems (IROS).

Jiaming Hu<sup>*</sup>, Akanimoh Adeleye<sup>*</sup>, Henrik I. Christensen (2022). <b>Place-And-Pick-Based Re-Grasping Using Unstable Placement</b>. The International Symposium on Robotics Research (ISRR).

Jiaming Hu , Henrik I. Christensen (2022). <b>Rotational Slippage Minimization in Object Manipulation</b>. International Conference on Automation Science and Engineering (CASE).

Akanimoh Adeleye , Jiaming Hu , Henrik I. Christensen (2022). <b>Putting away the Groceries with Precise Semantic Placements</b>. International Conference on Automation Science and Engineering (CASE).

Priyam Parashar , Aayush Naik , Jiaming Hu , Henrik I. Christensen (2021). <b>A Hierarchical Model to Enable Plan Reuse and Repair in Assembly Domains</b>. International Conference on Automation Science and Engineering (CASE).

<sup>*</sup> denotes equal contribution

Robotics Related Skills
======
OMPL, ROS1/2, IsaacLab/Sim, and CoppeliaSim, Moveit! 1 and 2, Curobo, Nav 2, Cuda Programming