# Graph Theory

![Graph Def](img/graph.png)

![Graph Def](img/app.png)
#### Graph definition:
It’s enough to think of a graph G as simply a way of encoding pairwise relationships among a set of objects. Thus, G consists of a pair of sets (V, E) — a collection V of nodes and a collection E of edges, each of which “joins” two of the nodes. We thus represent an edge e ∈ E as a two-element subset of V: e = {u, v} for some u, v ∈ V, where we call u and v the ends of e.  
A graph G = (V , E) has two natural input parameters, the number of nodes
|V|, and the number of edges |E|. We denote n = |V| and m = |E|.

#### Directed graph:
A directed graph G′ consists of a set of nodes V and a set of directed edges E′. Each e′ ∈ E′ is an ordered pair (u, v); in other words, the roles of u and v are not interchangeable, and we call u the tail of the edge and v the head. We will also say that edge e′ leaves node u and enters node v.

A directed graph is strongly connected if, for every two nodes u and v, there is a path from u to v and a path from v to u. We also define two nodes u and v in a directed graph are __mutually reachable__ if there is a path from u to v and also a path from v to u.

#### Undirected graph:
An undirected graph is graph that a set of nodes are connected together, where all the edges are bidirectional. In contrast, a graph where the edges point in a direction is called a directed graph.


#### Bipartite graph:
A bipartite graph (or bigraph) is a graph whose vertices can be divided into two disjoint sets U and V (that is, U and V are each independent sets), such that __every edge connects a vertex in U to one in V__. Vertex set U and V are often denoted as partite sets. Equivalently, a bipartite graph is a graph that does not contain any odd-length cycles. 

_A complete bipartite graph with m = 5 and n = 3_   
![Bipartitle graph](./img/bipartite.png)

![Graph](img/conn.png)

![Graph](img/gtree.png)

> __Theory__: Let G be an undirected graph on n nodes. Any two of the following statements implies the third.

> 1. G is connected.
2. G does not contain a cycle.
3. G has n−1 edges.

![Graph](img/degree.png)

![Graph](img/indegree.png)

---

### Representing Graphs

![Matrix](./img/matrix.png)

- Consider a graph G = (V , E) with n nodes, and assume the set of nodes is V = {1, . . . , n}. The simplest way to represent a graph is by an adjacency matrix, which is an n × n matrix A where A[u, v] is equal to 1 if the graph contains the edge (u, v) and 0 otherwise.
- If the graph is undirected, the matrix A is symmetric, with A[u, v]= A[v, u] for all nodes u, v ∈ V. 
- The adjacency matrix representation allows us to check in O(1) time if a given edge (u, v) is present in the graph.
- Disadvantage: The representation takes 􏰘⊝(n<sup>2</sup>) space, and many graph algorithms need to examine all edges incident to a given node v.

_Undirected graph, adjacency matrix representation_:

![Undirected Matrix](./img/umatrix.jpg)

---

![Matrix](./img/list.png)

- we have an array Adj, where Adj[v] is a record containing a list of all nodes adjacent to node v.
- For an undirected graph G = (V, E), each edge e = (v, w) ∈ E occurs on two adjacency lists: node w appears on the list for node v, and node v appears on the list for node w.
- Good for sparse graphs. It only requires O(m + n) space.

_Undirected graph, adjacency list representation_:

![Undirected List](./img/ulist.jpg)

> The adjacency matrix representation of a graph requires O(n<sup>2</sup>) space, while the adjacency list representation requires only O(m + n) space.

- For a simple graph (no double edges) E ≤ V<sup>2</sup> = O(V<sup>2</sup>) 
- For a connected graph E ≥ V − 1
- For a completed graph E = V(V-1)/2
- For a tree E = V − 1

![Graph](img/wgraph.png)

Adjacency Matrix is a 2D array of size V x V where V is the number of vertices in a graph. Let the 2D array be adj[ ][ ], a slot adj[i][j] = 1 indicates that there is an edge from vertex i to vertex j. Adjacency matrix for undirected graph is always symmetric. Adjacency Matrix is also used to represent weighted graphs. If adj[i][j] = w, then there is an edge from vertex i to vertex j with weight w.

An array of linked lists is used. Size of the array is equal to number of vertices. Let the array be array[]. An entry array[i] represents the linked list of vertices adjacent to the ith vertex. This representation can also be used to represent a weighted graph. The weights of edges can be stored in nodes of linked lists.

---
### Articulation Point and Diameter
__An articulation point__ in an undirected graph is a vertex whose removal increases the number of connected components in the graph. Intuitively: Consider a node in a graph. If removing that node and all edges incident on that node 􏰀breaks􏰁 the graph into pieces, then the node is an articulation point.

The __diameter__ of an undirected, unweighted graph is the largest possible value of the following quantity: the smallest number of edges on any path between two nodes. In other words, it's the largest number of steps required to get between two nodes in the graph.

### Breadth-First Search
- Discover vertices in order of distance from the source.
- Works for undirected and directed graphs.

### Depth-First Search
![DFS](./img/dfs.png)

__Stack Implementation__:
![DFS](./img/dfstack.png)

Depth First Traversal can be used to detect cycle in a Graph. DFS for a connected graph produces a tree. There is a cycle in a graph only if there is a back edge present in the graph. A back edge is an edge that is from a node to itself (selfloop) or one of its ancestor in the tree produced by DFS.

### Minimum Edge Cover􏰞 Problem
Input is a connected, undi- rected graph G = (V, E) with |V | ≥ 2, and the output is the smallest possible set E′ such that E′ ⊆ E and for all vertices v ∈ V , there is an edge (v,u) in E′. That is, every vertex in the graph is the endpoint of some edge in E′.

Formally, an edge cover of a graph G is a set of edges E' such that each vertex in G is incident with at least one edge in E'. The set E' is said to cover the vertices of G. 

(最小覆盖边：一句话，就是用最少的边覆盖所有的点)

#### Pseudocode
```python
G(V, E)   //assumed stored in adjacency list
let S = V
let E' = {}

for v in S:
	calculate total number of edges incident to v, label as e 

sort S increasely with value e 
while (S is not empty):
	choose v in S with the smallest value e 
	foreach node connected to v:
		u = the node with the smallest e
	add (v, u) to E'
	remove v, u from S
return E'
```

---
![Total Order](img/to.png)
__Definition__: Relation between any pair of node (u, v) is explicit

![Partial Order](img/po.png)
__Definition__: Not all relations between pairs are explicit

### Topological Sort
A topological sort is a total order of the vertices of a graph G = (V,E) such that if (u,v) is an edge of G then u appears before v in the order.

#### Topological Sort Algorithm I
- Find each vertex’s in-degree (# of inbound edges) : O(m)
- While there are vertices remaining
	- Pick a vertex with in-degree zero and output it : O(n) 
	- Reduce the in-degree of all vertices it has an edge to : O(n)
	- Remove it from the list of vertices : O(1)
- __Runtime__: Θ(n<sup>2</sup>)
- __Note__: n = vertices, m = edges: m ∈ O (n<sup>2</sup>)

#### Topological Sort Algorithm II
- Find each vertex’s in-degree  : O(m)
- Initialize a queue to contain all in-degree zero vertices
- While there are vertices in the queue : O(n)
	- Dequeue a vertex v (with in-degree zero) and output it
	- Reduce the in-degree of all vertices v has an edge to
	- Enqueue any of these that now have in-degree zero
- __Runtime__: Θ(n + m)
- __Note__: n = vertices, m = edges: m ∈ O (n<sup>2</sup>)

---
![Minimum Spanning Tree](img/spant.png)

![Minimum Spanning Tree](img/krusal.png)

![Minimum Spanning Tree](img/kexe.png)

![Minimum Spanning Tree](img/proof.png)

