# Shortest Path Project Instructions

This file explains how to run the example algorithms in the repository and how the code is organized.

## 1. Repository structure

- `algo/`
  - `dijkstra.py` — Dijkstra algorithm for shortest paths.
  - `bellman_ford.py` — Bellman-Ford algorithm for shortest paths with negative weights.
  - `floyd_warshall.py` — Floyd-Warshall algorithm for all-pairs shortest distances.
- `graph/`
  - `graph3.py` — example graph data used by the notebook.
  - Other graph files are currently empty templates.
- `display/`
  - `display_tool.py` — drawing helpers for tables and visuals.
  - `display_graph3.ipynb` — notebook that renders trace tables for `GRAPH_5`.
  - `display_graph1.ipynb` through `display_graph6.ipynb` — notebooks for each graph exercise.

## 2. Graph format

Graphs are stored as nested Python dictionaries.

Example:

```python
GRAPH_5 = {
    'a': {'b': 5, 'd': 1, 'f': 3},
    'b': {'a': 4, 'd': 3, 'e': 3, 'c': 2},
    # ...
}
```

- Outer keys are node names.
- Inner keys are neighbor nodes.
- Inner values are the edge weights.

## 3. GitHub repository URL

This project is hosted at:

https://github.com/Lilydayooo/Graph-HW (Privated)

## 4. How to run the code locally

Use these commands from the repository root:

```powershell
cd "E:\HCMUT_Work\HCMUT_IMP\HK252\Advanced_Algorithm\Homework\Graph-HW" (Your Path)
python -c "from algo.dijkstra import dijkstra; from graph.graph5 import GRAPH_5; dist, prev = dijkstra(GRAPH_5, 'a'); print(dist); print(prev)"
```

If you clone the project from GitHub, run:

```powershell
git clone https://github.com/Lilydayooo/Graph-HW
cd Graph-HW
python -c "from algo.dijkstra import dijkstra; from graph.graph5 import GRAPH_5; dist, prev = dijkstra(GRAPH_5, 'a'); print(dist); print(prev)"
```

## 5. Algorithm usage examples

### Dijkstra

```python
from algo.dijkstra import dijkstra
from graph.graph3 import GRAPH_5

distances, previous = dijkstra(GRAPH_5, 'a')
print(distances)
print(previous)
```

- Use Dijkstra when edge weights are all non-negative.

### Bellman-Ford

```python
from algo.bellman_ford import bellman_ford
from graph.graph3 import GRAPH_5

distances, previous, negative_cycle = bellman_ford(GRAPH_5, 'a')
print(distances)
print(previous)
print('negative cycle:', negative_cycle)
```

- Bellman-Ford works with negative edge weights.
- It also reports whether a negative cycle exists.

### Floyd-Warshall

```python
from algo.floyd_warshall import floyd_warshall
from graph.graph3 import GRAPH_5

distances, negative_cycle = floyd_warshall(GRAPH_5)
print(distances)
print('negative cycle:', negative_cycle)
```

- Floyd-Warshall computes distances between every pair of nodes.

## 6. How to use the notebooks

Open any notebook in `display/` and run each cell.

Use notebooks for each graph exercise:
- `display_graph5.ipynb` for `graph.graph5`

Each notebook imports its corresponding graph and then shows three sections:

- Dijkstra trace
- Bellman-Ford trace
- Floyd-Warshall trace

### How to edit graph data

Each `graph/graphX.py` file should define a dictionary named `GRAPH_X` using the same structure as `graph5.py`.

Example for `graph5.py`:

```python
GRAPH_5 = {
    'a': {'b': 5, 'd': 1, 'f': 3},
    'b': {'a': 4, 'd': 3, 'e': 3, 'c': 2},
    'c': {'b': 4, 'e': 2, 'h': 5},
    'd': {'b': 5, 'e': 4, 'a': 2},
    'e': {'b': 3, 'c': 3, 'd': 4, 'f': 2, 'g': 1},
    'f': {'a': 1, 'e': 2, 'g': 1},
    'g': {'f': 1, 'e': 1, 'h': 2},
    'h': {'c': 1, 'g': 4},
}
```

Copy this style into `graphX.py`, updating the node names and weights for each graph exercise.

## 7. Notes for teammates

- `distances` shows the shortest distance values.
- `previous` stores the previous node for each path.
- In Floyd-Warshall, `distances[i][j]` is the shortest path from `i` to `j`.
- If a distance is `inf`, there is no path.

## 8. Optional: path reconstruction example

```python
from algo.dijkstra import dijkstra
from graph.graph3 import GRAPH_5

def build_path(prev, target):
    path = []
    node = target
    while node is not None:
        path.append(node)
        node = prev[node]
    return list(reversed(path))


distances, previous = dijkstra(GRAPH_5, 'a')
print(build_path(previous, 'z'))
```

This builds the shortest path from `a` to `z`.
