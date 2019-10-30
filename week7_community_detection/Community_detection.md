[Back to menu](/README.md)

<h1 id = "7">Community Detection</h1>

## Contents

- [Girvan-Newman Algorithm](#1)
- [Modularity Maximization Algorithms](#2)
    - [Spectral Modularity Maximization](#21)
    - [Louvain Algorithm](#22)
- [Label Propagation Algorithm](#3)

<h2 id = "1">Girvan-Newman Algorithm</h2>

### Preparations

- Edge betweenness: 
    - For each edge, count the number of times it appears on shortest paths between node pairs. 
    - $C_{B}(e)=\frac{\sum_{s<t \atop(s, t) \neq e} \frac{n_{s t}^{e}}{g_{s t}}}{(n-1)(n-2) / 2}=\frac{2}{(n-1)(n-2)} \sum_{s<t \atop(s, t) \neq e} \frac{n_{s t}^{e}}{g_{s t}}$

### Algorithm Steps

1. Compute edge betweenness of all edges

2. Remove the edge(s) with highest score

3. Recalculate betweenness after removal and remove again

4. Repeat until there are no more edges

### Algorithm Performance

- Complexity $O(m n(m+n)) \sim O\left(n^{3}\right)$ for sparse networks. 

---

<h2 id = "2">Modularity Maximization Algorithms</h2>

- **Modularity** is the difference between the actual fraction of edges between nodes of the same type, and the expected fraction of edges between nodes of the same type if the edges were formed at random (while preserving node degree).

- $Q=\frac{1}{m}\left(\frac{1}{2} \sum_{i j} A_{i j} \delta\left(c_{i}, c_{j}\right)-\frac{1}{2} \sum_{i j} \frac{k_{i} k_{j}}{2 m} \delta\left(c_{i}, c_{j}\right)\right)=\frac{1}{2 m} \sum_{i j}\left(A_{i j}-\frac{k_{i} k_{j}}{2 m}\right) \delta\left(c_{i}, c_{j}\right)$
    - (actual - expected at random)

- Intuitively, a good division of a network in communities, should be a division that has **high** modularity

<h2 id = "21">2.1 Spectral Modularity Maximization</h2>

A divisive method

### Preparation

- $s_{i}=\begin{array}{ll}{+1 \text { if } i \text { belongs to } V_{1}} \\ {-1 \text { if } i \text { belongs to } V_{2}}\end{array}$, then $\delta\left(c_{i}, c_{j}\right)=\frac{1}{2}\left(s_{i} s_{j}+1\right)$

- Define **modularity matrix B**, $B_{i j}=A_{i j}-\frac{k_{i} k_{j}}{2 m}$

- Rewriting Q: 

    - $Q=\frac{1}{2 m} \sum_{i j} B_{i j} \delta\left(c_{i}, c_{j}\right)=\frac{1}{4 m} \sum_{i j} B_{i j}\left(s_{i} s_{j}+1\right)=\frac{1}{4 m} \sum_{i j} B_{i j} s_{i} s_{j}+\frac{1}{4 m} \sum_{i j} B_{i j}=\frac{1}{4 m} \sum_{i j} B_{i j} s_{i} s_{j}$
    - Notice that $\Sigma_{ij} B_ij = 0$
    - $Q = \frac{1}{4m} \mathbf{s^TBs}$

- Optimization problem: $\mathbf{s}^* = argmax_{\mathbf{s}} \mathbf{s^TBs} \qquad s_i \in \{-1, 1\}$

#### Relaxed version

- Relax the constraint to $\Sigma_i s^2_i = n$
    - $\mathbf{Bs} = \lambda\mathbf{s}$ and $Q = \frac{n}{4m} \lambda$
    - Since we want to maximize Q, so $\mathbf{s}_{relaxed}$ is the eigenvector of the **largest** eigenvalue of **B**. 
    - 让$\mathbf{s}_{relaxed}$的值化为-1或1(最接近的一个)，由此得到$\mathbf{s}^*$

- To split one network into **two** communities such that the modularity is maximized: 
    1. Compute the modularity matrix of the network
    2. Find the principal eigenvector of the modularity matrix
    3. Place all elements with a positive value in the principal eigenvector to a group and the ones with a negative value to the other group

#### Division into more communities 

- Intuition: 
    - Compute the change in modularity of the entire network
    - If the change is positive proceed and bisect $c_x$
    - Otherwise leave $c_x$ intact
    - repeat until there are no more communities whose bisection would produce a positive modularity change.

- $Q_{\text {before}}=\frac{1}{2 m} \sum_{i j} B_{i j} \delta(c_{i}, c_{j})=\frac{1}{2 m} \sum_{c \in C} \sum_{i j \in c} B_{i j}=\frac{1}{2 m} \sum_{c \in C-\left\{c_{x}\right\}} \sum_{i j \in c} B_{i j}+\frac{1}{2 m} \sum_{i j \in c_{x}} B_{i j}$

- $Q_{a f t e r}=\frac{1}{2 m} \sum_{c \in C-\{c_{x}\}{i} j \in c} \sum_{i j \in c_{x}} B_{i j \in c_{x}} B_{i j} \delta\left(c_{i}, c_{j}\right)$

- $\Delta Q\left(c_{x}\right)= Q_{after} - Q_{before} = \frac{1}{4 m} \sum_{i j \in c_{x}} B_{i j}\left(s_{i} s_{j}+1\right)-\frac{1}{2 m} \sum_{i j \in c_{x}} B_{i j}=\frac{1}{4 m}\left(\sum_{i, j \in c_{x}} B_{i j} s_{i} s_{j}-\sum_{i, j \in c_{x}} B_{i j}\right)$

- Define **D** as $D_{i j}=\begin{array}{ll}{\sum_{k} B_{i k},} & {\text { if } i=j} \\ {0} & {\text { otherwise }}\end{array}$, then $\sum_{i, j \in c_{x}} B_{i j}=\sum_{i, j \in c_{x}} D_{i j}=\sum_{i, j \in c_{x}} D_{i j} s_{i} s_{j}=\sum_{i, j \in c_{x}}\left(s_{i} s_{j} \delta_{i j} \sum_{k \in c_{x}} B_{i k}\right)$. 

- Hence $\Delta Q\left(c_{x}\right)=\frac{1}{4 m}\left(\sum_{i, j \in c_{x}} B_{i j} s_{i} s_{j}-\sum_{i, j \in c_{x}}\left(s_{i} s_{j} \delta_{i j} \sum_{k \in c_{x}} B_{i k}\right)\right)=\frac{1}{4 m} \sum_{i, j \in c_{x}}\left(B_{i j}-\delta_{i j} \sum_{k \in c_{x}} B_{i k}\right) s_{i} s_{j} = \frac{1}{4m} \mathbf{s^TB}^{(c_x)}\mathbf{s}$
    - $\mathbf{B}^{(c_x)}$ is community modularity matrix. 


### Algorithm Steps

- Init
    1. Compute the modularity matrix **B**
    2. Compute the leading eigenvector and divide **B** in two communities accordingly. 
    3. Add the two communities to the queue **Queue**

- While **Queue** is not empty: 
    1. c = pop(**Queue**)
    2. Compute matrix $\mathbf{B}^{(c)}$ 
    3. Compute its leading eigenvector $\mathbf{u_1}$
    4. If all elements in $\mathbf{u_1}$ have the same sign, leave community undivided
    5. else, divided c into 2 new communities, push the new communities in the **Queue**

### Algorithm Performance

- Complexity $O(m+n)\log{n} \sim O(n\log{n})$ on a sparse network. 
- Pretty fast, suitable for large networks

<h2 id = "22">2.2 Louvain Algorithm</h2>

Agglomerative algorithm: it starts with each node in its own community, communitiesemerge by merging. 

### Preparation


- Uses the modularity formalization with respect to communities
    - $Q = \Sigma_{c \in C} e_c - (a_c)^2$
    - $e_c$ 是在c里互相连接的edge个数（记得每个node都要算，即edge数要乘2），占总共edge数（同样乘2）的比例。
    - $a_c$ 是c里node所有edge的个数（不管连在里面还是外边）占总edge个数的比例。

- Calculate $\Delta Q$
    - $Q_{\text {before}}=\sum_{c \in c-\left[c_{x} c_{y}\right\}} Q_{c}+Q_{c_{x}}+Q_{c_{y}}$
    - $Q_{a f t e r}=\sum_{c \in c-\left\{c_{x}^{-}, c_{y}^{+}\right\}} Q_{c}+Q_{c_{x}^{-}}+Q_{c_{y}^{+}}$
    - $\Delta Q\left(x, c_{x}, c_{y}\right)=Q_{c_{x}^{-}}+Q_{c_{y}^{+}}-Q_{c_{x}}-Q_{c_{y}}$
    - Therefore, the computation of $\Delta Q$ requires the computation over the directly affected communities, not the entire network

### Algorithm Steps

1.  Each node is assigned to its own community –there are as many communities as there are nodes
2. Then for each node x, 
    - For each neighbor y, Evaluate the gain in overall network modularity if node x is moved into the community of y. 
    - Move node x to the community of the neighbor that results in maximum, positive modularity gain. 
    - If no such gain found, leave x in the original community. 
3.  Apply step 2 repeatedly and sequentially to all the nodes, until no further improvement can be obtained 
4. Build a new network in which nodes are the communities found in the previous step
    - Weigh the edges between the new nodes as the sum of the weight of the links between the nodes in the corresponding communities
    - Links between nodes of the same community result in weighted self-loops in the new network
5. Repeat steps 1-4 until no further improvement

### Algorithm Performance

- Complexity: exact time complexity not known because it is not known how many rounds are needed but:
    - $O(m+n)$ complexity of one round
    - $O(\log{n})$ rough approximation of the number of rounds. 
    - Total: $O((m+n)\log{n})$ or $O(n\log{n})$ on sparse network. 

---

<h2 id = "3">Label Propagation Algorithm</h2>

Does not optimize any objective function! Non-parametric: does not require the number of communities, nor sizes. Intuition: “I am the mode of my neighbors”. 

### Algorithm Steps

1. Assign each node to its own community
2. Pick a random node and update its community so that it joins the most frequent community among its neighbors 
    - Break ties: 
        - if the own community is also a max community, remain in 
        - otherwise, choose a max neighbor community uniformly at random
        - mark as visited
3. Repeat until all the nodes have been visited
4. Repeat steps 2 and 3 until no more changes occur 

### Algorithm Performance

- Complexity: 
    - $O(m)$ for one round
    - approx. 5 rounds required for multiple real-world networks

&nbsp;

---

THE END

&nbsp;

[Back to top](#7)