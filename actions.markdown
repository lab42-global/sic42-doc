---
layout: page
title: Actions
permalink: /actions/
---

Actions are what describe your agent behavior and you will let your Python script specify them based on the input the agent receives. Let the absolute position of the agent be given by \[x, y\]. We group the actions loosely by their type:

### Basic Survival Actions

- **move:** Move an agent from one cell to another.  

The value of the action is the location of the cell to move to. E.g.,

```json
"move": [-3, 4]
```

will make the agent move to \[x-3, y+4\].

- **eat:** Increase energy level of agent by eating an item that contains energy.

The value of the action is the relative location of the item to eat. E.g.,

```json
"eat": [-3, 4]
```

will make the agent eat the item at \[x-3, y+4\].

- **attack:** Attack another agent to lower its energy value.

The value of the action is the relative location of the agent to be attacked. E.g.,

```json
"attack": [-3, 4]
```

will make the agent attack the agent located at \[x-3, y+4\].

- **reproduce:** Reproduce by creating a copy of an agent.

The value of the action is the relative location of the cell the offspring should be placed on. E.g.,

```json
"reproduce": [-3, 4]
```

will create an offspring of the agent at the location \[x-3, y+4\].

### Item Interaction Actions

- **pickup:** Pick up an item and put it into storage.

The value of the action is the relative position of the item to be picked up. E.g.,

```json
"pickup": [2, 2]
```

will make the agent pick up the item located at \[x+2, y+2\].

- **putdown:** Put down an item in storage.

The value of the action is the relative position of the cell the item from storage should be placed on. E.g.,

```json
"putdown": [-1, 4]
```

will make the agent put down the item in storage at the position \[x-1, y+4\].

- **itemmerge:** Merge item in inventory with other item.

The value of the action is the relative position of the location of the item which should be merged with the one in storage. E.g.,

```json
"itemmerge": [-2, 3]
```

will make the agent merge the item in storage with the one at \[x-2, y+3\]. The newly created item will be stored in the inventory.

### Information Handling Actions

- **infostorage:**: Write information into item.

The value of the action consists of the relative position of the item into which the information should be written and the text to be written into the item. E.g.,

```json
"infostorage": [[-2, 3], "merge me with A!"]
```

will write the string "merge me with A!" into the item located at \[x-2, y+3\].

- **memory:**: Store information into agents memory.

The value of the action is a dictionary that should be stored to the internal memory of the agent. E.g.,

```json
"memory": {"coolitems": "A+B", "i": 1}
```

will write the dictionary with content {"coolitems": "A+B", "i": 1} into the internal memory which can be accessed again for example in the next simulation step.

- **broadcast:**: Broadcast information to other agents.

The value of the action is a list of pairs \[relative position, message\], where the relative positions refer to the agents to which the content of the message should be communicated. E.g.,

```json
"broadcast":  [[[1, 0], ”above you”], [[-1, 0], ”below you”]]
```

will broadcast the message "above you" to the agent at \[x+1, y\] and the message "below you" to the agent at \[x-1, y\].

### Environmental Interaction Actions

- **pheromone:** Place pheromones on the cells.

The value of the action consists of the relative position of the cell the pheromone should be placed on and a number describing the type of pheromone. E.g.,

```json
"pheromone":  [[0, 0], 1]  
```

will place the pheromone 1 on the cell \[0, 0\].

### Enhancement Actions

- **powerup:** Consume powerup from item.

The value of the action is the relative position of the item from which the powerup should be consumed. E.g.,

```json
"powerup":  [1, -1] 
```

will let the agent consume the powerup in the item located at \[x+1, y-1\] (if there is one). Note that powerups are temporary and cannot be passed to offsprings via reproduction.

- **upgrade:** Consume upgrade from item.

The value of the action is the relative position of the item from which the upgrade should be consumed. E.g.,

```json
"upgrade":  [1, 1] 
```

will let the agent consume the powerup in the item located at \[x+1, y+1\] (if there is one). Note that upgrades are permanent and will be passed to offsprings via reproduction.

## Combining actions

If allowed in a game, all of the above actions can be combined for a single step. Say the number of available activity points is 2, then the simulation will execute the first 2 requested actions in the list returned by the agent. E.g., if the number of activity points is 2 and the list returned by the agent is the following:

```json
[[”pickup”, [0, -1]], [”step”, [2, 0]], [”putdown”, [0, -1]]]
```

The agent will pickup the item located at \[x, y-1\] and then move to the cell at \[x+2, 0\], provided there is an item at the location and the storage is not full and the cell at \[x+2, 0\] is empty. The "putdown" action will never be executed as the number of activity points is too low even if "pickup" and/or "step" fails.
