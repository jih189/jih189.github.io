---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
redirect_from:
  - /projects
---

HOME ROBOT PROJECT(Current)
======
Intelligent home robots: An intelligent home robot is exemplified by a robot that can “reset” your home or put away the groceries or go fetch the coffee from the kitchen. The robot is required to operate in a semi-structured setting, understand the semantic organization of the home and manipulate objects to solve its tasks. A key part of the project is natural interaction with human users and other agents in the environment.

I am responsible for the task planning part, which includes the task decomposition, task sequencing, and task scheduling. I am also responsible for the motion planning part, which includes the motion planning for the robot arm and the mobile base.

<img src='/images/homerobot1.png' width="500">

ASSEMBLY PROJECT(2018-2019)
======
The [Assembly project](https://scholar.google.com/citations?view_op=view_citation&hl=en&user=qsb8eYwAAAAJ&citation_for_view=qsb8eYwAAAAJ:u-x6o8ySG0sC) entails designing an end-to-end pipeline for assembling products from individual parts using two UR5 robotic arms. This pipeline encompasses three primary stages: perception, planning, and execution.

In this endeavor, my responsibilities span several crucial areas:

<b>System Integration</b>: Setup the whole system on the ROS platform. This system contains multiple components such as object/pose detection, assembly task and motion planning, and force control.

<b>Perception</b>: I pioneered our [deep learning method](https://arxiv.org/pdf/2011.00372.pdf) to accurately estimate the 6D pose of objects.

Here is demonstration how our system detect the object which is not in predicted location.
<center>
    <video width="640" height="480" controls>
        <source src="/videos/object_detection.mp4" type="video/mp4">
    </video>
</center>

<b>Planning</b>: I crafted a constraint-based planning approach to methodically generate the assembly sequence.

<b>Control</b>: I employed impedance control, ensuring the robotic arms assemble the parts with precision.

Following is the video of how our system handle the possible noise during manipulation. Using the task and motion planning with impedance control, our system can detect the manipulation failure and select the proper action to recover it.

<div id="videoal">
<table>
    <tr>
        <td>
        <center>
            <video width="320" height="240" controls>
                <source src="/videos/assembly1.mp4" type="video/mp4">
            </video>
        </center>
       </td>
       <td>
         <center>
           <video width="320" height="240" controls>
              <source src="/videos/assembly2.mp4" type="video/mp4">
           </video>
          </center>
       </td>
       <td>
         <center>
           <video width="320" height="240" controls>
              <source src="/videos/assembly3.mp4" type="video/mp4">
           </video>
          </center>
       </td>
    </tr>
</table>
</div>

<!-- <center>
<video width="640" height="480" controls>
  <source src="/videos/assembly1.mp4" type="video/mp4">
</video>
</center> -->
<!-- 
<img src='/images/assembly1.png' width="500">
<img src='/images/assembly2.png' width="500">
<img src='/images/assembly3.png' width="500"> -->