# NULL Handling

### Date: 2024.02.03

---

### Null Handling
- **COALESCE** 함수 사용하여, Null 값을 다른 값으로 표현할 수 있다.

```sql
// NULL이 없는 column 조회
SELECT * FROM DB_name.Table_name WHERE column_name IS NOT NULL;

// NULL인 항목들을 다른 값으로 표현해서 출력
SELECT
  COALESCE(column_name, '####')
FROM DB_name.Table_name
```