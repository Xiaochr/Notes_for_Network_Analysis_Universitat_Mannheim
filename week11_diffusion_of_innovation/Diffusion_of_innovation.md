[Back to menu](/README.md)

<h1 id = "11">Diffusion of Innovation</h1>

## Content

- [Spreading Processes over Networks](#1)
- [Diffusion of Innovation](#2)

<h2 id = "1">Spreading Processes over Networks</h2>

- **Diffusion**: The behavior starts with a handful of initial adopters and then spreads through the network. 

- In networks, the **reach** of diffusion/contagion is determined by: 
    - Global structure
        - Network components
    - Local decisions
        - Immunity of some nodes
        - Links that fail to transmit

### Random Graphs’ Tolerance to Random Failure

- In the $G(n, p)$ model, a giant component exists only if the average node degree $c = (n - 1)p > 1$

- Denote by $\Phi$ the fraction of nodes that function well. Denote by $f$ the fraction of links that work. 

- The new average degree: 

$$c' = (n - 1)\Phi pf, \quad c' = cpf$$

- For a giant component to exist in the remaining network, $c'$ must be larger than 1. That is, $\Phi f > \frac{1}{c}$. 

- One must remove more than $1 - \Phi$ nodes and $1 - f$ links such that $\Phi f < \frac{1}{c}$ for the giant component to break up. 
    - *Robust against random failure*. $G(n, p)$ graphs with $c > 2$ tolerate the removal of about half of the nodes while maintaining the giant component. 

### Tolerance to Random Failure in Power Law Networks 

- No matter how many nodes are removed uniformly at random, the majority of the remaining nodes will be connected in a giant component! 

- Power-law networks are highly robust and can tolerate the uniform random removal of any amount of nodes
    - Good: by attacking random internet servers, the overall structure of the internet will not be affected and enough connectivity will remain for it to work for the remaining computers
    - Bad: To prevent epidemics, almost the entire population must be immune. Even if some random people refuse spreading rumors, the rumors will spread. 

- Removal of nodes with highest degree
    - In $G(n, p)$ random networks, removal of high-degree nodes **does not** produce different effects than uniform random removal. 
    - But in power law networks with $\alpha \in [2, 3]$, removal of highest degree nodes is **highly destructive**. 

- Power law networks are: 
    - Very robust to random failure of nodes
    - Very fragile to attacks that target the highest-degree nodes

---

<h2 id = "2">Diffusion of Innovation</h2>

### Bass Model

$$F(t+1)=F(t)+P(1-F(t))+Q(1-F(t)) F(t)$$

- $F(t)$: the fraction of population who have adopted by time t. 
- P: the rate of spontaneous adoption due to external factors. 
- Q: the rate of imitation of adoption. 
- Calculating procedure: 
    - $F(t+1)-F(t)=(P+Q F(t))(1-F(t))$
    - $\frac{d F(t)}{d t}=(P+Q F(t))(1-F(t))$
    - $F(t)=\frac{1-e^{-(P+Q) t}}{1+\frac{Q}{P} e^{-(P+Q) t}}$
- The cumulative adoption curve is **S shape** when $Q > P$
- When $Q > P$, it's a concave curve. 

&nbsp;

---

[Back to top](#11)