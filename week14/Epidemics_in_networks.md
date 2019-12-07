[Back to menu](/README.md)

<h1 id = "14">Epidemics in Networks</h1>

## Content
- [The SI Model](#1)
- [The SIR Model](#2)
- [The SIS Model](#3)

<h2 id = "1">1. The SI Model</h2>

### 1.1 Basic

- Only consider 2 states: susceptible and infected. 

- Notations: 
    - The spread chance $\beta$
    - The size of population $n$
    - The number of infected $X$, the fraction of infected $x$
    - The susceptible $S$

$$x(t+1)=x(t)+\beta s x$$
$$s(t+1)=s(t)-\beta s x$$
$$s(t)+x(t)=s(t+1)+x(t+1)=1$$

- Solve the equations, we get: $x(t)=\frac{x_{0} e^{\beta t}}{1-x_{0}+x_{0} e^{\beta t}}$

### 1.2 Networked

$$x_{i}(t+1)=x_{i}(t)+\beta s_{i}(t) \sum_{j} A_{i j} x_{j}(t)$$

$$s_{i}(t+1)=s_{i}(t)-\beta s_{i}(t) \sum_{j} A_{i j} x_{j}(t)$$

$$x_{i}(t+1)+s_{i}(t+1)=x_{i}(t)+s_{i}(t)=1$$

- $\frac{d x_{i}}{d t}=\beta\left(1-x_{i}\right) \sum_{j} A_{i j} x_{j}=\beta \sum_{j} A_{i j} x_{j}+\beta \sum_{j} A_{i j} x_{i} x_{j}$
    - Not solvable in closed form!
    - Consider large $n$ and small $t$, we can omit $x_ix_j$. So $\frac{d \mathbf{x}}{d t}=\beta \mathbf{A} \mathbf{x}$, the approximate solution is $\mathbf{x}(t)=\sim \mathrm{e}^{\beta \lambda_{1} t} \mathbf{v}_{1}$
    - At large t, all vertices reachable from the ones infected at $t_0$ will eventually become infected. 

<h2 id = "2">2. The SIR Model</h2>

- Consider 3 states: susceptible, infected, recovered. 

- Notations:
    - The recover rate $\gamma$

### 2.1 Basic

$$\frac{d s}{d t}=-\beta s x$$
$$\frac{d x}{d t}=\beta s x-\gamma x$$
$$\frac{d r}{d t}=\gamma x$$
$$s+x+r=1$$

- $r \approx 1-e^{-\frac{\beta r}{\gamma}}$
    - When $\beta < \gamma$, the only solution is $r = 0$, hence no epidemic at all. 
    - When $\beta > \gamma$, the equation has an additional solution, and the disease becomes an epidemic. 

### 2.2 Networked

$$\frac{d s_{i}}{d t}=-\beta s_{i} \sum_{j} A_{i j} x_{j}$$

$$\frac{d x_{i}}{d t}=\beta s_{i} \sum_{j} A_{i j} x_{j}-\gamma x_{i}$$

$$\frac{d r_{i}}{d t}=\gamma x_{i}$$

- When $n$ is large and $t$ is small, $s_{i} \rightarrow 1$
    - $\frac{d \mathbf{x}}{d t}=\beta \mathbf{M} \mathbf{x}$, where $\mathbf{M}=\mathbf{A}-\frac{\gamma}{\beta} \mathbf{I}$. 
    - So $\mathbf{x}(t) \sim e^{\left(\beta \lambda_{1}-\gamma\right) t} \mathbf{v}_{1}$. 
    - When $\beta \lambda_{1}-\gamma>0$, the individuals with high values in the principal eigenvector (the individuals with high eigenvector centrality) are likely to get infected first.
    - When $\beta \lambda_{1}-\gamma<0$, the probability of infection decays exponentially and the disease dies out before causing an epidemic.

<h2 id = "3">3. The SIS Model</h2>

- Consider 2 states: susceptible and infected. But allow **reinfection**. 

### 3.1 Basic

$$\frac{d x}{d t}=\beta s x-\gamma x$$

$$\frac{d s}{d t}=\gamma x-\beta s x$$

$$s+x=1$$

- Solve the equation, we get: $x(t)=x_{0} \frac{(\beta-\gamma) e^{(\beta-\gamma) t}}{\beta-\gamma+\beta x_{0} e^{(\beta-\gamma) t}}$
    - If $\beta>\gamma$, the growth curve is similar in shape to the SI model, but never reaches 1. the system finds a stable state where a steady fraction of the population is always infected: $x=\frac{\beta-\gamma}{\beta}$, called *endemic disease state*. 
    - If $\beta < \gamma$, The disease dies out, there is no epidemic. 

### 3.2 Networked

$$\frac{d s_{i}}{d t}=-\beta s_{i} \sum_{j} A_{i j} x_{j}+\gamma x_{i}$$

$$\frac{d x_{i}}{d t}=\beta s_{i} \sum_{j} A_{i j} x_{j}-\gamma x_{i}$$

- When $n$ is large and $t$ is small, the same as SIR, $\mathbf{x}(t) \sim e^{\left(\beta \lambda_{1}-\gamma\right) t} \mathbf{v}_{1}$. 

- At late time
    - If $\frac{\beta}{\gamma}<\frac{1}{\lambda_{1}}$, the disease was under epidemic threshold to start with. 
    - If $\frac{\beta}{\gamma}>\frac{1}{\lambda_{1}}$, endemic state: $x_{i}=\frac{\beta \sum_{j} A_{i j} x_{j}}{\beta \sum_{j} A_{i j} x_{j}+\gamma}=\frac{\sum_{j} A_{i j} x_{j}}{\sum_{j} A_{i j} x_{j}+\frac{\gamma}{\beta}}$
        - If $\frac{\beta}{\gamma}$ is very small, all vertices infected all the time. 
        - If $\frac{\beta}{\gamma} \rightarrow \lambda_1$, then $x_{i} \sim \frac{1}{\lambda_{1}} \sum_{j} A_{i j} x_{j}$, x is proportional to the principal eigenvector of A. 

&nbsp;

---

[Back to top](#14)