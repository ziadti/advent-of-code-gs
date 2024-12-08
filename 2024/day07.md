**[Day 7: Bridge Repair](https://adventofcode.com/2024/day/7)**

_(Input expected in A:A)_

**Part 1 & 2**

```py
=MAP(
    {0;1},
    LAMBDA(_, 
        SUMPRODUCT(
            MAP(
                TOCOL(A:A, 1),
                LAMBDA(a,
                    LET(
                        s, SPLIT(a, ": "),
                        t, SINGLE(s),
                        t * (
                            0 < COUNTIF(
                                REDUCE(
                                    ,
                                    CHOOSECOLS(s, SEQUENCE(COUNTA(s)-1, 1, 2)),
                                    LAMBDA(a, v, {a+v; a*v; _*(a&v)})
                                ),
                                t
                            )
                        )
                    )
                )
            )
        )
    )
)
```
