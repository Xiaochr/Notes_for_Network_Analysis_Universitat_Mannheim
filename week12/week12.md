[Back to menu](/README.md)

<h1 id = "12">Diffusion of Innovation (continued)</h1>

## Content
- [Independent Cascade Model](#1)
- [Threshold Model](#2)

<h2 id = "1">1. Independent Cascade Model</h2>

### 1.1 Homogeneous Population

- Every inactive node has a probability of adopting due to **external factors** ($p$) and **contagious neighbors** ($\beta$). 
- Notations
    - $I$: nodes have not adopted.
    - $C$: active and contagious nodes.
    - $U$: active(have adopted) but not contagious. 
- Each node who adopted has only one chance to influence its neighbors. 
- Given the node i has not adopted by time $t-1$, the probability that it adopts at time $t$ is:

$$q_{i}(t)=1-(1-p)(1-\beta)^{k_{i, C(t-1)}}$$

- The probability that a node i is active at time t: 

$$x_{i}(t)=1-\prod_{t^{\prime}=0}^{t}(1-q_{i}(t^{\prime})) = 1-(1-p)^{t+1}(1-\beta)^{\sum_{t^{\prime}=0}^{t}k_{i, C\left(t^{\prime}-1\right)}} =1-(1-p)^{t+1}(1-\beta)^{k_{i, X(t-1)}}$$

- Note that the probabilities at time t are computed based on the known state of the neighbors at time t-1, not on estimations! 

### 1.2 Heterogeneous Population 

- The same process as in the homogeneous one, except for $p_i$ and $\beta_{j, i}$. 
- Without spontaneous adoption:
    - Requires a set of initial adopters. Further adoptions happen only through the network. 
    - Very likely, the diffusion process finishes without all nodes having adopted. 
- With spontaneous adoption: 
    - Does not require initial adopters. The innovation will be adopted by the entire network. 
- Estimating the probability of adoption at $t+1$, when the exact states of all nodes are not known. 
    - $q_{i}(t+1)=1-\left(1-p_{i}\right) \prod_{j \in N_{i}}\left(1-\beta_{j, i}\right) q_{j}(t)$
    - No solution in closed form. 
    - In practice the estimation of the fraction of adopting individuals is done with numerical simulations. 


<h2 id = "2">2. Threshold Model</h2>

### 2.1 Homogeneous Population

- Coordination game of each node.
- The **threshold** for adopting A is $\theta_A = \frac{b}{a+b}$. If $f_{i, A} > \theta_A$, choose A; Otherwise, choose B. 

#### Complete/Incomplete cascade. 

- What can be done to push the adoption, or even to the complete cascade? 
    - Increase the payoff of X. 
    - Target well selected other individuals to convince to switch.
    - Change the structure of the network, get well chosen pairs of individuals to meet. 

#### Cascade and Community

- Tightly knit communities act as barrier to diffusion

- The condition for node i in community c to adopt an innovation with threshold $\theta$ is: $f_{i, X}=\frac{k_{i, X}}{k_{i}}>\theta_{X}$. 
    - Notations: $k_{i, X}$ is the number of neighbors of node i that adopted X. $k_i$ is the number of neighbors of node i. 

- $\frac{k_{i, c}}{k_{i}}<1-\theta_{X}$
    - For a node i in a community c to adopt an innovation with threshold $\theta$, its fraction of neighbors in c must be lower than $1-\theta$. 
    - For an innovation with threshold $\theta$ to enter a community, at least one member of the community must have its fraction of neighbors in the community lower than $1-\theta$. ($\rho < 1 - \theta$)

- Define density $\rho$ as: each node in the set has at least a $\rho$ fraction of its neighbors in the set. 

- High density clusters are the onlyobstacles to cascades. 

- Local bridges offer the opportunity to learn about new things, to spread information

&nbsp;

---

[Back to top](#12)