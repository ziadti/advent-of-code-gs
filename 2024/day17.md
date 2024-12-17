**[Day 17: Chronospatial Computer(https://adventofcode.com/2024/day/17)**

_(Input expected in A1)_

**Part 1**


```py
=LET(
  x, SPLIT(REGEXREPLACE(A1, "([\d,]+)|\n|.", "$1❅"), "❅"),
  p, SPLIT(INDEX(x, 4), ","),
  EX, LAMBDA(EX, a, b, c, i, out,
    LET(
      opc, INDEX(p, i + 1),
      op, INDEX(p, i + 2),
      cop, SWITCH(op, 4, a, 5, b, 6, c, op),
      dv, INT(a / 2 ^ cop),
      IF(
        i >= COUNT(p), out,
        EX(
          EX,
          IF(opc = 0, dv, a),
          SWITCH(opc, 
            1, BITXOR(b, op), 
            2, MOD(cop, 8), 
            4, BITXOR(b, c), 
            6, dv,
            b
          ),
          IF(opc = 7, dv, c),
          IF(opc = 3, IF(a, op - 2, i), i) + 2,
          IF(opc = 5, TEXTJOIN(",", 1, out, MOD(cop, 8)), out)
        )
      )
    )
  ),
  EX(EX, INDEX(x, 1), INDEX(x, 2), INDEX(x, 3), 0, )
)

```
