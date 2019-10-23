[Back to menu](/README.md)

<h1 id = "6">Graph Partitioning</h1>

## Contents

- [Kernighan-Lin Algorithm](##1)
- [Spectral Partitioning](##2)

<h2 id = "1">Kernighan-Lin Algorithm</h2>

Local search, greedy algorithm. 

Intuition: Start with a random partitioning, Swap pairs of nodes from the two partitions, looking to reduce the cut size

### Preparations

- Internal costs $I_x$ as the number of edges it has to other nodes in its partition. 

- Exeternal costs $E_x$ as the number of edges node x has to nodes in the other partition. 

- Given $x \in V_1, y \in V_2$: 
    - $c u t_{-} \operatorname{size}\left(V_{1}, V_{2}\right)=c u t_{-} \operatorname{size}\left(V_{1}-\{x\}, V_{2}-\{y\}\right)+E_{x}+E_{y}-A_{x y}$
    - After swapping x and y: 
    $c u t_{-} \operatorname{size}(\widehat{V_{1}}, \widehat{V_{2}})=c u t_{-} \operatorname{size}\left(V_{1}-\{x\}, V_{2}-\{y\}\right)+I_{x}+I_{y}+A_{x y}$
    - So the **gain of swapping**: 
    $gain(x \in \widehat{V_{2}}, y \in \widehat{V_{1}}) = c u t_{-} \operatorname{size}\left(V_{1}, V_{2}\right) - c u t_{-} \operatorname{size}(\widehat{V_{1}}, \widehat{V_{2}}) = E_x + E_y - I_x - I_y - 2A_{xy}$

### Algorithm Steps

- Init: start with a random partitioning of the network $V_1$ and $V_2$ that respects the size restrictions. 

- Step 1: Compute the cut size of the partitioning

- Step 2: Mark all nodes as unvisited

- Step 3: For all the nodes, compute internal and external costs

- Step 4: For all pairs of nodes: ($x \in V_1, y \in V_2$) compute the gain of swapping

- Step 5:
    - 5.1: Select the pair $(x, y)$ with maximum gain of swapping and store in list swaps
    - 5.2: Mark nodes in selected pair as visited
    - Recompute all internal and external costs of all elements in $V_1 - \{x\}$ and $V_2 - \{y\}$ as though x and y would be swapped

- Repeat steps 4 and 5 until all nodes have been visited

- Step 6: Given the output sequence of swaps and their gains, select the subsequence that maximizes the cumulative gain

- Step 7: Apply all the swaps in the selected subsequence

- Repeat Steps 1 to 7 for as long as the maximum cumulative gain is strictly positive

### 说人话

先随机初始化，算每一对pair的gain（需要先算出每个node的内外部cost），挑最高的互换（如果有多个最高就随机选一个），标为visited。假设已经互换了，再算换过之后所有unvisited的pair（也就是剩下的）的gain，再挑再换直到挑完，形成一个gain的队列（例如4，-1，-2）。选择到最高的cumulative gain的那一步（如这里换第一步即可）真正地互换。

重复上面的步骤直到发现所有cumulative gain都是非正的，停止算法。

### Algorithm Performance

- Complexity: $O(mn^2)$ done several times
    - $O(n^3)$ on sparse networks
    - $O(n^4)$ on dense networks

This makes the algorithm inapplicable to networks bigger than a couple of thousands of nodes

&nbsp;

---

<h2 id = "2">Spectral Partitioning</h2>

It works with **Undirected** graphs. **Unweighted** or **positively weighted** graphs.

### Preparations

- The Laplacian Matrix

    - $\mathbf{L} = \mathbf{D} - \mathbf{A}$
        - $\mathbf{D}$ is the diagonal matrix with node degrees on the diagonal. $D_{i j}=\left\{\begin{array}{ll}{k_{i}} & {\text { if } i=j} \\ {0} & {\text { otherwise }}\end{array}\right.$
        
    - Properties: 
        - The Laplacian matrix is symmetrical. It has real eigenvalues. 
        - The eigenvalues are non-negative for a graph with non-negative edge weights. 
        - One of its eigenvalues is equal to 0, for corresponding eigenvector vector $\mathbf{1} = (1,...,1)^T$. The sum of all elements on a row/column is 0. Hence $\mathbf{1^TL} = \mathbf{0^T}$ and $\mathbf{L1 = 0}$. 
        - The second smallest eigenvalue of the Laplacian is non-zero iffthe graph is connected, called “algebraic connectivity”. 

- Formalizing the Cut-size

    - Consider a division of the nodes of the network into two groups $V_1$ and $V_2$. Then the cut-size: $R=\sum_{i \in V_{1}} \sum_{j \in V_{2}} A_{i j}$. 

    - Define $\mathbf{s}$: $s_{i}=\left\{\begin{array}{l}{+1 \text { if } i \in V_{1}} \\ {-1 \text { if } i \in V_{2}}\end{array}\right.$

- Rewriting $\quad R = \frac{1}{4} s^{\mathrm{T}} \mathrm{Ls}$

    - Proof: $R=\sum_{i \in V_{1}} \sum_{j \in V_{2}} A_{i j}=\frac{1}{4} \sum_{i j} A_{i j}\left(1-s_{i} s_{j}\right)=\frac{1}{4} \sum_{i j}\left(A_{i j}-A_{i j} s_{i} s_{j}\right)$
    - and $\sum_{i j} A_{i j}=\sum_{i j} D_{i j}=\sum_{i j} D_{i j} s_{i} s_{j}$
    - so $R=\frac{1}{4} \sum_{i j}\left(D_{i j} s_{i} s_{j}-A_{i j} s_{i} s_{j}\right)=\frac{1}{4} \sum_{i j} L_{i j} s_{i} s_{j}=\frac{1}{4} s^{\mathrm{T}} \mathrm{Ls}$

- **Optimization Problem**
    - Target: min $R = \frac{1}{4} s^{\mathrm{T}} \mathrm{Ls}$
    - Constraints: $s_i \in \{-1, 1\}$, $\Sigma_is_i = n_1 - n_2$ where $n_1$ and $n_2$ are the desired group sizes. 

### **Simplified Problem**

The problem without imposing the group sizes (without 2nd constraint). Relax 1st constraint to $\Sigma_is_i^2 = n$. (this constraint relaxation means that we remove the constraint on the direction of s, but we keep the magnitude constraint $|s| = \sqrt{n}$) 

So the simplified optimization problem: 

- $\mathbf{s}_{relaxed} = argmin_s \mathbf{s_tLs}$
- Constraint: $n - \Sigma_i s_i^2 = 0$

Use Lagrange multiplier, the problem becomes: 

- Find $\mathbf{s}_{relaxed}$ that minimize $\sum_{i j} L_{i j} s_{i} s_{j}+\lambda\left(n-\sum_{i} s_{i}^{2}\right)$. 

- Steps: 
    1. 求各个s的偏导
    2. 求偏导取0时的s. 
        - $\frac{\partial}{\partial s_{k}}\left[\sum_{i j} L_{i j} s_{i} s_{j}+\lambda\left(n-\sum_{i} s_{i}^{2}\right)\right]=0$
        - That is $\mathbf{Ls} = \lambda \mathbf{s}$
    3. $\mathbf{s_tLs}$ is minimum when $\lambda$ is min and $\lambda > 0$. That is, **$\lambda$ is the second smallest eigenvalue of $\mathbf{L}$.**

- $R_{relaxed} = \frac{1}{4} \lambda_2 n$, $\mathbf{s}_{relaxed} = \mathbf{v_2}$. $\mathbf{s}^*$ is the vector with $s_i \in \{-1, 1\}$ that is closest to $\mathbf{s}_{relaxed}$. 

- Algorithm Steps for Simplified Problem

    1. Write the Laplacian matrix. 
    2. Find the eigenvector $\mathbf{v}_2$ corresponding to the second smallest eigenvalue of $\mathbf{L}$. 
    3. Put all nodes with negative value in $\mathbf{v}_2$ in one group and all with positive value in the other group. 

### Spectral Partitioning **with Specified Sizes**

When sizes are not specified, spectral partitioning is able to split nodes in 2 balanced groups.

Relax 1st constraint and add back 2nd constraint. 

- Algorithm Steps: 
    1. Write the Laplacian matrix. 
    2. Find the eigenvector $\mathbf{v}_2$ corresponding to the second smallest eigenvalue of $\mathbf{L}$. 
    3. Sort the elements in $\mathbf{v}_2$. 
    4. Starting from one end, put the nodes corresponding to the first $n_1$ values in one group and the remaining ones in the other group; then count the cut size. 
    5. Do the same as in step 4, starting from the other end. 
    6. Take the split obtained at step 4 or 5, that provided the smallest cut set.

### Algorithm Performance

- The computation of the second eigenvector of the Laplacian is the most time-consuming part. 

- $O(mn) \to O(n^2)$ on sparse graphs. (Better than Kernighan-Lin)

### Spectral Partitioning with Specified Sizes (Advanced)

To be finished...

---

[Back to top](#6)