_Input expected in A:A_

_https://adventofcode.com/2023/day/8_

# Part 1

```py
=REDUCE("AAA",SEQUENCE(25000),
   LAMBDA(a,i,
    IF(a="ZZZ",
       i-1,
       IFNA(
         VLOOKUP(
           a,
           ARRAYFORMULA(SPLIT(A2:A,"=(), ")),
           IF(MID(A1,MOD(i-1,LEN(A1))+1,1)="L",2,3),),
         MIN(a,i-1)))))
```
