**[Day 6: Wait For It](https://adventofcode.com/2023/day/6)**

_(Input expected in A:A)_

**Part 1 & 2**

```python
  LET(in,TOCOL(A:A,1),
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
