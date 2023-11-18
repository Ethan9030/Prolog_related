# Prolog proofs (& other tasks) as Graph search

Most AI tasks reduce to searching for goals in a graph structure 

**Search space** is a graph, with partial solutions or states as **nodes** and possible transitions as **arcs** 

• search space may contain cycles 

• often approximated by a tree: easier algorithm, requires less memory, but is less efficient because of repetitions 

• or can add loop detection by keeping a list of visited nodes 

• In general transitions may have costs associated with them (not on this unit) 



Different search strategies can be modelled with the notion of an **agenda** 



## Depth-First search

• agenda = stack (last-in first-out) 

• incomplete: may get trapped in infinite branch

• no shortest-path property 

• requires O(B x n) memory  





## Breadth-First search

• agenda = queue (first-in first-out) 

• complete: will find all solutions 

• first solution found along shortest path 

• requires O(B^n ) memory 





## Iterative Deepening search 

• Combines good features of bfs and dfs 

• Optimality of bfs + Memory footprint of dfs 

• Repeats work, but works well in practice 

• (in a binary tree, half the nodes are in the leaves!) 

![Iterative Deepening search](https://github.com/Ethan9030/Prolog_related/assets/78483249/72515cce-47b3-4671-8f1f-4cc5051cdc6b)




## Best-first search 

https://www.geeksforgeeks.org/best-first-search-informed-search/

The idea of **Best First Search** is to use an evaluation function to decide which adjacent is most promising and then explore. 





• agenda = priority queue (preferentially ordered ) 

• Behaviour depends on heuristic employed 

• Certain guarantees may be obtained if the metric satisfies certain properties (e.g. as in A* search) 





## A* Search Algorithm

https://www.geeksforgeeks.org/a-search-algorithm/

An “A” algorithm is a best-first search algorithm that aims at minimising the total cost along a path from start to goal. 



## Path Finding Live Demo

https://cs.stanford.edu/people/abisee/tutorial/astar.html
