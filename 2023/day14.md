_Input expected in A:A_

_https://adventofcode.com/2023/day/14_

# Part 1

```py
=ARRAYFORMULA(
   LET(a,A:A,
       G,LAMBDA(arr,se,LET(s,INDEX(se,,1),e,INDEX(se,,2),CHOOSEROWS(arr,SEQUENCE(e-s+1,1,s)))),
       TILT,LAMBDA(arr,
              SUMPRODUCT(
                BYROW(
                  BYCOL(arr,
                    LAMBDA(col,
                      IF(COUNTIF(col,"Z")=0,
                         SORT(col),
                         LET(idxs,FILTER(SEQUENCE(ROWS(col)),col="Z"),
                             rgs,{"1,"&SINGLE(idxs);
                                  QUERY(1+idxs&","&QUERY(idxs,"offset 1",),"limit "&ROWS(idxs)-1);
                                  INDEX(idxs,ROWS(idxs))+1&","&ROWS(col)},
                             REDUCE(TOCOL(,1),rgs,
                               LAMBDA(a,i,VSTACK(a,TOCOL(SORT(G(col,SPLIT(i,","))),2)))))))),
                  LAMBDA(row,COUNTIF(row,"O"))),
                ROWS(arr)-SEQUENCE(ROWS(arr))+1)),
       sp,REGEXEXTRACT(a,REPT("(.)",LEN(a))),
       sps,SWITCH(sp,"#","Z",".","Y",sp),
       TILT(sps)))
```
