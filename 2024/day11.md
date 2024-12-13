**[Day 11: Plutonian Pebbles](https://adventofcode.com/2024/day/11)**

_(Input expected in A1)_

**Part 1**

```py
=ARRAYFORMULA(
    ROWS(
        REDUCE(
            SPLIT(A1, " "), 
            SEQUENCE(25), 
            LAMBDA(s, _, 
                LET(
                    l, LEN(s) / 2, 
                    TOCOL(
                        SPLIT(
                            TOCOL(
                                IF(
                                    s = 0, 
                                    1, 
                                    IF(
                                        MOD(l * 2, 2) = 0, 
                                        MID(s, 1, l) & " " & MID(s, l + 1, l), 
                                        s * 2024
                                    )
                                )
                            ), 
                            " "
                        ), 
                        1
                    )
                )
            )
        )
    )
)
```
