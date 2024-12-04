**[Day 3: Mull It Over](https://adventofcode.com/2024/day/3)**

_(Input expected in A1)_

**Part 1 & 2**

```py
=MAP(
  {A1; REGEXREPLACE(A1, "(?s)don't\(\).*?(do\(\)|$)", "")},
  LAMBDA(
    _,
    SUMPRODUCT(
      MAP(
        TOCOL(
          SPLIT(
            REGEXREPLACE(_, "mul\((\d+),(\d+)\)|.", "$1*$2 "),
            " "
          )
        ),
        LAMBDA(x, SORTN(QUERY(, "select " & x)))
      )
    )
  )
)
```
