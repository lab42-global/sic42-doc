---
layout: page
title: Configuration
permalink: /configuration/
---

The configuration of a tournament can be specified in a JSON file. In the following we will not go through all the options and keep it high level, as in general you do not need to change the configuration file if your only intent is to take part in the SIC. However, if you wish to know all the details and make configuration files yourself please consult the technical documentation.

There are five categories into which we group the configuration, tournament, simulation, environment, agents, and visualization.

## Tournament

The mode of the tournament is explained in more detail on another [page](/tournament/). The important configurations are:

- **Goal Function:** The goal function specifies how the scores are calculated. A successful swarm maximizes it.
- **Tournament details:** It can be specified how many rounds a tournament consists of, how many sets and how many swarms there are per game.

## Simulation

Aside from the number of time steps the simulation runs and when it will stop the important thing is the time constraint per swarm:

- **Time constraints:** The available total runtime per swarm per set in seconds. It is roughly calculated as 

```text
available runtime = (time multiplier)*(nr of agents)*(total nr of time steps)
```

## Environment

- **Size:** The size of the environment may vary and can be specified as well as the symbol that should be taken for the background.
- **Swarms:** The number of agents per swarm that are initially spawned can be specified. Furthermore, it is possible to restrict the spawning of the swarm's agent to certain subregions, e.g., a disc or quadrant of the whole environment.
- **Items:** Each type of item that is spawned initially and possibly during the simulation can be specified according to the following concepts:
  - **Amount:** Number of items, where they are spawned, if they "regrow" and how they are displayed.
  - **Energy:** If they can be consumed, amount of energy they contain and if the energy increases after each simulation step.
  - **Carryable:** How much they weigh and if they can be picked up at all.
  - **Information:** If they can store information.
  - **Powerup:** What kind of powerup the item contains, how strong it is, how long it is effective and how likely it is that the item spawns with it.
  - **Upgrade:** What kind of upgrade the item contains, how strong it is and how likely it is that the item spawns with it.

## Agents

The parameter describing the initial configuration of a single agent can be set. They include:

- **View field:** Distance up to which an agent can see as well as if the view field is a circle or square.
- **Energy:** The initial energy level the agent has as well as how much it is reduced in each time step.
- **General Actions:** The number of activity points an agent has per step as well as the allowed actions. For each action it can be set how many activity points it requires, how much energy, up to which distance it can be applied and what the minimal amount of energy is the agent needs to execute it.
- **Carrying Actions:** How much the energy cost is increased when carrying an item in storage and what the maximum weight is such that the item can be carried.
- **Combat Actions:** The strength of an attack as well as the strength of the defense capabilities.
- **Information Actions:** The maximum size of the memory as well as how far an agent can broadcast a message. Furthermore, there is a bound to how much can be stored in an item.
- **Pheromone Actions:** The number of different pheromones an agent can place as well as how intense they are when placed and how much they decay.
- **Upgrade/Powerup Actions:** The maximum number of upgrades and powerups an agent can apply.

## Visualization

It is possible to specify if a video should be generated, if you want to be in interactive mode and observe the swarms live using pygame, if you wish to save plots and logs.
