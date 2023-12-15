**[Day 15: Lens Library](https://adventofcode.com/2023/day/15)**

_Input expected in A1_

**Part 1 & 2**

```py
=ARRAYFORMULA(
   LET(in,A1,
       n_boxes,256,
       GET_HASH,LAMBDA(arr,MAP(arr,LAMBDA(c,REDUCE(,SEQUENCE(LEN(c)),LAMBDA(hash,i,MOD((hash+CODE(MID(c,i,1)))*17,n_boxes)))))),
       box_id,SEQUENCE(n_boxes)-1,
       label_hashes,GET_HASH(TOCOL(REGEXEXTRACT(SPLIT(in,","),"\w+"))),
       init_sequence,TOCOL(SPLIT(in,",")),
       final_state,REDUCE(
                     {box_id,REPT(box_id,)},
                     SEQUENCE(ROWS(init_sequence)),
                     LAMBDA(boxes,i,
                       LET(hash,INDEX(label_hashes,i),
                           lens,INDEX(init_sequence,i),
                           content,INDEX(boxes,,2),
                           lens_label,REGEXEXTRACT(lens,"\w+"),
                           IF(box_id<>hash,{box_id,content},
                              IF(REGEXMATCH(lens,"-"),
                                {box_id,IF(REGEXMATCH(content,"\b"&lens_label&"\b")-1,
                                           content,
                                           REGEXREPLACE(content,",?\b"&lens_label&"=\d+",))},
                              IF(REGEXMATCH(lens,"="),
                                {box_id,IF(REGEXMATCH(content,"\b"&lens_label&"\b")-1,
                                           content&","&lens,
                                           REGEXREPLACE(content,REGEXREPLACE(lens,"\d+","\\d+"),lens))})))))),
        {SUM(GET_HASH(SPLIT(in,","))),
         SUM(IFERROR((box_id+1)*
             REGEXEXTRACT(SPLIT(INDEX(final_state,,2),","),"\d+")*
             SEQUENCE(1,COLUMNS(SPLIT(INDEX(final_state,,2),",")))))}))
```
