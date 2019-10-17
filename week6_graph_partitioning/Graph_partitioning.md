[Back to menu](/README.md)

<h1 id = "6">Graph Partitioning</h1>

## Kernighan-Lin Algorithm

Local search, greedy algorithm. 

Intuition: Start with a random partitioning, Swap pairs of nodes from the two partitions, looking to reduce the cut size

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

### Related definitions

- Internal costs $I_x$ as the number of edges it has to other nodes in its partition. 

- Exeternal costs $E_x$ as the number of edges node x has to nodes in the other partition. 

- Given $x \in V_1, y \in V_2$: 
    - $c u t_{-} \operatorname{size}\left(V_{1}, V_{2}\right)=c u t_{-} \operatorname{size}\left(V_{1}-\{x\}, V_{2}-\{y\}\right)+E_{x}+E_{y}-A_{x y}$
    - After swapping x and y: 
    $c u t_{-} \operatorname{size}(\widehat{V_{1}}, \widehat{V_{2}})=c u t_{-} \operatorname{size}\left(V_{1}-\{x\}, V_{2}-\{y\}\right)+I_{x}+I_{y}+A_{x y}$
    - So the **gain of swapping**: 
    $gain(x \in \widehat{V_{2}}, y \in \widehat{V_{1}}) = c u t_{-} \operatorname{size}\left(V_{1}, V_{2}\right) - c u t_{-} \operatorname{size}(\widehat{V_{1}}, \widehat{V_{2}}) = E_x + E_y - I_x - I_y - 2A_{xy}$

### Algorithm Performance

- Complexity: $O(mn^2)$ done several times
    - $O(n^3)$ on sparse networks
    - $O(n^4)$ on dense networks

This makes the algorithm inapplicable to networks bigger than a couple of thousands of nodes

## Spectral Partitioning

To be finished...




[Back to top](#6)