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
<!-- 
### `IsaacLabExtensionTemplate/`
- **`main/`**: Contains the main application code and resources.
  - **`java/`**: Source code for the main application.
    - `Main.java`: The entry point of the application.
  - **`resources/`**: Configuration files and other resources needed by the application.
    - `application.properties`: Application configuration settings.
  - **`webapp/`**: Web application resources.
    - `index.html`: The main HTML file for the web interface. -->


### `IsaacLabExtensionTemplate/`
- **`exts/`**: Your extensions to the IsaacLab.
    - <span style="color: green;">**`ext_template/`**</span>: The actual template of your extension.

- **`scripts/`**: Where you place the workflow scripts for your RL library. There are some workflow examples in **`source/standalone/workflow`**.
    - **`rsl_rl/`**: The workflow script of rsl_rl as example.
        - `cli_args.py`: Python script that typically handles command-line arguments for configuring various aspects of your RL library.
        - `play.py`: The script to play your trained model.
        - `train.py`: The script to train with your RL library.