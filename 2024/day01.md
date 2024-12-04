**[Day 1: Historian Hysteria](https://adventofcode.com/2024/day/1)**

_(Input expected in A:A)_

**Part 1 & 2**

```py
=ARRAYFORMULA(
  LET(
    x, BYCOL(SPLIT(A:A, " "), LAMBDA(c, SORT(c))),
    {
      SUM(ABS(MMULT(x, {1; -1})));
      SUM(INDEX(x, , 1) * COUNTIF(INDEX(x, , 2), INDEX(x, , 1)))
    }
  )
)
```
