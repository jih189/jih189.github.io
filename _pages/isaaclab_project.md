---
layout: archive
title: "RL Project Tutorial"
permalink: /isaaclab_project
---

To build your own project, Nvidia Team has provide a pre-configured and customizable [template](https://github.com/isaac-sim/IsaacLabExtensionTemplate.git) for creating projects in an isolated environment.

Due to the IsaacLab/source is mounted to your local machine, so I suggest to place your template into IsaacLab/source.

In the container, you can enter the template by
```
cd /workspace/isaaclab/source/IsaacLabExtensionTemplate
```

Throughout the repository, the name ext_template only serves as an example and it provides a script to rename all the references to it automatically:
```
# Rename all occurrences of ext_template (in files/directories) to your_fancy_extension_name
python scripts/rename_template.py your_fancy_extension_name
```

<H2> Template Explanation </H2>

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