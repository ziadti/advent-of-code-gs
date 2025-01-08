**[Day 22: Monkey Market](https://adventofcode.com/2024/day/22)**

_(Input expected in A:A)_

Part 1

```py
=SUMPRODUCT(
   REDUCE(
      TOCOL(A:A,1),
      ROW(1:2000),LAMBDA(s,_,LET(
        F,LAMBDA(x,y,MOD(BITXOR(x,y),2^24)),
        a,F(s,s*64),
        b,F(a,INT(a/32)),
        F(b,b*2048)))))
```
