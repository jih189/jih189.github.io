---
layout: archive
title: "Isaac Lab Task"
permalink: /isaaclab_task
---

Ok. In this tutorial, I will provide more detail about build your own task. First of all, let's see what are in a task directory.

- **`[your task]/`**:
    - **`config/`** # Agent directory
    - **`mdp/`** # MDP setting
    - `__init__.py`
    - `[your task]_env_cfg.py` # Environment file

Now, let me explain each of them in detail except __init__.py which is just a empty file.

<H3>Configuration File</H3>
Basically, this is the environment configuration file, and we only consider the manager-based environment in this tutorial. The following are two tutorial about env and RL env from Nvidia Team. You do not have to go through them, because they did not explain them based on the template. Thus, I will try to explain in my way.

- [Manager-Based Environment](https://isaac-sim.github.io/IsaacLab/source/tutorials/03_envs/create_manager_base_env.html)
- [Manager-Based RL Environment](https://isaac-sim.github.io/IsaacLab/source/tutorials/03_envs/create_manager_rl_env.html)

To define a RL environment configuration file, you must have following thing:

- Create a class named [your task]EnvCfg inherit class [ManagerBasedRLEnvCfg](https://isaac-sim.github.io/IsaacLab/source/api/lab/omni.isaac.lab.envs.html#omni.isaac.lab.envs.ManagerBasedRLEnvCfg).
    
    First, we need to initialize the following attributes:
    - `scene`: Scene settings.
    - `observations`: Observation space settings.
    - `actions`: Action space settings.
    - `events`: Event settings.
    - `is_finite_horizon`: Whether the task is treated as a finite or infinite horizon problem for the agent, default is False. Initialized it in __post_init__.
    - `episode_length_s`: Duration of an epsode (in seconds). Initialized in __post_init__.
    - `decimation`: Number of control action updates at sim dt per policy dt. Initialized in __post_init__. 
    - `rewards`: Reward settings.
    - `terminations`: Termination settings.
    - `curriculum`: Curriculum settings.
    - `commands`: Commmand Settings.

    To initialize them, it requires us to create the classes for them. For more detail, please check the tutorial in [Manager-Based Environment](https://isaac-sim.github.io/IsaacLab/source/tutorials/03_envs/create_manager_base_env.html) and [Manager-Based RL Environment](https://isaac-sim.github.io/IsaacLab/source/tutorials/03_envs/create_manager_rl_env.html).