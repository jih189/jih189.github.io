---
layout: archive
title: "Isaac Lab Task"
permalink: /isaaclab_task
---

Ok. In this tutorial, I will provide more detail about build your own task. First of all, let's see what are in a task directory.

- **`[your task]/`**:
    - **`config/`** # <a href="#agentdir">Agent directory</a>
    - **`mdp/`** # MDP setting
    - `__init__.py`
    - `[your task]_env_cfg.py` # <a href="#envfile">Environment File</a>

Now, let me explain each of them in detail except __init__.py which is just a empty file.

<H2 id="envfile">Environment File</H2>
Basically, this is the environment configuration file, and we only consider the manager-based environment in this tutorial. The following are two tutorial about env and RL env from Nvidia Team. You do not have to go through them, because they did not explain them based on the template. Thus, I will try to explain in my way.

- [Manager-Based Environment](https://isaac-sim.github.io/IsaacLab/source/tutorials/03_envs/create_manager_base_env.html)
- [Manager-Based RL Environment](https://isaac-sim.github.io/IsaacLab/source/tutorials/03_envs/create_manager_rl_env.html)

To define a RL environment configuration file, you must have following thing:

- Create a class named [your task]EnvCfg inherit class [ManagerBasedRLEnvCfg](https://isaac-sim.github.io/IsaacLab/source/api/lab/omni.isaac.lab.envs.html#omni.isaac.lab.envs.ManagerBasedRLEnvCfg).
    
    First, we need to initialize the following attributes:
    - **`scene`**: Scene settings.
    - **`observations`**: Observation space settings.
    - **`actions`**: Action space settings.
    - **`events`**: Event settings.
    - **`is_finite_horizon`**: Whether the task is treated as a finite or infinite horizon problem for the agent, default is False. Initialized it in `__post_init__`.
    - **`episode_length_s`**: Duration of an epsode (in seconds). Initialized in `__post_init__`.
    - **`decimation`**: Number of control action updates at sim dt per policy dt. Initialized in `__post_init__`. 
    - **`**rewards`**: Reward settings.
    - **`terminations`**: Termination settings.
    - **`curriculum`**: Curriculum settings.
    - **`commands`**: Commmand Settings.

    To initialize them, it requires us to create the classes for them. For more detail, please check the tutorial in [Manager-Based Environment](https://isaac-sim.github.io/IsaacLab/source/tutorials/03_envs/create_manager_base_env.html) and [Manager-Based RL Environment](https://isaac-sim.github.io/IsaacLab/source/tutorials/03_envs/create_manager_rl_env.html).

<H2 id="agentdir">Agent Dirctory</H2>
The agent directory is where you build the task configurations for different robots for your environment. That is, for single one task, you can have different robot to learn it. Thus, you need to specify how each robot to handle the task. For each robot, you need to have following modules:

- **`[your robot]/`**:
    - **`agents/`** # set the parameter for each RL library.
    - `__init__.py` # used to register the task.
    - `[your robot]_[your task]_env_cfg.py` # you can use whatever name you want here.

Now, I will give more detail of each modules.

<H3>agents/</H3>

Here is the directory where you set the model parameter for each RL library. You can check the example from [here](https://github.com/isaac-sim/IsaacLabExtensionTemplate/tree/dcebe2325631917123912ee0220288f412ac256a/exts/ext_template/ext_template/tasks/locomotion/velocity/config/anymal_d/agents).

<H3>[your robot]_[your task]_env_cfg.py</H3>

This file defines how the robot should be set for the task. For example, set the scene robot, set the random range, and some other parameters of the task. Furthermore, the configuration of play should be set here as well. Therefore, the following two classes should be here:

- [your robot][your task]EnvCfg: [your task]EnvCfg
- [your robot][your task]EnvCfg_PLAY: [your robot][your task]EnvCfg

<H3>__init__.py</H3>

Here is where we register the task. More [detail](https://isaac-sim.github.io/IsaacLab/source/tutorials/03_envs/register_rl_env_gym.html) is provided.

Here is the template of register file.
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>import gymnasium as gym

from . import agents, [your robot]_[your task]_env_cfg

gym.register(
    id="Isaac-[your task]-[your robot]-v[version number]",
    entry_point="omni.isaac.lab.envs:ManagerBasedRLEnv",
    disable_env_checker=True,
    kwargs={
        "env_cfg_entry_point": [your robot]_[your task]_env_cfg.[your robot][your task]EnvCfg,
        "[RL library]_cfg_entry_point": [link to RL library configuration file],
        ...
    },
)

gym.register(
    id="Isaac-[your task]-[your robot]-Play-v[version number]",
    entry_point="omni.isaac.lab.envs:ManagerBasedRLEnv",
    disable_env_checker=True,
    kwargs={
        "env_cfg_entry_point": [your robot]_[your task]_env_cfg.[your robot][your task]EnvCfg_PLAY,
        "[RL library]_cfg_entry_point": [link to RL library configuration file],
        ...
    },
)</code>
</pre>