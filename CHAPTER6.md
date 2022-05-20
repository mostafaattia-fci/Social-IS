```python
import random

%matplotlib inline
import networkx as nx
```


```python
G = nx.Graph()
nx.add_cycle(G ,[0, 1, 2, 3])
nx.add_cycle(G ,[4, 5, 6, 7])
G.add_edge(0, 7)

nx.draw(G, with_labels=True)
```


```python
partition = [
    {1, 2, 3},
    {4, 5, 6},
    {0, 7},
]
```


```python
nx.community.is_partition(G, partition)
```


```python
partition_map = {}
for idx, cluster_nodes in enumerate(partition):
    for node in cluster_nodes:
        partition_map[node] = idx

partition_map
```


```python
partition_map[0] == partition_map[7]
```


```python
node_colors = [partition_map[n] for n in G.nodes]
        
nx.draw(G, node_color=node_colors, with_labels=True)
```


```python
def modularity(G, partition):
    W = sum(G.edges[v, w].get('weight', 1) for v, w in G.edges)
    summation = 0
    for cluster_nodes in partition:
        s_c = sum(G.degree(n, weight='weight') for n in cluster_nodes)
        # Use subgraph to count only internal links
        C = G.subgraph(cluster_nodes)
        W_c = sum(C.edges[v, w].get('weight', 1) for v, w in C.edges)
        summation += W_c - s_c ** 2 / (4 * W)
    
    return summation / W
```


```python
modularity(G, partition)
```


```python
partition_2 = [
    {0, 1, 2, 3},
    {4, 5, 6, 7},
]
modularity(G, partition_2)
```


```python
nx.community.quality.modularity(G, partition_2)

```


```python
K = nx.karate_club_graph()
nx.draw(K, with_labels=True)

```


```python
K.nodes[0]

```


```python
K.nodes[9]


```


```python
K = nx.karate_club_graph()
club_color = {
    'Mr. Hi': 'orange',
    'Officer': 'lightblue',
}
node_colors = [club_color[K.nodes[n]['club']] for n in K.nodes]
nx.draw(K, node_color=nodes_colors, with_labels=True)
```


```python
groups = {
    'Mr. Hi': set(),
    'Officer': set(),
}

for n in K.nodes:
    club = K.nodes[n]['club']
    groups[club].add(n)
    
groups
```


```python
empirical_partition = list(groups.values())
empirical_partition
```


```python
nx.community.is_partition(K, empirical_partition)
```


```python
random_nodes = random.sample(K.nodes, 17)
random_partition = [set(random_nodes),
                    set(K.nodes) - set(random_nodes)]
random_partition
```


```python
random_node_colors = ['orange' if n in random_nodes else 'lightblue' for n in K.nodes]
nx.draw(K, node_color=random_node_colors)
```


```python
nx.community.quality.modularity(K, random_partition)

```


```python
G = nx.karate_club_graph()
nx.draw(G)
```


```python
nx.edge_betweenness_centrality(G)

```


```python
my_edge_betweenness = nx.edge_betweenness_centrality(G)
my_edge_betweenness[0, 1]
```


```python
max(my_edge_betweenness, key=my_edge_betweenness.get)

```


```python
max(G.edges(), key=my_edge_betweenness.get)

```


```python
my_edge_betweenness = nx.edge_betweenness_centrality(G)
most_valuable_edge = max(G.edges(), key=my_edge_betweenness.get)
G.remove_edge(*most_valuable_edge)
```


```python
nx.connected_components(G)

```


```python
list(nx.connected_components(G))

```


```python
G = nx.karate_club_graph()
partition_sequence = []
for _ in range(G.number_of_edges()):
    my_edge_betweenness = nx.edge_betweenness_centrality(G)
    most_valuable_edge = max(G.edges(), key=my_edge_betweenness.get)
    G.remove_edge(*most_valuable_edge)
    my_partition = list(nx.connected_components(G))
    partition_sequence.append(my_partition)
```


```python
len(partition_sequence), nx.karate_club_graph().number_of_edges()

```


```python
len(partition_sequence[0])

```


```python
import matplotlib.pyplot as plt
plt.plot(modularity_sequence)
plt.ylabel('Modularity')
plt.xlabel('Algorithm step')
```


```python
G = nx.karate_club_graph()
modularity_sequence = [modularity(G, p) for p in partition_sequence]
modularity_sequence
```


```python
best_partition = max(partition_sequence, key=nx.community.quality.modularity)

```


```python

def my_modularity(partition):
    return nx.community.quality.modularity(G, partition)
best_partition = max(partition_sequence, key=my_modularity)
```


```python
best_partition

```


```python
def create_partition_map(partition):
    partition_map = {}
    for idx, cluster_nodes in enumerate(partition):
        for node in cluster_nodes:
            partition_map[node] = idx
    return partition_map
```


```python
best_partition_map = create_partition_map(best_partition)

node_colors = [best_partition_map[n] for n in G.nodes()]
nx.draw(G, with_labels=True, node_color=node_colors)
```


```python
nx.community.quality.modularity(G, best_partition)

```


```python
for partition in partition_sequence:
    if len(partition) == 2:
        two_cluster_partition = partition
        break

two_cluster_partition
```


```python
two_cluster_partition_map = create_partition_map(two_cluster_partition)

node_colors = [two_cluster_partition_map[n] for n in G.nodes()]
nx.draw(G, with_labels=True, node_color=node_colors)
```


```python
import matplotlib.pyplot as plt

pos = nx.layout.spring_layout(G)
fig = plt.figure(figsize=(15, 6))

plt.subplot(1, 2, 1)
two_cluster_partition_map = create_partition_map(two_cluster_partition)
node_colors = [two_cluster_partition_map[n] for n in G.nodes()]
nx.draw(G, with_labels=True, node_color=node_colors, pos=pos)
plt.title('Predicted communities')

plt.subplot(1, 2, 2)
node_colors = [G.nodes[n]['club'] == 'Officer' for n in G.nodes()]
nx.draw(G, with_labels=True, node_color=node_colors, pos=pos)
plt.title('Actual communities')
```


```python
G.nodes[8]

```


```python
list(nx.community.girvan_newman(G))[:5]

```


```python

```
