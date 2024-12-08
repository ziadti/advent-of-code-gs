**[Day 5: Print Queue](https://adventofcode.com/2024/day/5)**

_(Input expected in A:A)_

**Part 1 & 2**

```py
=ARRAYFORMULA(
  BYCOL(
    LET(
      T, LAMBDA(g, LET(
        e, UNIQUE(TOCOL(g)),
        ini_in, COUNTIF(INDEX(g,, 2), e),
        ini_q, FILTER(e, 0 = ini_in),
        r, REDUCE(
          HSTACK(e, ini_in, ini_q),
          SEQUENCE(COUNTUNIQUE(g)),
          LAMBDA(a, _, LET(
            in, INDEX(a,, 2),
            q, INDEX(a,, 3),
            topo, INDEX(a,, 4),
            new_topo, TOCOL(VSTACK(topo, INDEX(q, 1, 1)), 3),
            new_g, FILTER(g, 0 = COUNTIF(new_topo, INDEX(g,, 1))),
            new_in, COUNTIF(INDEX(new_g,, 2), e),
            new_q, UNIQUE(TOCOL(
              VSTACK(
                FILTER(q, SEQUENCE(ROWS(q)) > 1),
                LET(
                  x, FILTER(e, 0 = new_in),
                  FILTER(x, 0 = COUNTIF(new_topo, x))
                )
              ), 3
            )),
            HSTACK(e, COUNTIF(INDEX(new_g,, 2), e), new_q, new_topo)
          ))
        ),
        INDEX(r,, 4)
      )),
      a, A:A,
      MAP(
        FILTER(a, FIND(",", a)),
        LAMBDA(w_, LET(
          w, TOCOL(SPLIT(w_, ",")),
          x, SPLIT(
            FILTER(
              a,
              FIND("|", a),
              REGEXMATCH(a, "^(" & JOIN("|", SUBSTITUTE(w, ",", "|")) & ")\|")
            ),
            "|"
          ),
          t, T(x),
          f, FILTER(t, COUNTIF(w, t)),
          IF(
            OR(f <> w),
            {0, INDEX(f, ROWS(f) / 2 + 1)},
            {INDEX(f, ROWS(f) / 2 + 1), 0}
          )
        ))
      )),
      LAMBDA(c, SUM(c))  
  )
)
```
