**[Day 14: Parabolic Reflector Dish](https://adventofcode.com/2023/day/14)**

_(Input expected in A:A)_

**Part 1**

**First approach: Splitting - Sorting - Merging**

```py
=ARRAYFORMULA(
  LET(in,A:A,
      G,LAMBDA(arr,se,LET(s,INDEX(se,,1),e,INDEX(se,,2),CHOOSEROWS(arr,SEQUENCE(e-s+1,1,s)))),
      TILT,LAMBDA(arr,
             BYCOL(SWITCH(arr,"#","Z",".","Y",arr),
               LAMBDA(col,
                 IF(COUNTIF(col,"Z")=0,
                    SORT(col),
                    LET(idxs,FILTER(SEQUENCE(ROWS(col)),col="Z"),
                        rgs,{"1,"&SINGLE(idxs);
                            QUERY(1+idxs&","&QUERY(idxs,"offset 1",),"limit "&ROWS(idxs)-1);
                            INDEX(idxs,ROWS(idxs))+1&","&ROWS(col)},
                        REDUCE(TOCOL(,1),rgs,LAMBDA(a,i,VSTACK(a,TOCOL(SORT(G(col,SPLIT(i,","))),2))))))))),
      sp,REGEXEXTRACT(in,REPT("(.)",LEN(in))),
      SUM(SEQUENCE(ROWS(sp),1,ROWS(sp),-1)*(TILT(sp)="O"))))
```

**Alternative approach: Replacing ".O" with "O."**

```py
=LET(in,A:A,
     rw,ROWS(in),
     SUMPRODUCT(
       SEQUENCE(rw,1,rw,-1)*
       (TRANSPOSE(
          REGEXEXTRACT(
            TOCOL(
              BYCOL(
                REGEXEXTRACT(in,REPT("(.)",rw)),
                  LAMBDA(col,REDUCE(JOIN(,col),SEQUENCE(rw),
                               LAMBDA(a,_,SUBSTITUTE(a,".O","O.")))))),
            REPT("(.)",rw)))="O")))
```
