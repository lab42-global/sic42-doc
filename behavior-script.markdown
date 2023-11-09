---
layout: page
title: Behavior Script
permalink: /behavior-script/
---

You successfully installed the sic42 package using our [quick start](/quick-start/) guide and now want to implement your own behavior? Just follow these main steps:

1. [Create a new Python file and add it to your behavior scripts folder](#1-create-a-new-python-file-and-add-it-to-your-behavior-scripts-folder)
2. [Add a `main()` function and code a behavior](#2-add-a-main-function-and-code-a-behavior)
3. [Test and improve it!](#3-test-and-improve-it)
4. [Submit it and participate in the cup!](#4-submit-it-and-participate-in-the-cup)

## 1. Create a new Python file and add it to your behavior scripts folder

Create a new Python file as the base for your new agent behavior script. If you participate in the cup, name it using your team name, e.g., 'lab42.py'. Then place it in the folder where you keep your behavior scripts, let's call it 'competitors'.

## 2. Add a `main()` function and code a behavior

Everything your file needs is a working `main()` function. It will be imported when running the simulation. At each time step of the simulation it can read the 'agent_input.json' and can create an 'agent_output.json' file containing the
actions your agents may take based on the content of the input file. For more information on the simulation and the input/output files head over to our [simulation](/simulation/) section.

A minimal example of an agent that just moves right independent of the input would be:

```python
import json
import sys

def from_json(path='agent_input.json'):
    with open(path, 'r') as fp:
        json_obj = json.load(fp)
    return (
        json_obj['self_view'],
        np.array(json_obj['relative_indices']),
        np.array(json_obj['entities']),
        np.array(json_obj['pheromones'], dtype='object')
    )

def main():
    """ simply move right """
    self_view, indices, entities, pheromones = from_json() # read input from json even though we don't need it
    # Initialize output list containing the desired actions
    desired_actions = []
    # Move Right
    desired_actions.append(('step', [0, 1]))
    # Write output to json
    with open('agent_output.json', 'w') as fp:
        json.dump(desired_actions, fp)
```

Note that we defined a function called `from_json` to read the agents input. However, we are not using its output in this simple behavior we just create a list called `desired_actions` and append an action with key `step` and value `[0, 1]` to it.
This will make the agent move right (if possible) as we write the `desired_actions` list to the `agent_output.json` file. This file will be read by the simulation handler and checked if the action can be executed as well as if your
agent still has enough activity points. You can read more about what an agent can do in our [actions](/actions/) section.

If you wish to use Python packages you can use most of the commonly available. For the beta phase we will run the tournaments using the official Kaggle docker-python image which means that you can use whatever is
[installed on Kaggle](https://www.kaggle.com/code/nagadomi/list-of-installed-packages). If you feel like there is something important missing reach out to us.

## 3. Test and improve it

To test your newly created agent behavior you have to apply the steps explained in the [quick start](/quick-start/) section and make sure you correctly specified the path to the behavior script files. Then you can run the tournament and
see how your agents behave. For reference, if you placed the file in the 'competitors' folder of your working directory and have the 'deathmatch_config.json' in the working directory just execute the following:

```python
from sic42 import sic
tournament = sic.Tournament(
        config_path='deathmatch_config.json',
        competitors_path='competitors'
    )
    tournament.run_tournament()
```

If you set the interactive flag to 'true' (cf., the subsection [2.3 Interactive mode](/quick-start/#23-interactive-mode) in the quick-start guide), you can follow the agent behavior in real time. Else you can check it afterwards by looking
at the content of the 'deathmatch_results' folder.

You can use the available plots and the visualization to make the behavior more interesting and improve the agent's behavior. You can see how your agents stand up against others by joining the Swarm Intelligence Cup.

## 4. Submit it and participate in the cup

You have an interesting behavior to show, or just want to see how your agents stack up against others? Take part in our 'Swarm Intelligence Cup'. Head over to our [Lab42 landing page](https://lab42.global/sic/) and then

1. [Sign Up](https://lab42.global/sic/registration/)
2. [Submit your Code](https://lab42.global/sic/submission/)
3. Get to the top of the [Leaderboard](https://lab42.global/sic/leaderboard/)