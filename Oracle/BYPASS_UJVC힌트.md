# BYPASS_UJVC
UPDATE 시에 키보존 테이블에 대해 DML이 불가능한 것을 가능하게 해주는 힌트라고 이해할 수 있다.

```sql
UPDATE /*+ BYPASS_UJVC */
(
SELECT TAB1. COL1, TAB1. COL2, TAB1. COL3 , TAB2.COL5, TAB6.COL6
  FROM TAB1, TAB2
 WHERE TAB1.COL1 = TAB2.COL5
) 
SET COL1 2 = COL6
```
- 키보존 테이블이란 키 값이 변경되지 않는 테이블을 말한다. 즉, 2개 테이블 조인이 1:M 테이블일 경우 M 테이블은 키보존 테이블이다.
- UJVC는 Updatable Join View Check의 약자다.

원래 키보존 테이블 이외의 테이블은 DML이 불가능하나 10g까지는 BYPASS_UJVC 힌트 사용 시 DML이 가능해져, 마치 마법과도 같은 힌트였다.

그러나 이 힌트는 결코 마법이 아니며, 사용자가 의도하지 않는 값으로 DML이 될 수 있는 위험한 힌트이기도 하다. 이 힌트의 위험성은 뒤에서 다시 언급될 것이므로 일단 여기까지만 설명하도록 하겠다.

이러한 이유로 11g에서는 사용을 금지하기 위해 아예 지원을 중단했을 것으로 짐작된다.

- 11g에서는 해당 힌트를 사용하더라도 키보존 테이블 변경 시의 오류코드와 동일한 ORA-01779 오류를 내며 종료한다.
-  11g에서 BYPASS_UJVC 힌트를 사용한 DML문에 대해서는 두 가지로 변경할 수 있다.