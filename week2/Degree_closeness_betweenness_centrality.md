[Back to menu](/README.md)

<h1 id = "2">Degree, Closeness and Betweenness Centrality</h1>

## Contents

- [Degree Centrality](#21)
- [Closeness Centrality](#22)
- [Betweenness Centrality](#23)

---

<h2 id = "21">Degree Centrality</h2>

The number of edges connected to a node.

For undirected graphs:

- $C_{D}(i)=k_{i}=\sum_{j=1}^{n} A_{i j}=\sum_{j=1}^{n} A_{j i}$

- Normalized: $C_{D}^{\prime}(i)=k_{i} /(n-1)=\frac{\sum_{j=1}^{n} A_{i j}}{n-1}=\frac{\sum_{j=1}^{n} A_{j i}}{n-1}$

For directed graphs: 

- In-degree centrality: $\sum_{j=1}^{n} A_{i j}$

- Out-degree centrality: $\sum_{j=1}^{n} A_{j i}$

&nbsp;

---

<h2 id = "22">Closeness Centrality</h2>

The average of the shortest distances to all the other nodes. 

For undirected graphs: 

- $C_{c}(i)=\frac{n-1}{\sum_{j=1}^{n} d(i, j)}$

- $d(i, j)$ denotes the length of the shortest path between vertices i and j

For directed graphs: 

- Incoming closeness:

    - $C_{c}^{i n}(i)=\frac{n-1}{\sum_{j=1}^{n} d d(j, i)}$
    - $dd(j, i)$ denotes the length of the shortest directed path from j to i

- Outgoing closeness:

    - $C_{c}^{out}(i)=\frac{n-1}{\sum_{j=1}^{n} d d(i, j)}$
    - $dd(i, j)$ denotes the length of the shortest directed path from i to j

**Problem**: What happens when the graph has 2 or more components? (there exists $d(x, y) \rightarrow \infty$)

- Solution 1: compute closeness centrality with respect to the component the vertex is part of. 

- Solution 2: redefine closeness in terms of the harmonic mean of the distances between vertices (**Harmonic Closeness Centrality**).

    - $C_{c}^{\prime}(i)=\frac{1}{n-1} \sum_{j=1 \atop j \neq i}^{n} \frac{1}{d(i, j)}$

&nbsp;

---

<h2 id = "23">Betweenness Centrality</h2>

The extent to which a node lies on the shortest paths between the other nodes. 

For undirected graphs:

- $C_B(i) = \frac{2}{(n-1)(n-2)} \sum_{s<t \atop s, t \neq i} \frac{n_{s t}^{i}}{g_{s t}}$

- $g_{st}$ denotes the number of shortest paths between vertices s and t. 

- $n_{st}^i$ denotes the number of shortest paths between vertices s and t that i is on. 

For directed graphs:

- $C_B^{dir}(i) = \frac{1}{(n-1)(n-2)} \sum_{s<t \atop s, t \neq i} \frac{n_{s t}^{i}}{g_{s t}}$

- $(n - 1)(n - 2)$ denotes the number of directed pairs of nodes excluding i. 

&nbsp;

[Back to top](#2)