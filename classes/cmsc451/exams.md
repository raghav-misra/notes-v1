# 	cmsc451; exam01

## Graphs and DFS

**In a graph:** # of edges is $0 \leq m \leq \binom{n}{2}$. Sum of degrees is $2m$.

**In a digraph:** # of edges is $0 \leq m \leq n^2$. Sum of degrees is $m$.

**DFS**. When you visit a node, immediately visit all its neighbors.

- **Discovery time** $d[u]$ indicates when node `u` was discovered; when first reached. **Finish time** $f[u]$ indicates when node `u` has finished processing; when it and all its neighbors have been finished. **Predecessor pointer** $p[u]$ indicates the node which discovered $u$.

  **Parenthesis Lemma:**

  - $u$ is a descendant of $v$ $\Leftrightarrow$ $[d[u], f[u]] \sube [d[v], d[v]]$.
  - $u$ is an ancestor of $v$ $\Leftrightarrow$ $[d[u], f[u]] \supe [d[v], f[v]]$.
  - $u$ and $v$ are unrelated $\Leftrightarrow$ $[d[u], f[u]] \cap [d[v], f[v]] = \emptyset$.

  Types of edges. **Tree edges** compose the actual search truee.

  - *Directed:* **Back** ($v$ is some ancestor of $u$). **Forward** ($v$ is non-child descendant of $u$ in tree). **Cross** (no relationship.)
  - *Undirected:* All **Back** (would make cycle.)

## Cycles and Strong Components

**DAG** is directed graph, no cycles. **Topo Sort** (DFS adaptation) orders nodes such that for all edges $(u, v)$, $u$ will come before $v$ in the order.

**Cycle Testing.** Just run DFS, if you find node already seen, then cycle! If a digraph has a **back edge** then it has cycle.

*Digraph* is **strongly connected** if all nodes can reach each other. Algorithm for finding *strongly connected components*:

- Find $G^R$ (reversed edges). Run DFS on $G^R$ and label $u$ with $f[u]$.
- Sort nodes by decreasing order of finish times. Run DFS on $G$ in this order of nodes. DFS trees are our strong components.

## Dijkstra and Bellman-Ford

**Dijkstra's** is a greedy algo for single-source SP. Predecessor links allow us to trace some node back to the source, forming the path.

- $s$ is source. Initialize $d[s] = 0$ $d[u] = \infty, \forall u \neq s$. Keep picking unpicked node $u$ with smallest $d[u]$. Discover neighbors of $u$ and see if new SP If so, set $d$-value and mark $u$ as its predecessor.
- $O(n \log n + m)$.

**Bellman-Ford**. Look at every node and adjust SP for neighbors if needed. Do this $n - 1$ times (across all nodes) for $n$ vertices. $o(mn)$.

*Dijkstra's* does not work for negative edges; *Bellman-Ford* does.

## Greedy Scheduling

**Scheduling.** *EFF* is optimal. Others, *ESF*, *SDF*, aren't.

- **Proof of EFF optimality:** Let $O$ be optimal. Let $G$ be *EFF* result. $O$ must have at least as many intervals as $G$. Consider first $i$ where $O_i \neq G_i$. We know $G_i$ does not conflict with any earlier request, so we replace $O_i$ with $G_i$. Clearly, schedule is still valid and optimal. This can be done repeated and we entirely make $O$ into $G$, so both are maximal.

**Partitioning.** Two overlapping intervals have different colors. $O(n^2)$.

- **Algo.** Sort them by start, inc. New request is assigned to smallest color which doesn't overlap. **Proof.** *Feasibility* is obvious as no overlap ever occurs. *Optimality:* 

  Let $\text{depth}(t)$ be number of requests at time $t$. For a $d$-coloring, $d \geq \max_{t} \text{depth}(t)$. WTS: greedy colors $\leq \max_t \text{depth}(t)$.

  Assume contradiction. At some $t_i$, $G$ uses $> \text{depth}(t_i)$ colors. $t_i$ must be start time of a request. Since it is first violation, we assume $d$ (number of used colors before) is $\leq \max_t \text{depth}(t)$. At $t_i$, we then use a new color, totaling $d + 1$. But then depth also increases so $d + 1 \leq \text{depth}(t_i)$. So contradiction.

## $k$-center and Gonzalez's

**$k$-center**. Compute the $k$ "centers" which minimize *max Euclidean distance* from one of the points to its closest center. Equivalently, find the minimum radius $\Delta$ and $k$ balls with radius $\Delta$ so all points lie within the balls. *NP-Hard!*

**Gonzalez's.** Select any point to be initial center $g_1$. We then let $g_2$ be the point farthest from $g_1$. Then $g_3$ is farthest from any center, so on...

- The maximum distance will always decrease as points are added.
- If $G$ is Gonzalez and $O$ is optimal, then $\Delta_G \leq 2 \Delta_O$.

## Greedy Approx: Set Cover

**Set Cover Problem.** $(X, S)$ where $X$ points and $S$ cover sets. We assume $x \in X$ appears in at least one $s \in S$. Find min # of covers from $S$ to cover all points in $X$. *NP-Hard!*

**Greedy Set Cover.** At every point, pick the set in $S$ which covers the most currently uncovered points in $X$. Bound is $G \leq O \cdot \ln |X|$.

## DP: Weighted Interval Scheduling

**WIS.** I know this already. Just know when you formulate, use `prior` to skip all overlapping schedules. Goes from right-to-left:
$$
W(i) = \begin{cases}
	0 &\text{if } i = 0, \\
	\max\{W(i - 1), v_i + W(\text{prior(i)})\}
		&\text{else.}
\end{cases}
$$

## DP: Chain Matrix Multiplication

**Chain Matrix Multiplication.** Matrix multiplication is associative. There are cheaper ways to go about the multiplication then. We have $n$ matrices $A_1, \dots, A_n$ to multiply. The dimensions of matrix $A_i$ are $p_{i - 1} \times p_{i}$. Cost of multiplying two consecutive matrices is their product of their dimensions. Following formulation:
$$
M(i, j) = \begin{cases}
0	&\text{if } i = j, \\
\min_{i \leq k \leq j - 1} [\\
	\qquad M(i, k) + M(k + 1, j) \\
	\qquad +\ p_{i - 1} p_k p_j \\],
	&\text{if } i < j.
\end{cases}
$$
## DP: Floyd-Warshall Algorithm

**Floyd-Warshall.** Shortest path between all pairs of nodes. Let `dist` be a $V\times V$ matrix. Let `dist[u][u]` be $0$ for all $u$. `dist[i][j]` is min distance from node $i$ to node $j$.

 ## Network Flows

**Network Flow.** Source $s$, sink $t$, weighted edges represent maximum flow through the edge. Maximum flow from $s$ to $t$?

- **Flow conservation.** Except $s$, $t$, inflow $=$ outflow.
- **Multi-source/multi-sink?** Add super-source, super-sink.
- **Greedy fails** because no way to decrease flow.

**Ford-Fulkerson (FF)**. Select a path and push flow equal to minimum edge.

- **Residual network.** Edges with remaining flow. And back edges with already sent flow. *Repeat until no paths from $s$ to $t$ exist.*

**$s-t$ cut.** Partition of vertices into $X$ and $Y$ where $s \in X$ and $t \in Y$.

- Given any network, flow, and cut, the amount of flow equals the amount of flow across the cut. Furthermore, the amount of flow can't exceed cut **capacity** (sum of edge weights $X$ to $Y$).

**Max-Flow/Min-Cut Theorem.** The following are all equivalent.

- **[1]** $f$ is a max flow in $G$. **[2]** Residual network $G_f$ has no $s-t$ paths. **[3]** $|f| = $ capacity of some cut $(X, Y)$. **Proof below.**
- **[1] to [2]** By contradiction. If $s-t$ paths, flow not maximal.
- **[2] to [3]** No $s-t$ paths. Let $S$ and all vertices reachable from $S$ be $X$. Let remaining vertices (including $T$) be $Y$. Clearly the edges from $X$ to $Y$ have been exhausted, so flow is equal to maximum flow which can be sent across these edges, which is the cut capacity $c(X, Y)$.
- **[3] to [1]** Flow upper bounded by cut capacity, so if it's equal, it can't be greater. Hence maximal.

## Network Flows: Applications

**Circulation**. Let $S$, $D$ be sets of supply, demand nodes. Edges with capacity will exist for various nodes from $S$ to nodes in $D$.

- Demand nodes have positive demand (duh). Supply nodes have negative demand.
- Want feasible circulation. How to send stuff from $S$ to $D$ and match capacity across edges and node demands?
- *Decision problem.* Can it be done or not?
- **Reducible to network flow.** Add super-source (link to $S$ nodes) and super-sink (link to $D$ nodes). Then, find max flow. If max-flow = total demand, *yes*, else *no*.

**With Lower Bounds.** Above only has upper bounds on edges.

- For each edge, we "force the min capacity." Then, remaining flexible capacity is $\text{upper} - \text{lower}$.
- For the node pushing flow, we decrease demand by $\text{lower}$.
- For the node receiving it, we increase demand by $\text{lower}$.

**Survey Design.** We sell $k$ products. Want to survey $n$ customers. Tailor the survey to customers based on products they have bought. 

- $i$th customer has tolerance for $[c_i^-, c_i^+]$ questions.
- $j$th product needs surveying by $[p_j^-, p_j^+]$ customers.
- *Bipartite graph: sets of customers and products.*
- Edge $(i, j)$ with bounds $[0, 1]$ between customer $i$ who bought product $j$.
- Super source $s$ and sink $t$. Edge $(s, i)$ for any customer $i$ should have bounds $[c_i^-, c_i^+]$. Edge $(j, t)$ for any product $j$ should have bounds $[p_j^-, p_j^+]$.

## P/NP: Definitions

**P.** Problems solvable in poly time. **NP.** Solutions can be verified in poly time. (Certificate + verification algo.)

- Problem $X$ is **NP-Hard** if any problem $Y$ in NP can be reduced to problem $X$; $X$ need not be in $NP$.
- Problem $X$ is **NP-complete** if it is NP-hard AND in NP.

**Reduction.** Devise an algorithm (polynomial time) which takes instance $x$ of problem $X$ and *reduces* it to instance $y$ of problem $Y$. Then $X \leq_P Y$ if the following can be proved.
$$
x \text{ solves } X \text{ iff } y \text{ solves }Y.
$$

## P/NP: Problems

**Cook's Theorem.** SAT is NP-complete. 

The following problems are all NP-complete.

**SAT.** Can we assign values to some Boolean variable expression (with ANDs and ORs and NOTs) such that it evaluates to true?

**IS. **Does a $k$-set of non-adjacent vertices exist?

**Clique.** Does a $k$-set of completely connected vertices exist?

**VC.** Does $k$-set of vertices to which all edges are incident exist?

**DS.** Does a $k$-set of vertices s.t. all vertices are in or adjacent to a vertex in the set exist?

**(D)HC.** $G$ has a cycle which visits all nodes once.

## Approximations

Some hard problems can be approximated to varying degrees. Constant or polynomial factor, PTAS of $\epsilon$, or inapproximable.

**VC. Approx.** (Greedy, like set cover, yields $\ln n$ factor.) 

- **Matching** is an edge set that hits every vertex.
- *Maximal matching* is not a subset of any other matching.
- $M$ is maximal matching; $V^*$ is optimal vertex cover.
- Then, $|M| \leq V^* \leq 2|M|$. All endpoints of make a VC.
- *Algorithm.* Construct $M$. (Repeatedly pick an edge, add it, and then discard all edges incident to its endpoints.) Then pick all endpoints, yielding  VC of at most $2|M|$. 

**Approximation factors not preserved by reductions.**

**TSP.** Given a set $P$ of $n$ points, find the minimum-weight cycle which visits all $n$ points in $P$.

- **Factor-2 Approx.** *If you remove one edge from a TSP tour, you get a spanning tree.* We say the **twice-around tour** walks around the MST of the graph. Shortcut by skipping repeated vertices. **Proof.** Walking around the tree is at most $2\times$ the total MST weight. MST total weight $\leq$ optimal TSP total weight. Bounding between $1$ and $2$ times means $\leq 2\times$.
- **Christofides ($1.5\times$).** *Handshake Lemma* states every graph has even number of odd-degree nodes. We match these nodes together such that we can cut out parts of our MST walk. *Minimum-weight matching* can be found in poly time, and we use this on our MST for odd-degree vertices.

