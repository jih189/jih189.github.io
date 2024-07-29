---
layout: archive
title: "RL Project Tutorial"
permalink: /isaaclab_project
---

To build your own project, Nvidia Team has provide a pre-configured and customizable [template](https://github.com/isaac-sim/IsaacLabExtensionTemplate.git) for creating projects in an isolated environment.

Due to the IsaacLab/source is mounted to your local machine, so I suggest to place your template into IsaacLab/source.

In the container, you can enter the template by
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code>cd /workspace/isaaclab/source/IsaacLabExtensionTemplate</code>
</pre>

Throughout the repository, the name ext_template only serves as an example and it provides a script to rename all the references to it automatically:
<pre style="font-size: 15px;color: white;background-color: #000000; padding: 10px;">
<code><span style="color: yellow;"># Rename all occurrences of ext_template (in files/directories) to your_fancy_extension_name</span>
python scripts/rename_template.py your_fancy_extension_name</code>
</pre>

<H2>Start Your Project</H2>
In IsaacLab, a "task" encompasses everything involved in the training process. Specifically, it includes both the [environment](https://isaac-sim.github.io/IsaacLab/source/features/environments.html) and the robot(agent). To start your own RL project, you'll need to configure both the environment and the robot within this task.

In this section, I'll provide a brief overview of how these two elements are organized within the project template and explain the underlying principles. For more detailed information, please refer to the additional tutorials that will be provided.

<H3>Environment Configuration</H3>
Environment defines the actual task and assets(ground, light, and objects except the robot) in the scene. Usually, the environment configuration file will be in the root of task directory, and named as "[task name]_env_cfg.py". In thie environment configuration you need to provide scene settings, basic settings, and MDP settings. If you want to modify the MDP setting here, you should create a MDP directory in the root to overwrite MDP terms.

<H3>Robot Configuration</H3>
The robot configuration defines the interface how the robot to complete the task, and here does not contain the actual detail of the robot such as mesh or material. This should be maintained in the `cofig` directory for each robot. In each robot, you need to do following steps:

- Provide the parameter setting for each RL library. Saved it in the agents directory.
- Overwrite the environment configuration by including the robot. For example, if the task of environment is to grasp the box with gripper(which we did not define the actual gripper), then here we need to define this gripper to be the gripper of the robot you want to use.
- Registrate the task in `__init__.py`

<H2> Template Organization Explanation </H2>

In this section, I will give a purpose explanation about important directories and files in the template.

### `IsaacLabExtensionTemplate/`
- **`exts/`**: Your extensions to the IsaacLab.
    - <span style="color: blue;">**`ext_template/`**</span>: The actual template of your extension. You can rename it by `python scripts/rename_template.py extension_name`.
        - **`config/`**:
            - `extension.toml`: Configuration file of your extension. It dictate how the extension is integrated into IsaacSim, ROS, and etc. <span style="color: blue;"> You should modify your extension name here</span>.
        - **`docs/`**: Save your template doc here.
        - **`ext_template/`**: The source of your template. It will be renamed by the script as well.
            - **`tasks/`**: This direcotry contains all tasks of your project.
                - **`locomotion/`**: Tasks related to locomotion such as legged robot.
                    - **`velocity/`**: Directory for the velocity task, where the robot's movement is controlled based on velocity.
                        - **`config/`**: Contains all definition the robot for RL.
                            - **`anymal_d/`**: definition of anymal_d
                                - **`agents/`**: Contains all configuration files( or API file) for specific RL library to understand your task.
                                    - `__init__.py`: If you have configuration file for rsl_rl here, then you should import it here. If you do not have rsl_rl here, then you do not need this file.
                                    - `rsl_rl_cfg.py`: The configuration file for rsl_rl to understand your task.
                                - `__init__.py`: <span style="color: green;">Registration file.</span> You registrate your task with your robot here. This is important file. Without this, training and playing will not recognize it.
                                - `flat_env_cfg.py`: The configuration file of your env with robot.
                                - `rough_env_cfg.py`: The configuration file of your env with robot.
                            - `__init__.py`: Empty here.
                        - **`mdp/`**: You can overwrite the mdp here.
                            - `__init__.py`: Include your overwriten in the mdp.
                            - `curriculumns.py`: Defines the way how you increase the task's difficulty as the agent training progess.
                            - `rewards.py`: Defines the reward terms for the agent.
                        - `__init__.py`: Empty here.
                        - `velocity_env_cfg.py`: The configuration file for the task environment.
                    - `__init__.py`: Marks other directories here as modules.
                - `__init__.py`: I do not know what is this for, so <span style="color: red;">Do not modify</span>.
            - **`assets/`**: <span style="color: green;">This is usually optional</span> because you can use those default assets provided by IsaacLab. This directory contains all assets of your project.
            - `__init__.py`: This file is used to mark the directory as a Python package. To import modules from this directory, you can use `from .YourDirectory import *`, replacing YourDirectory with the actual directory name. For example, if you have the a directory to save assets, then you should import it here.
        - `setup.py`: Python script used for install the necessary python packages for your project. <span style="color: red;">Do not modify</span>.

- **`scripts/`**: Where you place the workflow scripts for your RL library. There are some workflow examples in **`source/standalone/workflow`**.
    - **`rsl_rl/`**: The workflow script of rsl_rl as example.
        - `cli_args.py`: Python script that typically handles command-line arguments for configuring various aspects of your RL library.
        - `play.py`: The script to play your trained model.
        - `train.py`: The script to train with your RL library.