---
layout: page
title: Examples
permalink: /examples/
---

We will add some interesting sample behaviors at a later stage. If you think you have one and like to contribute it here reach out to us! For now here are the two sample behaviors that come with the [sic42 package missing link!]():

1. [Eater](#1-eater)
2. [Reproducer](#2-reproducer)

## 1. Eater

The following is the Python behavior script for the 'Eater' behavior found in the sic42 package. It's a very simple behavior meant for the swarm death match discipline. Maybe you can improve it?

```python
import json

from random import randint, choice
from typing import List, Dict, Tuple, Any, Union

import numpy as np

import sys
sys.path.append('...')
from math_utils import *

def veccast(vec):
    return list(map(int, vec))

def from_json(path='agent_input.json'):
    with open(path, 'r') as fp:
        json_obj = json.load(fp)
    return (
        json_obj['self_view'],
        np.array(json_obj['relative_indices']),
        np.array(json_obj['entities']),
        np.array(json_obj['pheromones'], dtype='object')
    )

def get_closest(
    srcpos: np.ndarray,
    pool: np.ndarray
) -> np.ndarray:
    """
    returns entry from pool with closest manhattan distance to srcpos

    srcpos: reference position
    pool: array of positions
    """
    deltas = np.abs(pool - srcpos)
    distances = np.sum(deltas, axis=1)
    idx = np.argmin(distances)
    return pool[idx]

def main():
    """ simply focuses on eating """
    self_view, indices, entities, pheromones = from_json()
    names = np.array([entity.get('name', None) for entity in entities])
    edibility = np.array([entity.get('edible', False) for entity in entities])
    empties = set(map(tuple, indices[names == 'empty'])) & set(DIRECS)
    desired_actions = []
    if sum(edibility) > 0:
        locs = indices[edibility]
        target_loc = get_closest(np.array([0, 0]), locs)
        direction = veccast(np.sign(target_loc))
        if within_chebyshev_distance(target_loc, (0, 0), 1):
            desired_actions.append(('eat', veccast(target_loc)))
        elif tuple(direction) in empties:
            desired_actions.append(('step', veccast(direction)))
    elif len(empties) > 0:
        direction = choice(list(empties))
        desired_actions.append(('step', veccast(direction)))
    with open('agent_output.json', 'w') as fp:
        json.dump(desired_actions, fp)
```

## 2. Reproducer

The following is the Python behavior script for the 'Eater' behavior found in the sic42 package. It's a very simple behavior meant for the swarm death match discipline. Maybe you can improve it?

```python
import json

from random import randint, choice
from typing import List, Dict, Tuple, Any, Union

import numpy as np

import sys
sys.path.append('...')
from math_utils import *

def veccast(vec):
    return list(map(int, vec))

def from_json(path='agent_input.json'):
    with open(path, 'r') as fp:
        json_obj = json.load(fp)
    return (
        json_obj['self_view'],
        np.array(json_obj['relative_indices']),
        np.array(json_obj['entities']),
        np.array(json_obj['pheromones'], dtype='object')
    )

def get_closest(
    srcpos: np.ndarray,
    pool: np.ndarray
) -> np.ndarray:
    """
    returns entry from pool with closest manhattan distance to srcpos

    srcpos: reference position
    pool: array of positions
    """
    deltas = np.abs(pool - srcpos)
    distances = np.sum(deltas, axis=1)
    idx = np.argmin(distances)
    return pool[idx]

def main():
    """ simply focuses on eating """
    REPRODUCTION_PROBABILITY = 0.1
    self_view, indices, entities, pheromones = from_json()
    names = np.array([entity.get('name', None) for entity in entities])
    edibility = np.array([entity.get('edible', False) for entity in entities])
    empties = set(map(tuple, indices[names == 'empty'])) & set(DIRECS)
    desired_actions = []
    if sum(edibility) > 0:
        locs = indices[edibility]
        target_loc = get_closest(np.array([0, 0]), locs)
        direction = veccast(np.sign(target_loc))
        if within_chebyshev_distance(target_loc, (0, 0), 1):
            desired_actions.append(('eat', veccast(target_loc)))
        elif tuple(direction) in empties:
            if randint(0, 100) < REPRODUCTION_PROBABILITY * 100:
                desired_actions.append(('reproduce', veccast(direction)))
            else:
                desired_actions.append(('step', veccast(direction)))
    elif len(empties) > 0:
        direction = choice(list(empties))
        desired_actions.append(('step', veccast(direction)))    
    with open('agent_output.json', 'w') as fp:
        json.dump(desired_actions, fp)
```
