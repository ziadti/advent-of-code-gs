# Part 1
```cp
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
