# 單元 7 - 使用 NamedParameterJdbcTemplate（四）- query 和 queryForObject 的差別

query 和 queryForObject 的差別

#### query() 方法

- 返回値是一個 `List`，裡面可能會有 0 個、1 個、或是 N 個以上 數據
- 適合用在所有使用 `SELECT` sql 査詢的情境

```java
@GetMapping("/students/{studentId}")
public Student select(@PathVariable Integer studentId) {
    String sql = "SELECT id, name FROM student WHERE id = :studentId";

    Map<String, Object> map = new HashMap<>();
    map.put("studentId", studentId);

    List<Student> list = namedParameterJdbcTemplate.query(sql, map, new StudentRowMapper());

    if (list.size() > 0) {
        return list.get(0);
    } else {
        return null;
    }
}
```

#### queryForObject() 方法

- 返回值是一個 java object
- 僅適合用在 `SELECT count(*)`

```java
@GetMapping("/students/{studentId}")
public Student select(@PathVariable Integer studentId) {

    String countSql = "SELECT count(*) FROM student";

    Map<String, Object> countMap = new HashMap<>();

    Integer count = namedParameterJdbcTemplate.queryForObject(countSql, countMap, Integer.class);

    System.out.println("student table 中的總數是: " + count);

    ...
```