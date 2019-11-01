[Back to menu](/README.md)

<h1 id = "3">HITS</h1>

- With HITS(Hyperlink-Induced Topic Search), each node has 2 scores: an authority centrality, a hub centrality. 
    - **Hubs** are important because they point towards important nodes. $x_i$
        - $\mathbf{x} = \alpha \mathbf{Ay}$
    - **Authorities** are important because they are pointed to by important nodes. $y_i$
        - $\mathbf{y} = \beta \mathbf{A^Tx}$

- After some computations: 
    - $\mathbf{x}(t + 1) = \alpha \beta \mathbf{AA^Tx}(t)$
    - $\mathbf{y}(t + 1) = \alpha \beta \mathbf{A^TAy}(t)$

- $x^*$ is the principal eigenvector of $AA^T$. $y^*$ is the principal eigenvector of $A^TA$. 

### Iterative Computation

- Start with $\mathbf{x}(0) = \mathbf{1}$
- Iteratively apply the mutual recursion:
    1. Apply hubs score update rule. Normalize hub scores (so that the largest component equals to 1). 
    2. Apply authority score update rule. Normalize authority scores (so that the largest component equals to 1).
    3. Repeat until convergence. 

&nbsp;

---

[Back to top](#3)