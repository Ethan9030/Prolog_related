# List related Operations

## List basic

**[X | Y]**: X绑定为列表的第一个项目的值，我们称之为表头（head）。而Y则绑定为剩下的列表，我们称之为表尾（tail) 

<u>X是列表头(head), 它可以是一个列表，或其他任何数据结构</u>

<u>Y 是列表尾(tail), 它只能可以是一个列表</u>



**最后这个匹配失败非常重要，在递归过程中经常使用它作为边界检测。即只要表不为空，那么它就能与[X|Y]匹配，当表为空时，就不能匹配，表示已经到达的边界条件**



**表可以看作是表头项目与表尾列表组合而成。而表尾列表又是由同样的方式组成的。本质上看就是递归的定义**



code:

```
?- [a|[b|[c|[d|[]]]]] = [a,b,c,d].
yes
```



首先考虑边界条件，在用递归解决问题 =====>  <u>详见下面member,append,reverse的函数怎么写的</u>



## List相关的函数

### Findall: 寻找目标并且放到一个List中

Finding all solutions to a goal

参数1： 结果列表的模板 

参数2： 目标模板 

参数3： 结果列表 



code example:

```
?- findall(X, connect(kitchen, X), L).
L = [office, cellar, ‘dining room’]

?- findall(foodat(X,Y), (location(X,Y) , edible(X)), L).
L = [foodat(apple, kitchen), foodat(crackers, kitchen)]
```



### Member: 可以用于找到List里的所有元素

code:

```
member(X,[X|_]).
member(X,[Y|T]) :- member(X,T).

?- member(X, [apple, broccoli, crackers]).
X = apple ;
X = broccoli ;
X = crackers ;
no
```



### Append: 把两个List变成一个

code:

```
append([],X,X).
append([H|T1],X,[H|T2]) :- append(T1,X,T2).

?- append([a,b,c],[d,e,f],X).
X = [a,b,c,d,e,f]
```



### Reverse: 反转List 

Succeeds if Reversed is the reversed list List 

code:

```
reverse(List, Rev) :-
        reverse(List, Rev, []).

reverse([], L, L).
reverse([H|T], L, SoFar) :-
        reverse(T, L, [H|SoFar]).
        
reverse([1,2,3,4,5], X).
X = [5, 4, 3, 2, 1]
yes.       
```

