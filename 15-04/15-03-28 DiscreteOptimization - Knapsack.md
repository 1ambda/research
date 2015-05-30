


### Greedy Algorithm Overview

- For one problem, there are many possiable greedy algorithm. Some will do better than others depends on the input

- Advantages: quick to design and implement. can be very fast

- Problem: No quality guarantees in general.

### Optimization Models

- Choose some **decision variables** which encode the result we are interested in

- Express the **problem constraints** in terms of these variables. They specify what the solutions to the problem are

- Express the **objective function**

Then, maximize objective function which subject to *decision variables* and *problem constraints*

### Dynamic Programming

According to Bellman Equations,

- O(k, j) = max(O(k, j-1),
                v_j + O(k-w_j, j-1) if w_j <= k)


- complexity: time to fill the table, `O(K n)`

We need log(K) bits to represent `K` on a computer. Hence the algorithm is in fact exponential. (pseudo-polynomial), efficient when `K` is small

### Branch and Bound

- **branching:** split the problem into a number of subproblems like in exhaustive search

- **bounding:** find an *optimistic estimate* of the best solution to the subproblem. maximization( upperbound), minimization(lower bound)

How to find this optimistic estimate? Use **relaxtion!**. Optimization is the art of relaxation.

convert `x_i in {0, 1}` into `0 <= x_i <= 1`. This is called the linear relaxation. We relax the integrality requirement.

Now,

- select most valuable items with least weights while the capacity is not exhausted.
- select a fraction of the last item

If you have good relaxing, the computing job that you will have to do, the search space that you will explore, is going to be much smaller

### Search Strategies

- **depth-first:** prunes when a node estimation is worse than the best found solution.
- **best-first:** select the node with the best estimation

If you really good evaluation (estimation), you can select minimum nodes.

<br/>

- **least-discrepancy:** trust a greedy heuristic

Assume that a good heuristic is available

- It makes very few mistakes
- The search tree is binary
- Following the heuristic means branching left
- Branching right means the heuristic was wrong

**Limited Discrepancy Search(LDS)**

- avoid mistakes
- explore the search space in increasing order of mistakes
- trusting the heuristic less and less (LDS waves)

Depending upon the way you would implement this search, There will be an interesting trade off between space and time,

### Sumamry

a releaxation and search match made in discrete optimization heaven

- Quality based soution approach: CP, DP, MIP
- Scalability based solution approache: LS

(1) Constraint Programming (CP)

- like solving puzzles
- lots of logic / discrete mathematics

(2) Mixed Integer Programming (MIP)

- grounded in linear algebra
- lots of continuous mathematics

(3) Local Search (LS)

- intuition based, most significant coding
- writing efficient code really helps
- lots of staring in the terminal
