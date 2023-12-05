_Input expected in A:A_

# Part 1 & 2

```cpp
=ARRAYFORMULA(
   BYCOL(
     MAP(A:A,LAMBDA(a,
       LET(s,SPLIT(REGEXREPLACE(a,"(\d+) "&{"r";"g";"b"}&"|.","$1 ")," "),
          {ROW(a)*AND(s<={12;13;14}),
           PRODUCT(BYROW(s,LAMBDA(r,MAX(r))))}))),
     LAMBDA(c,SUM(c))))
```
