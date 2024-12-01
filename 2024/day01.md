**[Day 1: Historian Hysteria](https://adventofcode.com/2024/day/1)**

_(Input expected in A1)_

**Part 1 & 2**

```py
=INDEX(LET(x,BYCOL(
   SPLIT(TOCOL(SPLIT(SUBSTITUTE(A1," ","~"),CHAR(10))),"~"),
   LAMBDA(c,SORT(c))),{
     SUM(ABS(MMULT(x,{-1;1})));
     SUM(INDEX(x,,1)*COUNTIF(INDEX(x,,2),INDEX(x,,1)))})
```
