_Input expected in A:A_

# Part 1

```python
=SUMPRODUCT(
   LET(in,A:A,
       rk,MAP(in,
          LAMBDA(in_,
             LET(crd,MID(in_,ROW(1:5),1),
                 cnt,JOIN(,SORT(QUERY(QUERY(crd,"select count(Col1) group by Col1"),"offset 1",))),
                 SWITCH(--cnt,11111,0,1112,1,122,2,113,3,23,4,14,5,6)))
             ),
       ts,REDUCE(in,ROW(1:5),LAMBDA(v,i,SUBSTITUTE(v,MID("TJQKA",i,1),MID("VWXYZ",i,1)))),
       SEQUENCE(ROWS(in))*REGEXEXTRACT(SORT(in,rk,1,ts,1),"\d+$")))
```

# Part 2
```python
=SUMPRODUCT(
   LET(in,A:A,
       Q,LAMBDA(x,QUERY(QUERY(x,"select count(Col1),Col1 group by Col1"),"offset 1",)),
       rk,MAP(in,
            LAMBDA(in_,
              LET(crd_,MID(in_,ROW(1:5),1),
                  grp_,Q(crd_),
                  grp,SORT(grp_,SUBSTITUTE(INDEX(grp_,,2),"J",0),),
                  vl,VLOOKUP(MAX(INDEX(grp,,1)),grp,2,), 
                  cnt,JOIN(,SORT(INDEX(Q(LEFT(SUBSTITUTE(crd_,"J",IF(vl="J",IFNA(INDEX(FILTER(INDEX(grp,,2),INDEX(grp,,2)<>"J"),1),"A"),vl)),5)),,1))),
                  SWITCH(--cnt,11111,0,1112,1,122,2,113,3,23,4,14,5,6)))
              ),
        ts,REDUCE(LEFT(in,5),ROW(1:5),LAMBDA(v,i,SUBSTITUTE(v,MID("TJQKA",i,1),MID("V0XYZ",i,1)))),
        SEQUENCE(ROWS(in))*REGEXEXTRACT(SORT(in,rk,1,ts,1),"\d+$")))
```
