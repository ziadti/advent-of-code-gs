_Input expected in A1_

_Note: The formula for Part 1 takes a few minutes to load_

# Part 1
```py
=ARRAYFORMULA(
   LET(a,A1,
       in,SUBSTITUTE(a,CHAR(10),),
       sz,COLUMNS(SPLIT(a,CHAR(10))),
       tb,MID(in,SEQUENCE(sz,sz),1),
       mk,MAKEARRAY(sz,sz,LAMBDA(r,c,
            LET(v,INDEX(tb,r,c),
                t,IF(NOT(ISNUMBER(--v)),,
                       TEXTJOIN(,,
                          MAKEARRAY(3,3,LAMBDA(i,j,
                                    IF((r+i=2)+(c+j=2),,
                                       IFERROR(INDEX(tb,r+i-2,c+j-2))))))),
                IF(REGEXMATCH(t,"^[\d.]+$"),v,)))),
       flta,TOCOL(tb),
       fltb,TOCOL(mk),
       zo,JOIN(,N(flta=fltb)),
       jn,TEXTJOIN(,,tb),
       rgxp,SUBSTITUTE(REGEXREPLACE(REGEXREPLACE(jn,"[^\d.]","."),"\d","(.)"),")(",), 
       sub,SUM(REGEXEXTRACT(jn,rgxp)*REGEXMATCH(REGEXEXTRACT(zo,rgxp),"^1+$")),
       SUM(SPLIT(REGEXREPLACE(in,"(\d+)|.","$1 ")," "))-sub))
```

# Part 2
```py
=SUMPRODUCT(
   LET(in,A1,
       sz,COLUMNS(SPLIT(in,CHAR(10))),
       n,TOCOL(SPLIT(REGEXREPLACE(in,"(?s)(\d+)|.","$1 ")," ")),  
       lt_,CHAR(SEQUENCE(ROWS(n)*2)+9800),
       lt,REPT(ARRAY_CONSTRAIN(FILTER(lt_,COUNTIF(lt_,lt_)=1),ROWS(n),1),LEN(n)), 
       sb,REDUCE(in,SEQUENCE(ROWS(n)),
            LAMBDA(a,i,REGEXREPLACE(a,"\b"&INDEX(n,i)&"\b",INDEX(lt,i)))),
       tb,REGEXEXTRACT(TOCOL(SPLIT(sb,CHAR(10))),REPT("(.)",sz)),
       mk,MAKEARRAY(sz,sz,
            LAMBDA(r,c,
              IF(INDEX(tb,r,c)<>"*",, 
                 TEXTJOIN(,,IFERROR(MAKEARRAY(3,3,LAMBDA(i,j,INDEX(tb,r+i-2,c+j-2)))))))),
       flt,TOCOL(mk,3),
       sp,MAP(flt,
            LAMBDA(f,
              LET(r,REGEXREPLACE(f,"[.*]",),
                  UNIQUE(MID(r,SEQUENCE(1,LEN(r)),1),1)))), 
       QUERY(MAP(sp,LAMBDA(sp,FILTER(n,EXACT(LEFT(sp),LEFT(lt))))),"select Col1*Col2")))
```
