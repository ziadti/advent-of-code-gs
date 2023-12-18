**[Day 16: The Floor Will Be Lava](https://adventofcode.com/2023/day/16)**

_(Input expected in A:A)_

**Part 1**

```py
=ARRAYFORMULA(
  LET(size,110,
      grid,REGEXEXTRACT(A:A,REPT("(.)",size)),
      coord,COMPLEX(SEQUENCE(size),SEQUENCE(1,size)),
      path,REDUCE(
            {"1,i",FALSE},
            SEQUENCE(16000),
            LAMBDA(acc,_,
              LET(to_visit,QUERY(acc,"select Col1 where Col2 = FALSE limit 1"),
                  pos,REGEXEXTRACT(to_visit,"(.+),"),
                  dir,REGEXEXTRACT(to_visit,",(.+)"),
                  new_pos,IMSUM(pos,dir),
                  updated_acc,{INDEX(acc,,1),IF(INDEX(acc,,1)=pos&","&dir,TRUE,INDEX(acc,,2))},
                  cur,INDEX(grid,IMREAL(new_pos),IMAGINARY(new_pos)),
                  IFNA(
                    IF(OR(COUNTIF(coord,new_pos)=0,
                          XLOOKUP(pos&","&dir,INDEX(acc,,1),INDEX(acc,,2),FALSE)=TRUE),
                       updated_acc,
                       IF(cur="/",VSTACK(updated_acc,{new_pos&","&IMSUB(0,COMPLEX(IMAGINARY(dir),IMREAL(dir))),FALSE}),
                          IF(cur="\",VSTACK(updated_acc,{new_pos&","&COMPLEX(IMAGINARY(dir),IMREAL(dir)),FALSE}),
                             IF(cur="|",VSTACK(updated_acc,{new_pos&",-1",FALSE;new_pos&",1",FALSE}),
                                IF(cur="-",VSTACK(updated_acc,{new_pos&",-i",FALSE;new_pos&",i",FALSE}),
                                   VSTACK(updated_acc,{new_pos&","&dir,FALSE})))))),
                    acc)))),
       visited,REGEXEXTRACT(INDEX(path,,1),"(.+),"),
       ans,COUNTUNIQUE(visited)-1,
       ans))
```
