**[Day 13: Point of Incidence](https://adventofcode.com/2023/day/13)**

_(Input expected in A1)_

**Part 1 & 2**

```py
=MAP({0,1},
   LAMBDA(mrg,
     SUMPRODUCT(
       MAP(TOCOL(SPLIT(A1,CHAR(10)&CHAR(10),)),
         LAMBDA(in,
           LET(S,LAMBDA(arr,LET(rw,ROWS(arr),
                   REDUCE(0,SEQUENCE(rw-1),
                     LAMBDA(a,i,
                       LET(l_,CHOOSEROWS(arr,SEQUENCE(i)),
                           r_,CHOOSEROWS(arr,SEQUENCE(rw-i,1,i+1)),
                           cl,ROWS(l_),
                           cr,ROWS(r_),
                           l,IF(cl>cr,CHOOSEROWS(l_,SEQUENCE(cr,1,cl-cr+1)),l_),
                           r,IF(cr>cl,CHOOSEROWS(r_,SEQUENCE(cl)),r_),
                           rr,CHOOSEROWS(r,SEQUENCE(ROWS(r),1,ROWS(r),-1)),
                           IF(COUNTIF(l=rr,FALSE)=mrg,i,a)))))),
               t,TOCOL(SPLIT(in,CHAR(10))),
               sp,REGEXEXTRACT(t,REPT("(.)",LEN(t))),
               100*S(sp)+S(TRANSPOSE(sp))))))))
```
