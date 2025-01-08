**[Day 25: Code Chronicle](https://adventofcode.com/2024/day/25)**

_(Input expected in A1)_

```py
=SUMPRODUCT(LET(
   n,CHAR(10),
   s,TOCOL(SPLIT(A1,n&n,)),
   F,LAMBDA(c,MAP(FILTER(s,LEFT(s)=c),
       LAMBDA(x,JOIN(",",BYROW(
         MID(SPLIT(x,n),ROW(1:7),1),
         LAMBDA(r,COUNTIF(r,"#"))))))),
   l,F("#"),k,F("."),
   MAP(l,LAMBDA(a,
     MAP(TOROW(k),LAMBDA(b,
       AND(SPLIT(a,",")+SPLIT(b,",")<8)))))))
```
