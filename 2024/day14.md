**[Day 14: Restroom Redoubt](https://adventofcode.com/2024/day/14)**

_(Input expected in A:A)_

**Part 1 & 2**

```py
=ARRAYFORMULA(
    LET(
        s, SPLIT(TOCOL(A:A, 1), "p=, v"),
        w, 101, h, 103, t, 100,
        x, INDEX(s, , 1), y, INDEX(s, , 2),
        vx, INDEX(s, , 3), vy, INDEX(s, , 4),
        nx, MOD(x + vx * t, w), ny, MOD(y + vy * t, h),
        xl, nx < (w - 1) / 2, xr, nx > (w - 1) / 2,
        yd, ny < (h - 1) / 2, yt, ny > (h - 1) / 2,
        {
            PRODUCT({
                SUM(xl * yt);
                SUM(xr * yt);
                SUM(xl * yd);
                SUM(xr * yd)
            });
            SINGLE(
                TOCOL(
                    MAP(
                        SEQUENCE(w * h),
                        LAMBDA(t,
                            LET(
                                nx, MOD(x + vx * t, w),
                                ny, MOD(y + vy * t, h),
                                z, nx & 0 & ny,
                                IF(COUNTUNIQUE(z) = COUNTA(z), t, )
                            )
                        )
                    ),
                    1
                )
            )
        }
    )
)
```
