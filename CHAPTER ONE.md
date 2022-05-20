```python
import networkx as nx 
G = nx.DiGraph()
G.add_edges_from([('A','B'),('B','C'),('C','D'),('D','A'),('E','A'),('E','B'),('E','C'),('E','D')])
nx.draw(G,with_labels=True,node_color='red',node_size=2500,font_size=32)
```


```python
G.has_edge('E','A')
```


```python
G.has_edge('A','E')
```


```python
print('Successors of D:', list(G.successors('D')))
```


```python
print('Predecessors of D:', list(G.predecessors('D')))
```


```python
G.in_degree('E')
```


```python
G.out_degree('E')
```


```python
G.degree('D')
```


```python

```
