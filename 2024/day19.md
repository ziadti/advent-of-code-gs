**[Day 19: Linen Layout](https://adventofcode.com/2024/day/19)**

_(Input expected in A1:A401)_

_* Excel formula_

**Part 1 & 2**

```py
=MAP(
    {1;0},
    LAMBDA(_,
        REDUCE(
            0,
            A2:A401,
            LAMBDA(s, d,
                s + LET(
                    t,
                    TAKE(
                        REDUCE(
                            VSTACK(1, SEQUENCE(LEN(d)) * 0),
                            SEQUENCE(LEN(d)),
                            LAMBDA(a, i,
                                REDUCE(
                                    a,
                                    TEXTSPLIT(A1, ", "),
                                    LAMBDA(a, p,
                                        IF(
                                            LEFT(MID(d, i, 9^9), LEN(p)) = p,
                                            IF(SEQUENCE(ROWS(a)) = i + LEN(p),
                                                INDEX(a, i) + INDEX(a, i + LEN(p)),
                                                a
                                            ),
                                            a
                                        )
                                    )
                                )
                            )
                        ),
                        -1
                    ),
                    IF(_, t > 0, t)
                )
            )
        )
    )
)
```
