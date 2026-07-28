# 單元 6 - 使用 NamedParameterJdbcTemplate（三）- query 方法（SELECT）

### NamedParameterJdbcTemplate

```java
query(String sql, Map‹String, Object> map, RowMapper<T> rowMapper)
```

1. `sql`: 放要執行的 sql 語法
2. `map`: 放 sql 語法裡面的變數的値
3. `rowMapper`: 將資料庫査詢出來的數據，轉換成 Java object
    - `List<Student> studentList`

在寫 SELECT sql 時，不要使用 `*` 號，使用 `*` 號的缺點：

1. 花費額外的網路流量
2. 無法提升資料庫査詢的速度 (`INDEX`)

```java
@RestController
public class StudentController {

    @Autowired
    private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

    @GetMapping("/students")
    public List<Student> select() {
        String sql = "SELECT id, name FROM student"; // 列舉 column (id, name)

        Map<String, Object> map = new HashMap<>();

        List<Student> list = namedParameterJdbcTemplate.query(sql, map, new StudentRowMapper());

        return list;
    }
}
```

### rowMapper

```java
@Override
public Student mapRow(ResultSet resultSet, int i) throws SQLException {
    return null;
}
```

- `Student`: 想要轉換成什麼類型的 Java object
- `resultSet`: 從資料庫中取得的數據
- `i`: 取到第幾筆數據

```java
public class StudentRowMapper implements RowMapper<Student> {

    @Override
    public Student mapRow(ResultSet resultSet, int i) throws SQLException {

        // 從資料庫中取得數據
        Integer a = resultSet.getInt("id");
        String b = resultSet.getString("name");

        // 將數據轉為 Java object
        Student student = new Student();
        student.setId(a);
        student.setName(b);

        /* 同上效果一樣
        Student student = new Student();
        student.setId(resultSet.getInt("id"));
        student.setName(resultSet.getString("name"));
        */

        return student;
    }
}
```

變化題

```sql
SELECT id AS student_id FROM student
```

```java
// 從資料庫中取得數據
resultSet.getInt("student_id");
```