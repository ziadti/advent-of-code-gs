**[Day 2: Red-Nosed Reports](https://adventofcode.com/2024/day/2)**

_(Input expected in A:A)_

**Part 1**

```py
=SUMPRODUCT(
  MAP(
    TOCOL(A:A, 1),
    LAMBDA(a,
      LET(
        s, SPLIT(a, " "),
        x, CHOOSECOLS(s - {0, s}, SEQUENCE(COLUMNS(s) - 1, 1, 2)),
        OR(
          AND(ISBETWEEN(x, 1, 3)),
          AND(ISBETWEEN(x, -3, -1))
        )
      )
    )
  )
)
```

**Part 2**

```py
=SUMPRODUCT(
  MAP(
    TOCOL(A:A, 1),
    LAMBDA(b,
      OR(
        MAP(
          LET(
            s, SPLIT(b, " "),
            REDUCE(
              b,
              SEQUENCE(COLUMNS(s)),
              LAMBDA(x, i,
                IFNA(
                  VSTACK(x, JOIN(" ", FILTER(s, NOT(SEQUENCE(1, COLUMNS(s)) = i))))
                )
              )
            )
          ),
          LAMBDA(a,
            LET(
              s, SPLIT(a, " "),
              x, CHOOSECOLS(s - {0, s}, SEQUENCE(COLUMNS(s) - 1, 1, 2)),
              OR(
                AND(ISBETWEEN(x, 1, 3)),
                AND(ISBETWEEN(x, -3, -1))
              )
            )
          )
        )
      )
    )
  )
)

```
