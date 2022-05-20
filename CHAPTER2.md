```python
import networkx as nx
```


```python
G = nx.Graph()

G.add_nodes_from(['a','b','c','d'])

G.add_edges_from([('a','b'),('b','c'),('a','c'),('a','d')])

nx.draw(G, with_labels=True , font_size=20 ,font_color = 'yellow')
```


```python
nx.has_path(G, 'c', 'd')
```


```python
list(nx.all_simple_paths(G, 'c', 'd'))
```


```python
nx.shortest_path(G, 'c', 'd')
```


```python
nx.shortest_path_length(G, 'c', 'd')
```


```python
nx.is_connected(G)
```


```python
G = nx.Graph()
nx.add_cycle(G, [ 'x', 'y', 'z'])
G.add_edge('a','b')

nx.draw(G, with_labels=True ,font_size=23 ,font_color = 'red')
```


```python

```


```python
nx.is_connected(G)
```


```python
nx.shortest_path(G, 'z', 'b')
```


```python
nx.number_connected_components(G)
```


```python
list(nx.connected_components(G))
```


```python
components = list(nx.connected_components(G))
len(components[0])
```


```python
max(nx.connected_components(G), key=len)
```


```python
core_nodes = max(nx.connected_components(G), key=len)
core = G.subgraph(core_nodes)

nx.draw(core, with_labels=True ,font_size=26 ,font_color = 'cyan')
```


```python
D = nx.DiGraph()
D.add_edges_from([
    (1,2),
    (2,3),
    (3,2), (3,4), (3,5),
    (4,2), (4,5), (4,6),
    (5,6),
    (6,4),
])
nx.draw(D, with_labels=True ,font_size=15 ,font_color = 'yellow')
```


```python
nx.has_path(D, 1, 4)
```


```python
nx.has_path(D, 4, 1)
```


```python
nx.shortest_path(D, 2, 5)
```


```python
nx.shortest_path(D, 5, 2)

```


```python
nx.is_strongly_connected(D)

```


```python
nx.is_weakly_connected(D)
```


```python
list(nx.weakly_connected_components(D))

```


```python
list(nx.strongly_connected_components(D))

```


```python

```
