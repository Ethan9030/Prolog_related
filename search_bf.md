## Grid World <u>Breadth-first search</u>

```search_bf :-
search_bf :-
    my_agent(A),
    get_agent_position(A, P),
    (complete(P) -> true
    ;otherwise   -> search_bf([[P]], [], Path), 
                    agent_do_moves(A, Path)).
```

- `my_agent/1` retrieves the agent.
- `get_agent_position/2` retrieves the initial position of the agent.
- If the current position (`P`) is already complete, the search is done (`true`). Otherwise, it proceeds to the next step.
- It calls `search_bf/3` with the initial state `[[P]]` (a list of a list containing the initial position), an empty visited list, and an unbound variable `Path`.

```
search_bf(Queue, Visited, Path) :-
    Queue = [Next | Rest],  #广度搜索现在的状态
    Next = [Pos | RPath],   #现在的位置和记录的路径
    (complete(Pos) -> reverse([Pos | RPath], [_ | Path])
    ;otherwise     -> (findall([NP, Pos | RPath],
                               (map_adjacent(Pos, NP, empty), 
                               \+ member(NP, Visited), 
                               \+ member([NP | _], Rest)),
                               Newfound),
                      append(Rest, Newfound, NewQueue),
                      search_bf(NewQueue, [Pos | Visited], Path)).
```

- `Queue` represents the current state of the search, where each element is a list `[Pos | RPath]`, indicating the current position `Pos` and the path taken so far `RPath`.
- If the current position `Pos` is already complete, the search is done, and the result is the reversed path from the start to the goal.
- Otherwise, it explores adjacent positions (`NP`) by using `map_adjacent/3` predicate, ensuring `NP` is not in the visited list and is not already in the current search queue.
- The new positions (`Newfound`) are added to the queue (`NewQueue`), and the search continues with the updated queue and visited list.

