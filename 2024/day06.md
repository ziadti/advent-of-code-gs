**[Day 6: Guard Gallivant](https://adventofcode.com/2024/day/6)**

_(Input expected in A:A)_

**Part 1**

```py
=ARRAYFORMULA(
    COUNTUNIQUE(
        LET(
            a, SPLIT(REGEXREPLACE(TOCOL(A:A, 1), "", "0"), 0),
            i, SEQUENCE(ROWS(a)),
            j, TOROW(i),
            g, COMPLEX(i, j),
            REDUCE(
                {-1; TOCOL(IF(a = "^", g, ), 1)},
                SEQUENCE(6000),
                LAMBDA(x, _, LET(
                    d, SINGLE(x),
                    r, ROWS(x),
                    c, INDEX(x, r),
                    nd, IMPRODUCT(d, "-i"),
                    o, COUNTIF(IF(g = IMSUM(c, d), a), "#"),
                    y, IF(o, nd, d),
                    s, IMSUM(c, y),
                    IF(
                        COUNTIF(g, s),
                        {IF(SEQUENCE(r) = 1, y, x); s},
                        x
                    )
                ))
            ) - 1
        )
    )
)
```
