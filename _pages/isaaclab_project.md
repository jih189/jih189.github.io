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


### `src/`
- **`main/`**: Contains the main application code and resources.
  - **`java/`**: Source code for the main application.
    - `Main.java`: The entry point of the application.
  - **`resources/`**: Configuration files and other resources needed by the application.
    - `application.properties`: Application configuration settings.
  - **`webapp/`**: Web application resources.
    - `index.html`: The main HTML file for the web interface.

- **`test/`**: Contains test code and resources.
  - **`java/`**: Source code for unit and integration tests.
    - `MainTest.java`: Test cases for the application.
  - **`resources/`**: Resources needed for testing.
    - `test-config.properties`: Test configuration settings.

- **`assets/`**: Static assets like images and styles.
  - **`images/`**: Contains image files used in the project.
  - **`styles/`**: Contains CSS files for styling.
    - `main.css`: Main stylesheet.

### `build/`
- **`classes/`**: Compiled classes and artifacts.
- **`libs/`**: External libraries and dependencies.
- **`reports/`**: Build and test reports.

### `docs/`
- **`setup-guide.md`**: Instructions for setting up the project.
- **`api-docs/`**: API documentation and related resources.

### Root Files
- **`.gitignore`**: Specifies files and directories to be ignored by Git.
- **`build.gradle`**: Build configuration file for Gradle.
- **`README.md`**: Project overview, installation, and usage instructions.
- **`LICENSE`**: Licensing information for the project.