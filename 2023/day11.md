_Input expected in A:A_

_Note: This formula is extremely slow_

# Part 1 & 2

```py
=MAP({2,1e6},
   LAMBDA(v,SUMPRODUCT(
     LET(in,A:A,
         sz,ROWS(in),
         sqv,SEQUENCE(sz),
         sqh,TOROW(sqv),
         uni,REGEXEXTRACT(in,REPT("(.)",sz)),
         expr,JOIN(,--REGEXMATCH(TRANSPOSE(QUERY(TRANSPOSE(uni),,9^9)),"^[^#]+$")),
         expc,JOIN(,--REGEXMATCH(TRANSPOSE(QUERY(uni,,9^9)),"^[^#]+$")),
         cord_,TOCOL(IF(uni<>"#",,sqv&","&sqh),3),
         cord,SPLIT(
                TOCOL(IF(SEQUENCE(ROWS(cord_))>SEQUENCE(1,ROWS(cord_)),,
                       cord_&","&TOROW(cord_)),3),","),
         ax,INDEX(cord,,1),
         ay,INDEX(cord,,2),
         bx,INDEX(cord,,3),
         by,INDEX(cord,,4),
         xmin,IF(ax<bx,ax,bx),
         xmax,IF(ax>bx,ax,bx),
         ymin,IF(ay<by,ay,by),
         ymax,IF(ay>by,ay,by),
         rgxpr,REGEXREPLACE(SUBSTITUTE(expr,"1","(1)"),"[01]","."),
         rgxpc,REGEXREPLACE(SUBSTITUTE(expc,"1","(1)"),"[01]","."),
         clsr,LEN(REGEXREPLACE(rgxpr,"[^(]",)),
         clsc,LEN(REGEXREPLACE(rgxpc,"[^(]",)),
         emptr,MMULT(
                 REGEXEXTRACT(expr,rgxpr)*
                   REGEXEXTRACT(REPT(0,xmin-1)&
                                REPT(1,xmax-xmin+1)&
                                REPT(0,sz-xmax),rgxpr),
                 SEQUENCE(clsr)^0),
         emptc,MMULT(
                 REGEXEXTRACT(expc,rgxpc)*
                   REGEXEXTRACT(REPT(0,ymin-1)&
                                REPT(1,ymax-ymin+1)&
                                REPT(0,sz-ymax),rgxpc),
                 SEQUENCE(clsc)^0),
         IF((ax=bx)*(ay=by),,(xmax-xmin)+(ymax-ymin)+(v-1)*(emptr+emptc))))))
```
