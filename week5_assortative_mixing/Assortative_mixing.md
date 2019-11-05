[Back to menu](/README.md)

<h1 id = "5">Assortative Mixing</h1>

- It appears that people have a strong tendency to associate with others whom they perceive as being similar to themselves in some way. In sociology, this tendency has been called **homophily**. 

- **Assortative mixing** refers to the extent to which nodes in a graph tend to have similar characteristics to their neighbors. 

- Assortative mixing accounts for the edges that exist between nodes that have similar characteristics. However, in general, the terms homophilyand assortative mixing are used to account for the edges that exist between nodes that have similar features that are not network dependent. 

## Assortative Mixing by Enumerative Characteristics

$$mixing = m_{same} - m_{same}^{exp}$$

### Computation Steps

1. Compute the fraction of edges that run between vertices of the same type

$$m_{\text {same}}=\frac{\frac{1}{2} \sum_{i j} A_{i j} \delta\left(c_{i}, c_{j}\right)}{m}=\frac{1}{2 m} \sum_{i j} A_{i j} \delta\left(c_{i}, c_{j}\right)$$
- $\delta(c_i, c_j)$ is Kronecker delta. （相等为1，不相等为0）

2. Compute the fraction of edges  that would run between vertices of the same type, if edges were formed at random without regard of vertex types, **but preserving the vertex degree**.

$$m_{\text {same }}^{e x p}=\frac{\frac{1}{2} \sum_{i j} \frac{k_{i} k_{j}}{2 m} \delta\left(c_{i}, c_{j}\right)}{m}=\frac{1}{2 m} \sum_{i j} \frac{k_{i} k_{j}}{2 m} \delta\left(c_{i}, c_{j}\right)$$

3. Compute the mixing

$$\operatorname{mixing}=\frac{1}{2 m} \sum_{i j}\left(A_{i j}-\frac{k_{i} k_{j}}{2 m}\right) \delta\left(c_{i}, c_{j}\right)$$

### Properties

- $-1 \leq mixing \leq 1$

    - Assortive mixing: the mixing is large in absolute value and positive
    - If the mixing is close to 0, then the edges are formed independently of the type
        - $mixing = 0$ when: 
            - All nodes belong to the same class
            - Each node belongs to its unique class
    - Disassortative mixing: the mixing is large in absolute value and negative

- This measure of assortative mixing is not normalized. 

### Normalized

$$\operatorname{mixing}_{\max }=\frac{1}{2 m}\left(2 m-\sum_{i j} \frac{k_{i} k_{j}}{2 m} \delta\left(c_{i}, c_{j}\right)\right)$$
$$\operatorname{mixing}_{n o r m}=\frac{\operatorname{mixing}}{m i x i n g_{\max }}=\frac{\sum_{i j}\left(A_{i j}-\frac{k_{i} k_{j}}{2 m}\right) \delta\left(c_{i}, c_{j}\right)}{2 m-\sum_{i j} \frac{k_{i} k_{j}}{2 m} \delta\left(c_{i}, c_{j}\right)}$$

Sometimes this is called **assortativity coefficient**. 

### Alternative Form

- The previous formula requires knowledge about each individual edge, and the fraction of zero terms (pairs of nodes of different types) is often very large, making computation significantly slow. 

$$mixing = \Sigma_{r \in C} (e_r - a_r^2)$$

- $e_r$ is the fraction of edges that have both ends of type r
    - $e_{r}=\frac{\sum_{i, j \in r} A_{i j}}{2 m}=\frac{\sum_{i \in r} k_{i, r}}{2 m}$
- $a_r$ is the fraction of edge ends of type r
    - $a_r = \frac{\Sigma_{i \in r}k_i}{2m}$

$$mixing_{max} = 1 - \Sigma_{r \in C} a_r^2$$
$$mixing_{norm} = \frac{mixing}{mixing_{max}} = \frac{\Sigma_{r \in C}(e_r - a_r^2)}{1 - \Sigma_{r \in C} a_r^2}$$

## Assortative Mixing by Scalar Values

- Consider each vertex has a scalar feature, for example: age, income, weight, price, etc

### Computation Steps

1. Each edge from node i to j can be written as the pair $(x_i, x_j)$
2. Compute the assortativity coefficient as the **Pearson correlation coefficient** between the vector of values of the first endnode and the vector of values of the second endnode across all edge

$$r_{XY} = \frac{Cov_{XY}}{st\_dev_x st\_dev_y}$$

- In our case the set of value of X is the same as the set of value of Y, since we consider an undirected graph. So $r_{XY} = \frac{cov_{XY}}{var_X}$

- Further computations
    - $\operatorname{var}=\frac{1}{2 m} \sum_{i j} A_{i j}\left(x_{i}-\mu\right)^{2}=\frac{1}{2 m} \sum_{i}\left(x_{i}-\mu\right)^{2} \sum_{j} A_{i j}=\frac{1}{2 m} \sum_{i} k_{i}\left(x_{i}-\mu\right)^{2}$
    - $\operatorname{cov}=\frac{1}{2 m} \sum_{i j} A_{i j}\left(x_{i}-\mu\right)\left(x_{j}-\mu\right)$
    - $\mu=\frac{\sum_{i j} A_{i j} x_{i}}{\sum_{i j} A_{i j}}=\frac{\sum_{i} x_{i} \sum_{j} A_{i j}}{2 m}=\frac{\sum_{i} x_{i} k_{i}}{2 m}$

$$r=\frac{\operatorname{cov}}{v a r}=\frac{\sum_{i j}\left(A_{i j}-\frac{k_{i} k_{j}}{2 m}\right) x_{i} x_{j}}{\sum_{i j}\left(k_{i} \delta_{i j}-\frac{k_{i} k_{j}}{2 m}\right) x_{i} x_{j}}$$

这里没有弄懂……下次要去问下

## Assortative Mixing by Node Degree

It measures to what extent nodes tend to be connected to nodes of similar degree. 

$$r_{\text {degree}}=\frac{\operatorname{cov}}{\operatorname{var}}=\frac{\sum_{i j}\left(A_{i j}-\frac{k_{i} k_{j}}{2 m}\right) k_{i} k_{j}}{\sum_{i j}\left(k_{i} \delta_{i j}-\frac{k_{i} k_{j}}{2 m}\right) k_{i} k_{j}}$$

- **core-periphery structure**: Large degree nodes connect to large degree nodes AND low degree nodes connect to low degree nodes
- **recurring star-shape pattern**: Large degree nodes connect to small degree nodes

&nbsp;

---

[Back to top](#5)