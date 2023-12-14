**[Day 7: Camel Cards](https://adventofcode.com/2023/day/7)**

_(Input expected in A:A)_

**Part 1 & 2**

```python
=ARRAYFORMULA(
   LET(in,A:A,
       Q,LAMBDA(x,QUERY(QUERY(x,"select count(Col1),Col1 group by Col1"),"offset 1",)),
       S,LAMBDA(x,REDUCE(in,ROW(1:5),LAMBDA(v,i,SUBSTITUTE(v,MID("TQKAJ",i,1),MID("VXYZ"&x,i,1))))),
       W,LAMBDA(x,SWITCH(--x,11111,0,1112,1,122,2,113,3,23,4,14,5,6)),
       O,LAMBDA(x,y,SEQUENCE(ROWS(in))*REGEXEXTRACT(SORT(in,x,1,y,1),"\d+$")),
       rk,MAP(in,
            LAMBDA(in_,
              LET(crd,MID(in_,ROW(1:5),1),
                  grp_,Q(crd),
                  cntA,JOIN(,SORT(INDEX(grp_,,1))),
                  rkA,W(cntA),
                  grp,SORT(grp_,SUBSTITUTE(INDEX(grp_,,2),"J",0),),
                  vl,VLOOKUP(MAX(INDEX(grp,,1)),grp,2,), 
                  cntB,JOIN(,SORT(INDEX(Q(LEFT(SUBSTITUTE(crd,"J",IF(vl="J",IFNA(INDEX(FILTER(INDEX(grp,,2),INDEX(grp,,2)<>"J"),1),"A"),vl)),5)),,1))),
                  rkB,W(cntB),
                  {rkA,rkB}))
              ),
       BYCOL({O(INDEX(rk,,1),S("W")),O(INDEX(rk,,2),S(0))},LAMBDA(c,SUM(c)))))
```
