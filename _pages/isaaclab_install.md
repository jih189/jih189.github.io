---
layout: archive
title: "Isaac Lab Install"
permalink: /isaaclab_install
---

This is the tutorial to install Nvidia isaac sim with isaac lab. Here we suggest using docker to install and launch everything. In the following tutorial, we will show each steps:

## 1. Install Nvidia Driver and Docker

Follow the tutorial in this [link](https://docs.omniverse.nvidia.com/isaacsim/latest/installation/install_container.html).

 ### <span style="color: #FF69B4;">Possible Issues with solution:</span>

 #### 1. During installation, you may meet the error to disable nouveau. 
 
 Please follow this [link](https://docs.nvidia.com/ai-enterprise/deployment-guide-vmware/0.1.0/nouveau.html#ubuntu).

 #### 2. During installation, you may meet error “ERROR: An error occurred while performing the step: "Building kernel modules". See /var/log/nvidia-installer.log for details.”

 This means your GCC version is too low. You may need to upgrade it to 12. Here is the [link](https://www.dedicatedcore.com/blog/install-gcc-compiler-ubuntu/).

## 2. Download docker container for Isaac-Sim

Then you need to download the image for building container. There is the [link](https://isaac-sim.github.io/IsaacLab/source/deployment/docker.html). By the way, please save your API KEY some where.

 ### <span style="color: #FF69B4;">Possible Issues with solution:</span>

 #### 1. You need to generate your NGC API Key. But the tutorial may be wrong.

You need to login to your nvidia account. Instead of clicking Organization > Service Keys, you should click setup. The GenerateAPIKey is there.

## 3. Build the container
In the IsaacLab, they provide script to build env for IsaacLab on the IsaacSim.
#### 1. Clone the Isaac Lab from https://github.com/isaac-sim/IsaacLab
#### 2. Go to the directory IsaacLab/docker, you can run following code
```
./container.sh start isaaclab
```
This command will pull and update, then build the container.
```
./container.sh enter isaaclab
```
This command will let you enter the container. You can open multiple terminals and run this command to enter the container.
```
./container.sh stop isaaclab
```
This command will stop the container and remove it. If you directly, close the container, then you have to use __docker rm__ to rm the container.

For more information about using IsaacLab in docker, please check [this](https://isaac-sim.github.io/IsaacLab/source/deployment/docker.html).