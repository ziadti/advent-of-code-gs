_Input expected in A1:A2_

# Part 1 & 2

```cpp
=INDEX(
  LET(in,A1:A2,
      splt,{SPLIT(in,"TtimeDsnca: "),REGEXREPLACE(in,"\D",)},
      time,INDEX(splt,1),
      dist,INDEX(splt,2),
      a,0.5*time,
      b,0.5*(time^2-4*dist)^0.5,
      QUERY(
       ROUNDDOWN(a+b)-ROUNDUP(a-b)+1,
      "select Col1*Col2*Col3*Col4,Col5")),
  2)
```
