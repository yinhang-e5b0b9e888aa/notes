# networkx

# networkx 画图
```
import networkx as nx
import pylab

G=nx.DiGraph()
# Add nodes and edges
G.add_edge(1, 2, r=9)
G.add_edge(2, 3, r=8)
G.add_edge(3, 2, r=7)
#nx.draw(G, with_labels = True)

pos=nx.spring_layout(G)

pylab.figure(2)
nx.draw(G,pos, with_labels=True)
# specifiy edge labels explicitly
edge_labels=dict([((u,v,),d['r'])
             for u,v,d in G.edges(data=True)])
nx.draw_networkx_edge_labels(G,pos,edge_labels=edge_labels, label_pos=0.3, font_size=7)

# show graphs
pylab.show()
```
