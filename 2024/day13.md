**[Day 13: Claw Contraption](https://adventofcode.com/2024/day/13)**

_(Input expected in A1)_

**Part 1 & 2**

```py
=MAP({0; 10^13}, 
    LAMBDA(_, 
        SUMPRODUCT(
            LET(
                c, WRAPROWS(
                    SPLIT(
                        REGEXREPLACE(A1, "(\d+)|\n|.", "$1❅"), 
                        "❅"
                    ), 
                    6
                ),
                MAP(
                    INDEX(c,,1), INDEX(c,,2), INDEX(c,,3), 
                    INDEX(c,,4), INDEX(c,,5)+_, INDEX(c,,6)+_, 
                    LAMBDA(ax, ay, bx, by, x, y, 
                        LET(
                            m, MMULT(MINVERSE({ax, bx; ay, by}), {x; y}),
                            AND(ABS(m - ROUND(m)) < 0.001) * SUM(m * {3; 1})
                        )
                    )
                )
            )
        )
    )
)
```
