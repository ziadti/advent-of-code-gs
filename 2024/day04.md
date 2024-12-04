**[Day 4: Ceres Searchs](https://adventofcode.com/2024/day/4)**

_(Input expected in A:A)_

**Part 1**

```py
=ARRAYFORMULA(
  LET(
    L, LAMBDA(s, SUM(LEN(REGEXREPLACE(s, "(X)MAS|.", "$1") & REGEXREPLACE(s, "(S)AMX|.", "$1")))),
    a, TOCOL(A:A, 1),
    s, SPLIT(REGEXREPLACE(a, , "0"), 0),
    i, SEQUENCE(ROWS(a)),
    j, SEQUENCE(1, LEN(A1)),
    L(a) +
    L(BYCOL(s, LAMBDA(c, JOIN(, c)))) +
    REDUCE(
      , SEQUENCE((MAX(i, j) - 4) * 2 + 1, 1, 4 - MAX(i)),
      LAMBDA(x, y, x + L(TEXTJOIN(, , IF(i + y = j, s, ))))
    ) +
    REDUCE(
      , SEQUENCE((MAX(i, j) - 4) * 2 + 1, 1, 4 - MAX(i)),
      LAMBDA(x, y, x + L(TEXTJOIN(, , IF(i + j = ROWS(s) + 1 + y, s, ))))
    )
  )
)
```

**Part 2**

```py
=ARRAYFORMULA(
  LET(
    a, TOCOL(A:A, 1),
    r, SEQUENCE(ROWS(a)),
    c, SEQUENCE(1, LEN(SINGLE(a))),
    g, COMPLEX(c, r),
    s, SPLIT(REGEXREPLACE(a, , "0"), 0),
    as, TOCOL(IF(s = "A", g, ), 1),
    w, REDUCE(
      , as,
      LAMBDA(x, y,
        VSTACK(
          x,
          TEXTJOIN(
            , ,
            IF(
              REGEXMATCH(
                g,
                "^(" & SUBSTITUTE(JOIN("|", IMSUM(y, "-1-i"), IMSUM(y, "-1+i"), IMSUM(y, "1-i"), IMSUM(y, "1+i")) & ")$",
                "+", "\+"
              ),
              s,
            )
          )
        )
      )
    ),
    SUM(--REGEXMATCH(w, "MMSS|MSMS|SSMM|SMSM"))
  )
)
```
