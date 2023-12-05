# Part 1 & 2

```
=ARRAYFORMULA(
   BYCOL(
     MAP(A:A,LAMBDA(a,
       LET(s,SPLIT(REGEXREPLACE(a,"(\d+) "&{"r";"g";"b"}&"|.","$1 ")," "),
          {ROW(a)*AND(s<={12;13;14}),
           PRODUCT(BYROW(s,LAMBDA(r,MAX(r))))}))),
     LAMBDA(c,SUM(c))))
```
