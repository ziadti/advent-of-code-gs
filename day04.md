# Part 1 & 2

```cpp
=MAP({3,2},LAMBDA(i,
  SUM(INDEX(
    LET(crds,SEQUENCE(ROWS(A:A)),
        REDUCE({crds,crds^0,crds^0-1},
               crds,
               LAMBDA(a,i,LET(s,SPLIT(TOCOL(SPLIT(REGEXEXTRACT(SUBSTITUTE(INDEX(A:A,i)," ","x"),":x(.*)"),"|")),"x"),
                   m,SUM(COUNTIF(INDEX(s,2),INDEX(s,1))),
                   IF(m=0,a,a+IF(COUNTIF(SEQUENCE(m)+i,INDEX(a,,1)),{0,INDEX(a,i,2),2^(m-1)/m})))))),,i))))
```
