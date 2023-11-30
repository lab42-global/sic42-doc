---
layout: page
title: FAQ
permalink: /faq/
---

We will collect some frequently asked questions here, both concerning the sic42 package as well as the swarm intelligence cup.

## sic42

**Q: Why should sic42 help us on the path to more intelligent systems?**

A: Intelligence is about being able to adapt to changing conditions, learn new skills, explore and create theories about the environment. In nature everything is built from seemingly unintelligent
and simple building blocks -- think cells in our body or a single ant -- that once combined are able to solve complex tasks in a robust manner. The sic42 package is designed to allow for the
implementation of a large variety of tasks. Additionally, the possibility to combine objects to create new more powerful ones, necessitates agents to explore and communicate to be successful. The goal is
to develop sic42 into a framework that is as simple as possible yet allows to study and iterate on as many aspects of intelligence as possible.

**Q: How does the item merging currently work?**

A: Item merging is a key component of sic42 as it is a way for agents to exploit their environment. Every time two types of objects that have not yet been combined are brought together a new type
is created with properties that are on average more favorable to the agents than the properties of the uncombined items. Once two types of objects have been combined for the first time,
every time those are brought together the combined item will have the same properties for the rest of the simulation. This allows agents to learn about the best items to combine to find powerful
powerups, upgrades or a better resource to be more successful.

**Q: What is the difference between "powerups" and "upgrades"?**

A: Think of "powerups" affecting the agent that consumes it only temporarily while "upgrades" are permanent and can also be passed to offsprings. Consuming a "powerup" is like drinking a coffee in
the morning while consuming an upgrade would be like improving its own genetics or learning a skill that is passed to offsprings.

**Q: What are features are planned for upcoming versions?**

A: There are many things we would still like to implement and we encourage everyone to contribute ideas and/or code. Things we would like to add include:

- More sample disciplines in addition to swarm-deathmatch and an easier way to play with them.
- More complex environment with cells that have different properties. Like cells that suck energy, allow for faster movement or protect against adversaries.
- And many more...

**Q: What is copied when using the "reproduce" action?**

A: When you use the "reproduce" action an identical copy of the parent agent is produced with the following differences in the child:

- Empty storage
- Empty memory

Note that there is usually an energy penalty to both the parent and child when reproducing (energy is halfed) but this can be configured. If you wish to pass some information to the child you
can use the "broadcast" action in conjunction with the "reproduce" action.

## Swarm Intelligence Cup

**Q: What are the configuration files used for the competition matches?**

A: For the swarm-deathmatch matches we will keep the configuration file close to the one provided with the package with a few exceptions:

- Your agents are allowed to use all actions.

**Q: Why are you not specifying the configuration files in more detail?**

A: Our goal is to find rules that govern single agents that are "simple" yet allow the swarm to show a robust behavior to changing conditions. This is a key aspect to develop truly intelligent systems
and the swarms we observe in nature show this treat.

**Q: Swarm-deathmatch can easily be solved by reinforcement-learning, why do you propose it as a step towards more intelligent systems?**

A: It might be true that a single discipline is an easy task for current reinforcement-learning techniques but keep in mind that this is only the first of several disciplines the swarms should compete
in in the future. We chose swarm-deathmatch as the first discipline as it is easy to grasp quickly and allows us to test the package and see which things still need to change for the full cup.
