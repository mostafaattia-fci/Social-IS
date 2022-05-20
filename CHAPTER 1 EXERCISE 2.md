```python
import networkx as nx 
G = nx.Graph()
G.add_edges_from([(1,2),(2,3),(3,4),(4,1),(4,2),(2,5)])
nx.draw(G,with_labels=True,node_color='lightblue',node_size=2000,font_size=27)
print (max_degree(G))



```


```python
max_grade=[]
def max_degree(G):
    for node in range(G.nodes): 
        max_grade=max(G.degree(node))
        max_grade.append(node)
    return max_grade
print(max_grade)
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
