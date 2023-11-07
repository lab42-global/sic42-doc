---
layout: page
title: Simulation
permalink: /simulation/
---

The simulation environment is created based on the [configuration](/configuration/) file. In there it is specified how the environment is populated with agents and items and what there properties are. We will call the combination of agents and environments at a given time "board".

The simulation is divided into simulation steps in which every agent gets its turn to execute actions.

## Simulation Step

For every simulation there is a maximum number of time steps where each of these steps consists of the following:

1. A random order of agents is chosen. This is the order according to which agents can execute their actions within the time step, i.e., the simulation is asynchronous.
2. For each agent that is alive:
    i. The agent behavior module, corresponding to the swarm the agent belongs to, receives the information about the current board "agent input" and has to return the requested actions "agent output".
    ii. It is checked if the requested actions are possible and if so the board is updated accordingly.
    iii. The time it takes the behavior script to generate the requested actions is measured and deducted from the totally available of the corresponding swarm.
3. The items are updated. E.g., the energy level of items may grow or items may be spawned.
4. Pheromones loose intensity according to their decay function.

## Agent Input and Output

As described before in every simulation step the behavior module receives an "agent_input" and has to generate a corresponding "agent_output" containing the actions the agent should execute.

### Agent Input

At each time step each agent receives the state of the current board (c.f., step 2.i. above). The agent input contains the following:

- **self_view:** Information about the current state of the agent. E.g.,

```json
{'inventory_info': None, 'swarm_name': 'A', 'energy_level': 81, 'inbox': [], 'n_pheromone_symbols': 1, 'memory': {'prev_di': 0, 'prev_dj': -1, 'home_i': -1, 'home_j': 1, 'mode': 0}}
```

- **indices:** A list of relative \[x, y\] coordinates specifying the view-field of the agent. E.g., if the view-field is 1

```json
[[-1, -1], [-1, 0], [-1, 1], [0, -1], [0, 0], [0, 1], [1, -1], [1, 0], [1, 1]]  
```

- **entities:** A list describing what entity is on which of the above indices. The entries can be an item view, an agent view or "none" (no entity). Each item only exposes certain information about itself which is visible here. The agent view only consists of the name of the swarm it belongs to. E.g., if there is an agent of swarm 'A' at the relative position \[-1, -1\] and an item that has certain properties (e.g., energy 0) at the relative position \[1, 1\] we would have:

```json
[{'type': 'swarm', 'name': 'B'}, {'type': None, 'name': 'empty'}, {'type': None, 'name': 'empty'}, {'type': None, 'name': 'empty'}, {'type': None, 'name': 'empty'}, {'type': None, 'name': 'empty'}, {'type': None, 'name': 'empty'}, {'type': None, 'name': 'empty'}, {'type': 'item', 'name': 'obstacle', 'energy': 0, 'pickupable': True, 'edible': False, 'infostorage': False, 'weight': 1}]  
```

- **pheromones:** A list describing if a pheromone is present on one of the above indices. E.g., if the pheromone '1'is present at the position \[-1, -1\] and '1' and '2' at the position \[1, 1\] we have

```json
[[1], [], [], [], [], [], [], [], [1, 2]]  
```

### Agent Output

The agent output is a list of actions the agent wants to execute and should be returned by the agent behavior module. For more details on the possible actions refer to the corresponding [page](/actions/). Important is that each agent only has a limited number of activity points at each time step which limits the number of possible actions the agent can do in one time step.  E.g., if the number of activity points is 2 and the list returned by the agent is the following:

```json
[[”pickup”, [0, -1]], [”step”, [2, 0]], [”putdown”, [0, -1]]]
```

The agent will pickup the item located at \[x, y-1\] and then move to the cell at \[x+2, 0\], provided there is an item at the location and the storage is not full and the cell at \[x+2, 0\] is empty. The "putdown" action will never be executed as the number of activity points is too low even if "pickup" and/or "step" fails.
