_Input expected in A:A_

_https://adventofcode.com/2023/day/6_

# Part 1 & 2

```python
  LET(in,A:A,
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
