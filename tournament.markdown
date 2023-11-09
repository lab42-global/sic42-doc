---
layout: page
title: Tournament
permalink: /tournament/
---

To evaluate the contributions of the participants against each other we will hold Swiss-style tournaments to ensure a fair ranking and be resource efficient. During the tournament opponents play games against each other. Depending on the environment any number of opponents within a game is possible, i.e., there could be only one opponent in the environment but also two, three or more.

## Tournament style

A tournament is divided into two stages

1. [Rounds](#1-rounds)
2. [Games](#2-games)

### 1. Rounds

In each round the opponents are matched based on their current ranking. That is, if there are two opponents per game, the first plays the second, the third the fourth and so on. The number of rounds can be specified explicitly but defaults to log2(#opponents). In the first round the opponents are matched randomly and if there is an odd number of participants opponents are picked randomly to not play during a round. In that case the score they are assigned will be:

- First round: Average score of all participants.
- Else: Average of their own scores of the previous round(s).

### 2. Games

Each game consists of sets, where the same opponents may play several times against each other. The configuration of the environment may change from set to set to achieve a more meaningful score. E.g., the number of agents or items in the environment may change from set to set.

## Ranking

The final ranking is determined by the sum of the scores achieved in all rounds. The score per round is calculated as the average score achieved in all sets.
