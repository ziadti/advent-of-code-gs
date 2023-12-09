_Input expected in A:A_

# Part 1 & 2

```py
=LET(Y,LAMBDA(Y,a,i,
         SUMPRODUCT(
            BYROW(
              LET(l,CHOOSEROWS(a,-1),
                  IF(OR(l)-1,
                     a,
                     Y(Y,{a;IFNA(CHOOSECOLS(l,SEQUENCE(1,COLUMNS(l)-i,2))-l)},i+1))),
              LAMBDA(r,INDEX(r,COUNT(r)))))),
     BYCOL(
       MAP(A:A,
         LAMBDA(s_,
            LET(s,SPLIT(s_," "),
               {Y(Y,s,1), 
                Y(Y,CHOOSECOLS(s,SEQUENCE(COUNT(s),1,-1,-1)),1)}))),
        LAMBDA(c,SUM(c))))
```
