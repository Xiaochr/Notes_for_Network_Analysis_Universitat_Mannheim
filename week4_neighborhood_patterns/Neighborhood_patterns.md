[Back to menu](/README.md)

<h1 id = "4">Neighborhood Patterns</h1>

## Riciprocity

- Measures the frequency of loops of length 2 in directed networks. 
- Intuition: how likely a vertex that you point towards, points back to you. 
- Computation: 

    $$R = \frac{1}{m} Tr\mathbf{A}^2$$

    - m: the total number of edges

## Transitivity

The phenomenon by which two nodes who are neighbors of the same node, become connected themselves is called **triadic closure**; The resulting “triangle” structure is called *closed triad*. 

- A common principle in social network analysis:
    - If two people in  a social network have a friend in common, then there is an increased likelihood that they will become friends themselves at some point in the future

### Clustering Coefficient

Clustering coefficient is a measure used to quantify transitivity in a network / to measure the prevalence of triadic closure. 

#### 1. Global Clustering Coefficient

$$C = \frac{the\ number\ of\ closed\ paths\ of\ length\ 2}{the\ number\ of\ paths\ of\ length\ 2}\\ = \frac{6 \times the\ number\ of\ triangles}{the\ number\ of\ paths\ of\ length\ 2}$$

- In directed situation, pay attention to the direction! 

#### 2. Local Clustering Coefficient

$$C_i = \frac{the\ number\ of\ pairs\ of\ neighbors\ of\ i\ that\ are\ connected}{the\ number\ of\ pairs\ of\ neighbors\ of\ i}$$

- You can see the example in the slides p11 to have a better understanding. 
- $the\ number\ of\ pairs\ of\ neighbors\ of\ i = \frac{k_i(k_i - 1)}{2}$
- Nodes with high local clustering coefficient have neighbors which are themselves neighbors. 
- **High** local clustering coefficient, more likely **low** betweenness centrality. Because the neighbors are linked to each other, short cuts, no need to go through A. 

#### 3. Average Local Clustering Coefficient

$$C_{avg} = \frac{1}{n} \Sigma_i C_i \\ = \frac{1}{n} \Sigma_i \frac{number\ of\ triangles\ of\ i}{k_i(k_i - 1)/2}$$

- Triangle就算一个，不用方向

### Edge Embeddedness and Neighborhood Overlap

- **Edge embeddedness** is the number of triangles the edge is part of. 
    - $emb(AB)$
- **Neighborhood overlap** is the ratio of common neighbors out of the total set of neighbors. 
    - $n_overlap(AB)$
- Nodes with many edges with high embeddedness tend to have relatively high clustering coefficient.
- Pros and cons of high embeddedness: 
    - Pros: potentially trusted relations
    - Cons: redundant relations, no control over information flow (due to high local clustering coefficient)

### Local Bridges and Structural Holes

- Edges with embeddedness zeroare called **local bridges**.
    - Their removal would make it significantly harder for the neighbors of the endpoints to reach each other. 
- The regions of the graph around local bridges are called **structural holes**. 

### The Strength of Weak Ties Theory

- Results: 
    - Many people learnt about new job opportunities from personal contacts. 
    - These personal contacts were often described as acquaintances rather than close friends. 

&nbsp;

---

[Back to top](#4)