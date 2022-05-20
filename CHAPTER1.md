```python
import networkx as nx 
G = nx.Graph()
nodes = ['x', 'y', 'z','w']
G.add_nodes_from(nodes)
edges = [('x', 'y'), ('y', 'z'), ('x', 'w'),('z','w'),('x','z')]
G.add_edges_from(edges)
nx.draw(G, with_labels=True,node_size=2000,node_color='yellow',font_color='red',font_size=16)
G.nodes()
G.edges()
for node in G.nodes:
    print(node)
for edge in G.edges:
    print(edge)

```


```python
nx.is_tree(G)
```


```python
nx.is_connected(G)
```


```python
list(G.neighbors('y'))
```


```python
G.number_of_edges()
```


```python
G.number_of_nodes()
```


```python
G.has_node('c')
```


```python
G.has_edge('y', 'z')
```


```python
len(list(G.neighbors('y')))
```


```python
G.degree('z')
```


```python

```
