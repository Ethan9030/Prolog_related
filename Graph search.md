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

Video:https://www.youtube.com/watch?v=dv1m3L6QXWs

Words:https://www.geeksforgeeks.org/best-first-search-informed-search/

The idea of **Best First Search** is to use an evaluation function to decide which adjacent is most promising and then explore. 

```
// Pseudocode for Best First Search
Best-First-Search(Graph g, Node start)
    1) Create an empty PriorityQueue
       PriorityQueue pq;
    2) Insert "start" in pq.
       pq.insert(start)
    3) Until PriorityQueue is empty
          u = PriorityQueue.DeleteMin
          If u is the goal
             Exit
          Else
             Foreach neighbor v of u
                If v "Unvisited"
                    Mark v "Visited"                    
                    pq.insert(v)
             Mark u "Examined"                    
End procedure
```



• agenda = priority queue (preferentially ordered ) 

• Behaviour depends on heuristic employed 

• Certain guarantees may be obtained if the metric satisfies certain properties (e.g. as in A* search) 





## A* Search Algorithm

https://www.geeksforgeeks.org/a-search-algorithm/

**Algorithm** 
We create two lists – Open List and Closed List (just like Dijkstra Algorithm)  

```
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)
```

So suppose as in the below figure if we want to reach the target cell from the source cell, then the A* Search algorithm would follow path as shown below. Note that the below figure is made by considering Euclidean Distance as a heuristics.

![A_Star_Search](https://media.geeksforgeeks.org/wp-content/uploads/a_-search-algorithm-2.png)

**Heuristics** 
We can calculate **g** but how to calculate h ?
We can do things. 
A) Either calculate the exact value of h (which is certainly time consuming). 
             OR 
B ) Approximate the value of h using some heuristics (less time consuming).
We will discuss both of the methods.
A) **Exact Heuristics** –
We can find exact values of h, but that is generally very time consuming.
Below are some of the methods to calculate the exact value of h.
1) Pre-compute the distance between each pair of cells before running the A* Search Algorithm.
2) If there are no blocked cells/obstacles then we can just find the exact value of h without any pre-computation using the [distance formula/Euclidean Distance](https://en.wikipedia.org/wiki/Euclidean_distance)

**B) Approximation Heuristics –** 
There are generally three approximation heuristics to calculate h –

**1) Manhattan Distance –**  

- It is nothing but the sum of absolute values of differences in the goal’s x and y coordinates and the current cell’s x and y coordinates respectively, i.e.,

```
 h = abs (current_cell.x – goal.x) + 
     abs (current_cell.y – goal.y)
```

- When to use this heuristic? – When we are allowed to move only in four directions only (right, left, top, bottom)

The Manhattan Distance Heuristics is shown by the below figure (assume red spot as source cell and green spot as target cell). 

![Manhattan_Heuristics](https://media.geeksforgeeks.org/wp-content/uploads/a_-search-algorithm-3.png)

**2) Diagonal Distance-** 

- It is nothing but the maximum of absolute values of differences in the goal’s x and y coordinates and the current cell’s x and y coordinates respectively, i.e.,

```
dx = abs(current_cell.x – goal.x)
dy = abs(current_cell.y – goal.y)
 
h = D * (dx + dy) + (D2 - 2 * D) * min(dx, dy)

where D is length of each node(usually = 1) and D2 is diagonal distance between each node (usually = sqrt(2) ). 
```

- When to use this heuristic? – When we are allowed to move in eight directions only (similar to a move of a King in Chess)

The Diagonal Distance Heuristics is shown by the below figure (assume red spot as source cell and green spot as target cell).

![Diagonal_Heuristics](https://media.geeksforgeeks.org/wp-content/uploads/a_-search-algorithm-4.png)

**3) Euclidean Distance-**

- As it is clear from its name, it is nothing but the distance between the current cell and the goal cell using the distance formula

```
 h = sqrt ( (current_cell.x – goal.x)2 + 
            (current_cell.y – goal.y)2 )
```

- When to use this heuristic? – When we are allowed to move in any directions.

The Euclidean Distance Heuristics is shown by the below figure (assume red spot as source cell and green spot as target cell).

![Euclidean_Heuristics](https://media.geeksforgeeks.org/wp-content/uploads/a_-search-algorithm-5.png)

**Relation (Similarity and Differences) with other algorithms-** 
Dijkstra is a special case of A* Search Algorithm, where h = 0 for all nodes.

**Implementation** 
We can use any data structure to implement open list and closed list but for best performance, we use a **set** data structure of C++ STL(implemented as Red-Black Tree) and a boolean hash table for a closed list.
The implementations are similar to Dijkstra’s algorithm. If we use a Fibonacci heap to implement the open list instead of a binary heap/self-balancing tree, then the performance will become better (as Fibonacci heap takes O(1) average time to insert into open list and to decrease key)

Also to reduce the time taken to calculate g, we will use dynamic programming. 

## Path Finding Live Demo

https://cs.stanford.edu/people/abisee/tutorial/astar.html










