# Merge into

```sql
Merge Into tb_test T  -- (데이터가 변경될 대상 테이블)
Using (
    tb_join     
) S -- 변경시킬 조건 테이블  
On (T.joinColumn = S.joinColumn) -- 조건
-- On 절에 있는 컬럼은 업데이트 시킬 수 없다.
When Match Then
Update
   set T.updateColumn = S.updateColumn
   -- On절에서 매칭된 row를 업데이트
When Not Match Then
   Insert into tb_test (T.joinColumn, T.updateColumn)
   Values (S.joingColumn, S.updateColumn)
   -- On절에서 매칭이 안된 row를 삽입
```

> MERGE UPDATE 절이나 MERGE INSERT 절의 WHERE 절의 조건은 인라인 뷰에 기술하는 것이 성능적인 측면에서 바람직하다. 

> 다만 MERGE UPDATE 절과 MERGE INSERT 절을 모두 사용하는 경우 결과가 달라지지 않게 주의해야 한다.

```sql
MERGE
 INTO (SELECT * FROM t1 WHERE c1 BETWEEN 1 AND 100) a
USING (SELECT * FROM t2 WHERE c1 BETWEEN 1 AND 100 AND c2 BETWEEN 1 AND 10) b
   ON (b.c1 = a.c1)
 WHEN MATCHED THEN
    UPDATE
       SET a.c2 = b.c2;
  
-------------------------------------------------------------------------------------
| Id  | Operation                               | Name  | Starts | A-Rows | Buffers |
-------------------------------------------------------------------------------------
|   0 | MERGE STATEMENT                         |       |      1 |      0 |     132 |
|   1 |  MERGE                                  | T1    |      1 |      0 |     132 |
|   2 |   VIEW                                  |       |      1 |     10 |     120 |
|   3 |    NESTED LOOPS                         |       |      1 |     10 |     120 |
|   4 |     NESTED LOOPS                        |       |      1 |     10 |     110 |
|*  5 |      TABLE ACCESS BY INDEX ROWID BATCHED| T2    |      1 |     10 |     102 |
|*  6 |       INDEX RANGE SCAN                  | T2_X1 |      1 |    100 |       2 |
|*  7 |      INDEX RANGE SCAN                   | T1_X1 |     10 |     10 |       8 |
|   8 |     TABLE ACCESS BY INDEX ROWID         | T1    |     10 |     10 |      10 |
-------------------------------------------------------------------------------------
  
Predicate Information (identified by operation id):
---------------------------------------------------
   5 - filter(("C2"<=10 AND "C2">=1))
   6 - access("C1">=1 AND "C1"<=100)
   7 - access("T2"."C1"="T1"."C1")
       filter(("C1"<=100 AND "C1">=1))
```