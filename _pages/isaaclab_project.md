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