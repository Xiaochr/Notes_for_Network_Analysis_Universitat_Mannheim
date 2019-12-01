[Back to menu](/README.md)

<h1 id = "3">Eigenvector Centrality</h1>

## For Undirected Graphs

The importance of a vertex is increased by having connections to other vertices that are important. 

A high eigenvector centrality indicates many neighbors or important neighbors or both. 

- $\mathbf{x}(t)=\mathbf{A}^{t} \mathbf{x}(0)$

Initialize $\mathbf{x}(0)$, all the vertices equal to 1. 

- When stable: 
    - $\mathbf{x^*}= const \cdot \mathbf{A} \mathbf{x^*}$
    - $\mathbf{x}^*$ is an eigenvector of $\mathbf{A}$. 
    - $\mathbf{x^*}=\lim _{t \rightarrow \infty} \mathbf{x}(t)=c_{1} \lambda_{1}^{t} \mathbf{v}_{1}$

- Iteration Steps: 
    - $\mathbf{x}(1)=\mathbf{A} \mathbf{x}(0)$
    - Normalize $\mathbf{x}(1)$
    - $\mathbf{x}(2)=\mathbf{A} \mathbf{x}(1)$
    - ...

- The power iteration method does not always converge. (when the adjacency matrix has another eigenvalue with the same absolute value as the principal eigenvalue)

### For Directed Graphs

- $A_{ij}$ is 1 when there is an edge **from j pointing to i**. 

- The adjacency matrix is not symmetrical in directed graphs. For unsymmetrical matrices, there are two sets of eigenvectors: left and right. 
    - **More common: right**. The right eigenvector centrality indicates a node is important if important nodes point towards it. 

- Limitations: 
    - In DAG (direct acyclic graphs), all nodes have left and right eigenvector centrality 0!
    - The only nodes with positive right / left eigenvector centrality are those in:
        - strongly connected components
        - in out-components / in-components of strongly connected components
    - A high-centrality vertex pointing to many vertices, gives all those vertices a very high centrality. (not always appropriate)

- Potential Solutions: (PageRank)
    - Give each vertex a small importance “for free”, so that none has importance
    - Divide the importance of a vertex equally among the nodes it points to

&nbsp;

---

[Back to top](#3)