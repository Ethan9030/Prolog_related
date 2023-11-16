# The Cut & Negation

Automatic backtracking is one of the most characteristic features of Prolog. But backtracking can lead to inefficiency. Sometimes Prolog can waste time exploring possibilities that lead nowhere. It would be pleasant to have some control over this aspect of its behavior

====> Just control how Prolog look for solutions



P.S. 这里说一下back tracking


![backtracking](https://github.com/Ethan9030/Prolog_related/assets/78483249/4ba8ea42-3ed7-476c-8b56-34271473d4d2)

Suppose A to G are some rules and facts. We start from A and want to reach G. The proper path will be A-C-G, but at first, it will go from A to B, then B to D. When it finds that D is not the destination, it backtracks to B, then go to E, and backtracks again to B, as there is no other child of B, then it backtracks to A, thus it searches for G, and finally found G in the path A-C-G. (Dashed lines are indicating the backtracking.) So when it finds G, it stops.

## Cut: Prevent backtracking    "!"

```
f (X,0) :- X < 3, !. % Rule 1

f (X,2) :- 3 =< X, X < 6, !. % Rule 2

f (X,4) :- 6 =< X. % Rule 3
```

?- f (1,Y), 2 < Y. 

Prolog choose rule 1 since 1 < 3 and fails the goal 2 < Y fails. Prolog will try to backtrack, but not beyond the point marked ! In the program, rule 2 and rule 3 will not be generated. 

**Output**:

```
| ?- [backtrack].
   1 1 Call: [backtrack] ?
compiling D:/TP Prolog/Sample_Codes/backtrack.pl for byte code...
D:/TP Prolog/Sample_Codes/backtrack.pl compiled, 10 lines read - 1373 bytes written, 15 ms
   1 1 Exit: [backtrack] ?
(16 ms) yes
{trace}
| ?- f(1,Y), 2<Y.
   1 1 Call: f(1,_23) ?
   2 2 Call: 1<3 ?
   2 2 Exit: 1<3 ?
   1 1 Exit: f(1,0) ?
   3 1 Call: 2<0 ?
   3 1 Fail: 2<0 ?
no
{trace}
| ?-
```



## Negation: as Failure   "  \ +  "

Perform failure when condition does not satisfy 

Suppose we have a statement, “Mary likes all animals but snakes”, we will express this in Prolog. 

expressed as  ===> 

- If X is snake, then “Mary likes X” is not true
- Otherwise if X is an animal, then Mary likes X.

```
likes(mary,X) :- snake(X), !, fail.

likes(mary, X) :- animal(X).
```

The ‘fail’ statement causes the failure. 
