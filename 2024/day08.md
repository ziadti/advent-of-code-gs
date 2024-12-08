**[Day 8: Resonant Collinearity](https://adventofcode.com/2024/day/8)**

_(Input expected in A:A)_

**Part 1 & 2**

```py
=ARRAYFORMULA(
    MAP(
        {1; 0},
        LAMBDA(_, LET(
            a, SPLIT(REGEXREPLACE(TOCOL(A:A, 1), "", "❄️"), "❄️"),
            i, SEQUENCE(ROWS(a)),
            j, TOROW(i),
            g, COMPLEX(i, j),
            f, UNIQUE(TOCOL(IF(a = ".", , a), 1)),
            COUNTUNIQUE(
                REDUCE(
                    TOCOL(, 1),
                    f,
                    LAMBDA(x, y, LET(
                        o, TOCOL(IF(EXACT(a, y), g, ), 1),
                        s, SEQUENCE(ROWS(o)),
                        p, SPLIT(
                            TOCOL(IF(o = TOROW(o), , o & "," & TOROW(o)), 1),
                            ","
                        ),
                        VSTACK(
                            x,
                            MAP(
                                j - 1,
                                LAMBDA(n, MAP(
                                    INDEX(p, , 1),
                                    INDEX(p, , 2),
                                    LAMBDA(x, y, LET(
                                        m, IMSUM(y, IMPRODUCT(IMSUB(y, x), IF(_, 1, n))),
                                        IF(COUNTIF(g, m), m, )
                                    ))
                                ))
                            )
                        )
                    ))
                )
            )
        ))
    )
)

```
