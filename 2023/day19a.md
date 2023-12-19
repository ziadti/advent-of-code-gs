**[Day 19: Aplenty](https://adventofcode.com/2023/day/19)**

_(Input expected in A:A)_

**Part 1**

```py
=SUMPRODUCT(
   LET(in,A:A,
       sp,SPLIT(FILTER(in,LEFT(in)<>"{"),",{}"),
       workflow,INDEX(sp,,1),
       conditions,CHOOSECOLS(sp,SEQUENCE(COLUMNS(sp)-1,1,2)),
       ratings,FILTER(in,LEFT(in)="{"),
       SPLIT(
         FILTER(ratings,
                "A"=MAP(ratings,
                      LAMBDA(ratings,
                        REDUCE("in",SEQUENCE(10),
                          LAMBDA(cur_,_,
                            IFERROR(
                              LET(cur,XLOOKUP(cur_,workflow,conditions),
                                  QUERY(REDUCE(TOCOL(,1),
                                        SEQUENCE(COUNTA(cur)-1),
                                        LAMBDA(_,i,
                                           VSTACK(_,
                                              LET(val,INDEX(cur,,i),
                                                  cat,REGEXEXTRACT(val,"\w+"),
                                                  op,REGEXEXTRACT(val,"[<>]"),
                                                  bound,--REGEXEXTRACT(val,"\d+"),
                                                  next,REGEXEXTRACT(val,"\w+$"),
                                                  rating,VLOOKUP(cat,WRAPROWS(SPLIT(ratings,"=,{}"),2),2,),
                                                  IF(op="<",IF(rating<bound,next,INDEX(cur,,i+1)),
                                                    IF(rating>bound,next,INDEX(cur,,i+1))))))),
                                        "where not Col1 contains ':' limit 1",)),
                              cur_)))))),"{xmas,=}")))
```
