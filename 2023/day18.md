**[Day 18: Lavaduct Lagoon](https://adventofcode.com/2023/day/18)**

_(Input expected in A:A)_

**Part 1 & 2**

```py
=ARRAYFORMULA(
   LET(sp,SPLIT(TOCOL(A:A,1)," "),
       F,LAMBDA(s,
           INDEX(
             REDUCE({0,1},SEQUENCE(ROWS(s)),
               LAMBDA(a,i,
                 LET(c,INDEX(s,i),
                     p,INDEX(a,,1)+IMREAL(c),
                     {p,INDEX(a,,2)+IMAGINARY(c)*p+IMABS(c)*0.5}))),,
             2)),
      {F(MAP(
           INDEX(sp,,1),INDEX(sp,,2),
           LAMBDA(d,s,IMPRODUCT(XLOOKUP(d,{"R";"D";"L";"U"},{1;"i";-1;"-i"}),s)))),
       F(MAP(
           INDEX(sp,,3),
           LAMBDA(c,
             IMPRODUCT(XLOOKUP(--MID(c,8,1),{0;1;2;3},{1;"i";-1;"-i"}),
                       HEX2DEC(MID(c,3,5))))))}))

```
