[Back to menu](/README.md)

<h1 id = "10">Growing Random Graphs</h1>

## Content

- [Uniform randomness](#1)
- [The BA Model](#2)

Growing random graphs are models in which new nodes are born over time and form edges to existing nodes when they are born. 

- Model a process that is closer to real world network formation than Poisson models
- Result in networks with richer degree distributions, closer to real network degree distributions

<h2 id = "1">Uniform randomness –a baseline growing model</h2>

A dynamic variation of the Poisson random-graph in which nodes are born over time and form links to randomly selected nodes that already exist

### The Model

- At each time instance, a new node is born
- The newly born node i forms b links to pre-existing nodes
- Each of the b nodes is chosen with equal probability out of the set of pre-existing nodes

### Properties

- Start with $b + 1$ nodes fully connected. (0,...,b) The first new born node we consider is the one born at time $b + 1$. The new node forms b edges. 
- At each time $t > b$, there are t pre-existing nodes, each has the probability of getting a new edge equals to $\frac{b}{t}$. 
    - as time passes and nodes accumulate, each node in the network has a smaller probability of receiving a new edge. 
- Expected degree of node i at time t: 

$$k_{i}^{(t)}=b+\frac{b}{i+1}+\frac{b}{i+2}+\ldots+\frac{b}{t}$$

- Expected number of edges **received** by node i from all subsequent nodes up to time t: 

$$k_{i}^{\prime}(t)=\frac{b}{i+1}+\frac{b}{i+2}+\cdots+\frac{b}{t} \approx b\left(\ln \left(\frac{t}{i}\right)\right)$$

- **Cumulative distribution**: The fraction of the nodes that have an expected number of received edges less than k at time t: 

$$F(k)=\frac{t-t e^{-\frac{k}{b}}}{t}=1-e^{-\frac{k}{b}}$$

- Proof: $b\left(\ln \left(\frac{t}{i}\right)\right)<k$, so $i>t e^{-\frac{k}{b}}$. The total is t, so the fraction is $\frac{t - i_k}{t}$. 

- The $F(k)$ is the cumulative distribution of expected received edges $p_{k}^{\prime}=\frac{1}{b} e^{-\frac{k}{b}}$. 
- So the probability of a node to have total degree of k is: 

$$p_{k}=p_{k-b}^{\prime}=\frac{1}{b} e^{-\frac{k-b}{b}}$$

- The probability decreases rapidly, large nodes are (almost) impossible. 

---

<h2 id = "2">Preferential attachment model of Barabásiand Albert –The BA Model</h2>

### Price's Model

- The pre-existing papers that a new paper cites are chosen at random, with probability proportional to the number of citations those papers already have
- New papers do not have any citations, so to give them a chance of being cited, the probability that a paper receives a new citation is proportional to how many citations it already has, plus a positive constant a. 
- It is the first model whose degree distribution follows a power law: 
    - $p_q \sim q^{-\alpha}$, $\alpha = 2 + \frac{a}{b}$, where q is the in-degree of a vertex. 

### Barabási-Albert model

A model of **undirected** networks, based on a similar intuition as Price’s model

#### The Model

- Nodes are added one by one
- Each newly added node forms exactly b connections to pre-existing nodes
- **Connections are made to vertices proportional to their degree**

#### Properties

- $p_k^{(t)}$ is the fraction of nodes of degree k at time t. 
- There are t pre-existing nodes. The smallest degree in the network is b. 
- There are $tb$ pre-existing edges and $(t + 1)b$ edges in total. 
    - $tb$ is only an approximation when t is large. 
- $(t+1)p_k^{(t)}$ is the total number of nodes with degree k at time t.
- At time t, a pre-existing node of degree k receives an edge with probability $\frac{k}{\sum_{i=0}^{t-1} k_{i}}=\frac{k}{2 t b}$
- The number of nodes with degree k at time t: 
    - The probability that a particular pre-existing node of degree k receives an edge: $b\frac{k}{2tb} = \frac{k}{2t}$. Then the number of pre-existing nodes of degree k that receive an edge: $t p_{k}^{(t-1)} \frac{k}{2 t}=p_{k}^{(t-1)} \frac{k}{2}$. 
    - The number of nodes having degree k at time $t - 1$ and did not receive an edge at time t: $t p_{k}^{(t-1)}-p_{k}^{(t-1)} \frac{k}{2}$. 

- For $k > b$: 

$$(t+1) p_{k}^{(t)}=p_{k-1}^{(t-1)} \frac{k-1}{2}+t p_{k}^{(t-1)}-p_{k}^{(t-1)} \frac{k}{2}$$

- For $k = b$: 

$$(t+1) p_{b}^{(t)}=t p_{b}^{(t-1)}-p_{b}^{(t-1)} \frac{b}{2}+1$$

- We are interested in the stationary degree distribution, $p_{k}^{(t-1)}=p_{k}^{(t)}=p_{k}$
    - For $k > b$:

    $$p_{k}=\frac{k-1}{k+2} p_{k-1}$$

    - For $k = b$: 

    $$p_b = \frac{2}{b + 2}$$

- $p_{k}=\frac{2 b(b+1)}{k(k+1)(k+2)}$, so $p_k \sim k^{-3}$. Hence the BA model generates a degree distribution with a power-law tail that always has an exponent $\alpha = 3$. 

#### Power Law Networks

- Power law degree distribution
- Small-world effect ensured by the large degree nodes
- Low clustering coefficients
- Size of Giant Component: $S=1-p_{0}-L i_{\alpha}(1-S)$
    - $L i_{\alpha}(x)=\sum_{k=1}^{\infty} k^{-\alpha} x^{k}$
    - If $p_0 = 0$, there will always exist a giant component that covers all the nodes because there is no solution to the equation other than $S = 1$

&nbsp;

---

[Back to top](#10)