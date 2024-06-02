**[Day 21: Step Counter](https://adventofcode.com/2023/day/21)**

_(Input expected in A:A)_

_Note: This formula is extremely slow_

**Part 1**

```py
=ARRAYFORMULA(
  LET(in,TOCOL(A:A,1),
      dim,131,
      grid_,REGEXEXTRACT(in,REPT("(.)",dim)),
      grid,SPLIT(TOCOL(IF(grid_="#",,grid_&","&COMPLEX(SEQUENCE(dim),SEQUENCE(1,dim))),1),","),
      ROWS(
        REDUCE("66+66i",
          SEQUENCE(64),
          LAMBDA(to_visit,_,
            LET(pos,MAP(to_visit,
                        LAMBDA(cur,{IMSUM(cur,1),IMSUM(cur,-1),IMSUM(cur,"i"),IMSUM(cur,"-i")})),
                UNIQUE(TOCOL(IF(COUNTIF(grid,pos),pos,),1))))))))
```
