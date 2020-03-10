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