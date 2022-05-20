```python
import networkx as nx 
G = nx.DiGraph()
G.add_edges_from([('A','B'),('B','C'),('C','D')])
nx.draw(G,with_labels=True,node_color='red',node_size=2500,font_size=32)
print (get_leaves(G))
li_nodes=[]
def get_leaves (G):
    for node in G.nodes:
        if G.degree(node)==1:
            li_nodes.append(node)
    return li_nodes

```


```python

            
        
    
    
```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```
