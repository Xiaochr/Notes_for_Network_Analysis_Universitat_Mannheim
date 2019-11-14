[Back to menu](/README.md)

<h1 id = "3">PageRank</h1>

$$\mathbf{x}(t+1) = \alpha \mathbf{Mx}(t) + \beta$$

## Naive PageRank

$$\mathbf{x}(t+1) = \alpha \mathbf{Mx}(t)$$

- Transition matrix **M**, $M_{i j}=\{\begin{array}{cc}{\frac{A_{i j}}{k_{j}^{o u t}}} & {\text { if } k_{j}^{o u t}>0} \\ {0} & {\text { otherwise }}\end{array}\}.$

- $\mathbf{x}(t) = \mathbf{M^tx}(0)$

- $\mathbf{x^*}$ is right eigenvector of **M**. 

### Problems: 

#### Dead Ends

- The importance “leaks out” of the system. When the random surfer reaches the dead ends, it disappears. 

##### Solutions to Dead Ends

- Prune and Propagate
    1. Recursively remove dead-ends, until no dead-ends are left in the graph
    2. Compute the PageRank for the remaining nodes
    3. Restore the graph and compute the PageRank of dead-end nodes as function of their solved incoming neighbors. (比如C被移去了，原先只有A连向C，而A的out degree为3，则C的PageRank为A的乘以$\frac{1}{3}$)

- Teleport
    1. When a dead-end is reached, “teleport” to a randomly selected node in the network 
    2. Equivalent to adding edges from all dead-ends to all nodes in the network (including to them-selves)
    3. Adjust the transition matrix so that all elements on zero-columns become $\frac{1}{n}$. We call the adjusted matrix **S**.

#### Spider Trap

- A spider trap is a strongly connected component where all  nodes have outgoing edges (no dead ends), but only among themselves, hence, no outgoing edge to any other node in the network.

- When the random surfer enters a spider trap, it cannot leave. Spider traps accumulate all the importance in the network. 

##### Solution to Spider Traps

- Modify the process of random surfers, so that at any point, they can teleport with a certain probability to a random node anywhere in the graph. 

- $\mathbf{x}(t+1)=\beta \mathbf{M} \mathbf{x}(t)+(1-\beta) \mathbf{1} / n$
    - $1 - \beta$ is the probability that the random surfer will teleport to any other node in the network
    - In networks with dead ends, there is still a fraction of importance that gets lost, so the final sum of all importances will be $< 1$

##### Solution to both Spider Traps and Dead Ends

- $\mathbf{x}(t+1)=\beta \mathbf{S} \mathbf{x}(t)+(1-\beta) \mathbf{1} / n$
    - Now the sum of $\mathbf{x}$ equals to 1. 

- The mathematical solution of $\mathbf{x}^{*}=\beta \mathbf{S} \mathbf{x}^{*}+(1-\beta) \mathbf{1} / n$ is equivalent to finding the principal eigenvector of **Google matrix**
    - $\mathbf{G}=\beta \mathbf{S}+\frac{(1-\beta)}{n} \mathbf{E}$
    - $\mathbf{E}$ is the $n \times n$ matrix of only 1's
    - Usually, $\beta$ is set such that $0.8 \leq \beta \leq 0.9$
    - For large networks the mathematical solution is very costly to compute. Practically, PageRank is computed iteratively. 

&nbsp;

---

[Back to top](#3)