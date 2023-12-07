_Input expected in A:A_

# Part 1 & 2

```py
={SUMPRODUCT(LET(r,REGEXREPLACE(A:A,"\D",),LEFT(r)&RIGHT(r))),
  SUMPRODUCT(
    LET(n,{"one";"two";"three";
          "four";"five";"six";
          "seven";"eight";"nine"},
        r,REGEXREPLACE(
            REDUCE(
              A:A,
              ROW(1:9),
              LAMBDA(a,i,SUBSTITUTE(a,INDEX(n,i),INDEX(n&ROW(1:9)&n,i)))),
            "\D",),
        LEFT(r)&RIGHT(r)))
 }
```
