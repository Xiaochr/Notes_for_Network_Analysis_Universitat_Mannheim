[Back to menu](/README.md)

<h1 id = "9">Static Random Graphs</h1>

## Content

- [G(n, m) Model](#1)
- [Erdos-Renyi Model - G(n, p) Model](#2)
- [The Configuration Model](#3)
- [The small world model of Watts and Strogatz](#4)

**Random graph models** are meant to be simplifications of the real-world complex networks, so that they can be mathematically analyzed, and so that the effects of their properties can be traced. 

<h2 id = "1">G(n, m) Model</h2>

### To construct the model: 

- Fix the number of **vertices n** and the number of **edges m**. 
- Out of $C_n^2 = \frac{n(n-1)}{2}$ pairs of nodes, randomly select m, and add an edge between them. 

### Properties

- There are $C_{C_n^2}^m$ individual graphs in the $G(n, m)$ family. 
- Average degree: $\langle k \rangle = c = \frac{2m}{n}$

<h2 id = "2">Erdos-Renyi Model - G(n, p) Model</h2>

### To construct the model:

- Fix the number of **vertices n**. 
- Decide a value for $p \in [0, 1]$, the probability of an edge existing between any two vertices. 
- For each pair of vertices
    - Randomly choose a number $\in [0, 1)$
    - If the number is smaller than p, add an edge between the pair. Otherwise do not add an edge. 

### Properties

- Probability of a graph with m edges: 

$$P(m)= C_{C_n^2}^m p^{m}(1-p)^{C_n^2 - m}$$

- Mean number of edges $\langle m\rangle = p\frac{n(n-1)}{2}$

- Mean degree $\langle k \rangle = c = \frac{1}{n} \sum_{i} k_{i}=\frac{2\langle m\rangle}{n}=(n-1) p$

- Density $\langle\rho\rangle=\frac{\langle m\rangle}{n(n-1) / 2}=p$

#### Clustering Coefficient

- Real world graphs are usually sparse, the global clustering coefficient tends to be 0 when n is large. 
    - slides上给的证明感觉说不通……

- Local clustering coefficient
    - $C_{i}=\frac{\frac{p k_{i}\left(k_{i}-1\right)}{2}}{\frac{k_{i}\left(k_{i}-1\right)}{2}}=p$
    - $C_{a v g}=\frac{\sum_{i} c_{i}}{n}=\frac{n p}{n}=p=C=\frac{c}{n-1} \stackrel{n \rightarrow \infty}{\longrightarrow} 0$

- Low clustering coefficients and generally low frequency of loops, random graphs are locally **tree-like**. 
    - The average number of vertices s steps away from a randomly chosen vertex is $c^s$

#### Diameter

- The diameter is approximately $\frac{\log{n}}{\log{c}}$
    - Proof: All nodes are reached when $c^s \approx n$, that is $s \approx \frac{\log{n}}{\log{c}}$. 
    - Random graphs have the small world property. 

#### Degree Distribution

- The probability of a node to be connected to exactly k other nodes: (binomial degree distribution)

$$p_{k}=C_{n-1}^k p^{k}(1-p)^{n-1-k}$$

- When n is very large, approximate to Poisson distribution: 

$$p_{k}=e^{-c} \frac{c^{k}}{k !}$$

- $G(n, p)$ random graphs are also called Poisson random graphs. 

#### Giant Component

- A **giant component** is a component whose size is a positive function of n. 

- $u$ denotes the average fraction of vertices in the random graph that do NOT belong to the giant component. 
    - A node does NOT belong to the giant component if none of its neighbors belongs to the giant component:
    
    $$u=p_{0}+p_{1} \cdot u+p_{2} \cdot u^{2}+\cdots=\sum_{k=0}^{\infty} p_{k} u^{k}$$

    - Estimation:

    $$u \approx e^{-c} \sum_{k} \frac{(u c)^{k}}{k !} \approx e^{-c(1-u)}$$

- Then the size of giant component: 

$$S = 1 - u = 1 - e^{-cS}$$

- Phase transition at $c = 1$. 
    - Generally, $G(n, p)$ random graph has a giant component if $c > 1$. 
    - When $c \leq 1$, $S = 0$. 

### Limitations

- They show no transitivity (clustering coefficient approaching zero) while real world networks are characterized by high clustering coefficients. 
- They show no assortative mixing by degree
- They have no community structure. 
- They do not have a right-skewed degree distribution. 

<h2 id = "3">The Configuration Model</h2>

- Random graphs with n nodes and a given degree sequence. 

### To construct the model

- To each vertex i, provide $k_i$ tubs. 
- Choose randomly 2 tubs and connect them. 
- Do the same until there is no tub left. 

### Properties

- Probability that two nodes are connected: 

$$p_{i j}=\frac{k_{i} k_{j}}{2 m-1}$$

- The graphs can contain self-and multi-edges
- The configuration model has the small world property
- The configuration model can model graphs with power law distribution
- The configuration model has a clustering coefficient approaching zero

<h2 id = "4">The small world model of Watts and Strogatz</h2>

- Real world networks have:
    - **Short average shortest paths**. Similar to networks formed at random. 
    - **Relatively high avgclustering coefficient**. Similar to regular networks. 

### To construct the model

- Obtained through random-rewiring that preserves the number of nodes and number of edges
    - pick a random edge
    - with probability p choose to rewire the edge by keeping one endnode the same and rewiring the other one to a randomly chosen node

### Properties

- When $p = 0$, the network is a regular ring lattice: high clustering and long shortest paths. 

- When $p = 1$, each edge is rewired, so the network becomes a random network: low clustering and short shortest paths. 

- Even tiny amounts of irregularity can dramatically shorten the shortest paths in an (almost) regular network, while it barely affects the clustering coefficient. 

&nbsp;

---

[Back to top](#9)