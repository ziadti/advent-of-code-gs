**[Day 5: If You Give A Seed A Fertilizer](https://adventofcode.com/2023/day/5)**

_(Input expected in A:A)_

**Part 1**

```python
=ARRAYFORMULA(
  LET(in,TOCOL(A:A,1),
      rs,SEQUENCE(ROWS(in)-1),
      sd,SPLIT(INDEX(in,1),"seeds: "),
      mp,CHOOSEROWS(in,SEQUENCE(ROWS(in)-1,1,2)),
      rc,COUNTIFS(mp,"*to*",rs,"<="&rs),
      u,UNIQUE(rc),
      MIN(MAP(sd,
            LAMBDA(sd_,
              REDUCE(sd_,u,
                LAMBDA(v,i,
                   LET(s,SPLIT(QUERY(FILTER(mp,rc=i),"offset 1",)," "),
                       x,INDEX(s,,1),
                       y,INDEX(s,,2),
                       z,INDEX(s,,3),
                       jn,JOIN(,IF(ISBETWEEN(--REPT(v,SEQUENCE(ROWS(s))^0),y,y+z-1),v-y+x,)),
                       IF(jn="",v,--jn)))))))))
```
