**[Day 3: Gear Ratios](https://adventofcode.com/2023/day/3)**

_(Input expected in A1)_

**Part 1**
```py
=SUMPRODUCT(
   LET(in,A1,
       sz,COLUMNS(SPLIT(in,CHAR(10))),
       n,TOCOL(SPLIT(REGEXREPLACE(in,"(?s)(\d+)|.","$1 ")," ")),
       lt_,CHAR(SEQUENCE(ROWS(n)*2)+9800),
       lt,REPT(ARRAY_CONSTRAIN(FILTER(lt_,COUNTIF(lt_,lt_)=1),ROWS(n),1),LEN(n)),
       sb,REDUCE(in,SEQUENCE(ROWS(n)),
            LAMBDA(a,i,REGEXREPLACE(a,"(?s)(.*?)\b"&INDEX(n,i)&"\b(.*)","$1"&INDEX(lt,i)&"$2"))),
       tb,REGEXEXTRACT(TOCOL(SPLIT(sb,CHAR(10))),REPT("(.)",sz)),
       mk,MAKEARRAY(sz,sz,
            LAMBDA(r,c,
              IF(COUNTIF(LEFT(lt),INDEX(tb,r,c))=0,,
                 TEXTJOIN(,,IFERROR(MAKEARRAY(3,3,LAMBDA(i,j,INDEX(tb,r+i-2,c+j-2)))))))),
       flt,TOCOL(mk,3),
       cln,FILTER(flt,REGEXMATCH(flt,"[#%=/+$@&*-]")),
       MAP(UNIQUE(LEFT(REGEXREPLACE(cln,"[#%=/+$@&*.-]",))),
         LAMBDA(u,FILTER(n,EXACT(u,LEFT(lt)))))))
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
