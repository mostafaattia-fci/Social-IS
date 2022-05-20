```python
import networkx as nx
```


```python
G = nx.read_edgelist('ia-enron-only.edges', nodetype=int)
print(nx.info(G))
nx.draw(G)
```


```python
max([1,2,3,4,5])
```


```python
max(['apple', 'grape', 'carrot'])

```


```python
max(['apple', 'grape', 'carrot'], key=len)
```


```python
highest_degree_node = max(G.nodes, key=G.degree)
highest_degree_node
```


```python
G.degree(highest_degree_node)
```


```python
betweenness = nx.centrality.betweenness_centrality(G)
highest_betweenness_node = max(G.nodes, key=betweenness.get)
highest_betweenness_node
```


```python

betweenness[highest_betweenness_node]
```


```python
degree_sequence = [G.degree(n) for n in G.nodes]
```


```python
import statistics

print('Mean degree:', statistics.mean(degree_sequence))
print('Median degree:', statistics.median(degree_sequence))
```


```python
betweenness = nx.centrality.betweenness_centrality(G)
betweenness_sequence = list(betweenness.values())

print('Mean betweenness:', statistics.mean(betweenness_sequence))
print('Median betweenness:', statistics.median(betweenness_sequence))
```


```python
from collections import Counter

degree_counts = Counter(degree_sequence)
degree_counts
```


```python
min_degree, max_degree = min(degree_counts.keys()), max(degree_counts.keys())

plot_x = list(range(min_degree, max_degree + 1))
```


```python
plot_y = [degree_counts.get(x, 0) for x in plot_x]
```


```python
import matplotlib.pyplot as plt

plt.bar(plot_x, plot_y)
```


```python
counts, bins, patches = plt.hist(betweenness_sequence, bins=10)
```


```python
bins
```


```python
counts
```


```python
nx.connected_components(G)
```


```python
core = next(nx.connected_components(G))
core
```


```python
len(core)

```


```python
components = list(nx.connected_components(G))

```


```python
len(components)

```


```python
C = G.copy()

```


```python
import random

nodes_to_remove = random.sample(list(C.nodes), 2)
C.remove_nodes_from(nodes_to_remove)
```


```python
number_of_steps = 25
M = G.number_of_nodes() // number_of_steps
M
```


```python
num_nodes_removed = range(0, G.number_of_nodes(), M)

```


```python
N = G.number_of_nodes()
C = G.copy()
random_attack_core_proportions = []
for nodes_removed in num_nodes_removed:
    # Measure the relative size of the network core
    core = next(nx.connected_components(C))
    core_proportion = len(core) / N
    random_attack_core_proportions.append(core_proportion)
    
    # If there are more than M nodes, select M nodes at random and remove them
    if C.number_of_nodes() > M:
        nodes_to_remove = random.sample(list(C.nodes), M)
        C.remove_nodes_from(nodes_to_remove)
plt.title('Random failure')
plt.xlabel('Number of nodes removed')
plt.ylabel('Proportion of nodes in core')
plt.plot(num_nodes_removed, random_attack_core_proportions, marker='o')
```


```python
nodes_sorted_by_degree = sorted(G.nodes, key=G.degree, reverse=True)
top_degree_nodes = nodes_sorted_by_degree[:M]
top_degree_nodes
```


```python
N = G.number_of_nodes()
number_of_steps = 25
M = N // number_of_steps

num_nodes_removed = range(0, N, M)
C = G.copy()
targeted_attack_core_proportions = []
for nodes_removed in num_nodes_removed:
    # Measure the relative size of the network core
    core = next(nx.connected_components(C))
    core_proportion = len(core) / N
    targeted_attack_core_proportions.append(core_proportion)
    
    # If there are more than M nodes, select top M nodes and remove them
    if C.number_of_nodes() > M:
        nodes_sorted_by_degree = sorted(C.nodes, key=C.degree, reverse=True)
        nodes_to_remove = nodes_sorted_by_degree[:M]
        C.remove_nodes_from(nodes_to_remove)
```


```python
plt.title('Targeted attack')
plt.xlabel('Number of nodes removed')
plt.ylabel('Proportion of nodes in core')
plt.plot(num_nodes_removed, targeted_attack_core_proportions, marker='o')
```


```python

```
