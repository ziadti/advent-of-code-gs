_Input expected in A:A_

_https://adventofcode.com/2023/day/2_

# Part 1 & 2

```py
=ARRAYFORMULA(
   BYCOL(
     MAP(A:A,LAMBDA(a,
       LET(s,SPLIT(REGEXREPLACE(a,"(\d+) "&{"r";"g";"b"}&"|.","$1 ")," "),
          {ROW(a)*AND(s<={12;13;14}),
           PRODUCT(BYROW(s,LAMBDA(r,MAX(r))))}))),
     LAMBDA(c,SUM(c))))
```
