---
layout: page
title: Quick Start
permalink: /quick-start/
---

There are several possible ways you can use the SIC simulation with increasing complexity, respectively number of additional software needed:

1. [Use the Colab template](#1-use-the-colab-template) [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lab42-global/sic42-template/blob/main/sic-template.ipynb) (free Google account required).
2. [Use a local Python installation](#2-use-a-local-python-installation) and install the package via pip. (We recommend using a virtual environment).
3. [Use a local Python installation with the source code.](#3-use-a-local-python-installation-with-the-source-code) Get it from our [GitHub repository](https://github.com/lab42-global/sic42).
4. [Use the development container](#4-use-the-development-container) together with VSCode found on our [GitHub repository](https://github.com/lab42-global/sic42) to be as close as possible to our evaluation environment.

## 1. Use the Colab Template

For everyone that wants to start as quickly as possible or does not have a lot of experience with coding we recommend using our Colab template:
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lab42-global/sic42-template/blob/main/sic-template.ipynb)

It should be self-explanatory and we suggest you go through it step by step by evaluating the code cells in the Notebook yourself. You can do that by clicking the play button on the left side of the code block or by pressing `Shift+Enter` when a code cell is selected.

You can find the source and everything that comes with it on our [GitHub repository](https://github.com/lab42-global/sic42-template) for the template. We will update it continuously and are happy to incorporate your feedback on how we can improve it.

Note that there is one limitation due to how Colab works: For now there is no interactive live view of the simulation. For that you need to run the code locally.

## 2. Use a local Python installation.

We recommend that you use a virtual environment manager such as [Anaconda](https://docs.anaconda.com/free/anaconda/install/index.html) to manage the dependencies. Installing the sic42 package is then as simple as running

```bash
pip install sic42
```

### 2.1 Test your installation

Once you've done that you can test if everything worked by executing the following code:

```python
from sic42 import sic
sic.Tournament().run_tournament()
```

This will run a tournament using the swarm death match configuration together with two very simple sample behaviors provided in the package. After the simulation runs finished you should find a folder called 'deathmatch_results' in the directory in which you executed the code.
It should have the following structure:

```text
deathmatch_results
├── leaderboard.csv
├── tournament_log.json
├── round_1
│   ├── game_1_Reproducer_Eater
│   │   ├── results.csv
│   │   ├── times.csv
│   │   ├── set_1
│   │   │   ├── visualization.mp4
│   │   │   ├── logs
│   │   │   │   ├── Eater_actions.json
│   │   │   │   ├── Eater_errors.json
│   │   │   │   ├── Reproducer_actions.json
│   │   │   │   ├── Reproducer_errors.json
│   │   │   ├── plots
│   │   │   │   ├── action_counts
│   │   │   │   │   ├── attack_count.png
│   │   │   │   │   ├── eat_count.png
│   │   │   │   │   ├── ...
│   │   │   │   ├── average_agent_attribute_values
│   │   │   │   │   ├── average_energy_level.png
│   │   │   │   │   ├── ...
│   │   ├── set_2
│   │   │   ├── ...
│   ├── game_2_X_Y
│   │   ├── ...
│   ├── ...
├── round_2
│   ├── ...
```

It may be that the visualization videos are not being generated on your system because you lack a working ffmpeg installation. If you use Anaconda you can install it using the following command in your shell:

```bash
conda install -c conda-forge --yes ffmpeg
```

### 2.2 Use your own behavior scripts and config file

Once you've installed and tested the package successfully you can start adding your own behavior scripts and if you like also change the configuration script. For that you should create a folder into which you want to put
the behavior scripts (and only those), e.g. called "competitors" in your working directory. You can also create another folder for the configuration script or keep it in the parent directory. Once you've done that add at
least two behavior scripts and a configuration file. If you wish to use the examples that come with the package it's easiest to find them on our [GitHub repository](https://github.com/lab42-global/sic42-template) for the Colab template. Make sure that you also copy the 'math_utils.py'
file you will find there into your parent directory as the two sample behavior scripts rely on that. You can also find the behaviors and the helper file in the [examples](/examples/) section.

You can then test if everything works by specifying the paths to the behavior scripts and the configuration file when running the tournament:

```python
from sic42 import sic
tournament = sic.Tournament(
        config_path='deathmatch_config.json',
        competitors_path='competitors'
    )
tournament.run_tournament()
```

In this case we put the behavior scripts in the 'competitors' folder and specified the config file to use ('deathmatch_config.json') which is in our parent directory. Note that when running a tournament it will go through
all Python files that are in the competitors folder, check if they have a main function and if so import them using the name of the Python file. For example if you wish to let two agents with the same behavior compete
against each other you can just duplicate the behavior script and give it a different name (e.g. 'Eater_1.py' and 'Eater_2.py').

### 2.3 Interactive mode

The sic42 package comes with an interactive mode that let's you see in real time what your agents do and some basic stats about the swarms. To enable it change the entry in the config file (e.g., 'deathmatch_config.json') called '"interactive"' (at the end of '"visualization"') from 'false' to 'true'.
Running the tournament will then open a pygame window with a real time view on the simulation. You can pause it by pressing the space bar on your keyboard and hover with your mouse over an agent to get some basic information about it.

## 3. Use a local Python installation with the source code

In case you wish to look at the underlying code of the sic42 package you can find it on our [GitHub repository](https://github.com/lab42-global/sic42). Everything is published under an Apache 2.0 license and we are happy to receive your feedback
on how we can improve the code for the future.

## 4. Use the development container

We would like to leave you as much freedom as possible when it comes to the behavior scripts in terms of allowed packages that are allowed for the competition. For now we will rely on the publicly available Kaggle [docker-python](https://github.com/Kaggle/docker-python) image,
which contains many of the most used packages. You can test if your behavior script will run smoothly through our evaluation by using the .devcontainer folder found on our [GitHub repository](https://github.com/lab42-global/sic42). 

There are several things you need if you follow the suggested path:

1. A working [Docker](https://docs.docker.com/get-docker/) and [Visual Studio Code](https://code.visualstudio.com/download) installation.
2. The Dev Containers Extension for Visual Studio Code.
3. The .devcontainer folder in your working directory.

If you have everything ready and running it's as simple as using the shortcut `Ctrl+Shift+P` (Windows) or `Cmd+Shift+P` (macOS) in Visual Studio Code to run a command and then selecting `Dev Containers: Open Folder in Container...`. You can then select the folder in which
you have the '.devcontainer' folder as well as your behavior script folder and config file to create a Docker container and clone the folder into an isolated container volume. Note that the first time you do this the build process will take some time and you will have to 
download the large (>5GB) docker-python image. This will be noticeably faster afterwards if you don't change anything in your settings. You can now run the simulation inside the docker container using all the available packages. Furthermore, it's configured to also start
an ipython notebook server which you can access in your browser under `http://localhost:8080`.

If you feel that an important package is still missing that you'd like to use you can also reach out to us and we can consider adding it to the evaluation environment for the cup.