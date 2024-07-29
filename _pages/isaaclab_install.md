---
layout: archive
title: "Isaac Lab Install"
permalink: /isaaclab_install
---

This is the tutorial to install Nvidia isaac sim with isaac lab. Here we suggest using docker to install and launch everything. In the following tutorial, we will show each steps:

<H2> 1. Install Nvidia Driver and Docker </H2>

Follow the tutorial in this [link](https://docs.omniverse.nvidia.com/isaacsim/latest/installation/install_container.html).

 <H3> <span style="color: #FF69B4;">Possible Issues with solution:</span> </H3>

<H4> 1. During installation, you may meet the error to disable nouveau.  </H4>
 
 Please follow this [link](https://docs.nvidia.com/ai-enterprise/deployment-guide-vmware/0.1.0/nouveau.html#ubuntu).

<H4> 2. During installation, you may meet error “ERROR: An error occurred while performing the step: "Building kernel modules". See /var/log/nvidia-installer.log for details.”</H4>

 This means your GCC version is too low. You may need to upgrade it to 12. Here is the [link](https://www.dedicatedcore.com/blog/install-gcc-compiler-ubuntu/).

<H2> 2. Download docker container for Isaac-Sim </H2>

Then you need to download the image for building container. There is the [link](https://isaac-sim.github.io/IsaacLab/source/deployment/docker.html). By the way, please save your API KEY some where.

<H3> <span style="color: #FF69B4;">Possible Issues with solution:</span> </H3>

 <H4> 1. You need to generate your NGC API Key. But the tutorial may be wrong. </H4>

You need to login to your nvidia account. Instead of clicking Organization > Service Keys, you should click setup. The GenerateAPIKey is there.

<H2> 3. Build the container </H2>
In the IsaacLab, they provide script to build env for IsaacLab on the IsaacSim.
<H4> 1. Clone the Isaac Lab from https://github.com/isaac-sim/IsaacLab </H4>
<H4> 2. Go to the directory IsaacLab/docker, you can run following code</H4>

<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>./container.sh start isaaclab</code>
</pre>

This command will pull and update, then build the container.
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>./container.sh enter isaaclab</code>
</pre>
This command will let you enter the container. You can open multiple terminals and run this command to enter the container.
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>./container.sh stop isaaclab</code>
</pre>

This command will stop the container and remove it. If you directly, close the container, then you have to use __docker rm__ to rm the container.

For more information about using IsaacLab in docker, please check [this](https://isaac-sim.github.io/IsaacLab/source/deployment/docker.html).