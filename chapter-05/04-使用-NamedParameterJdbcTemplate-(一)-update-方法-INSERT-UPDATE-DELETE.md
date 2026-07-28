# 單元 4 - 使用 NamedParameterJdbcTemplate（一）- update 方法（INSERT、UPDATE、DELETE）

由 Spring JDBC 自動創建 NamedParameterJdbcTemplate 的 bean

### NamedParameterJdbcTemplate

```java
update(String sql, Map‹String, Object> map)
```

1. `sql`: 放要執行的 sql 語法
2. `map`: 放 sql 語法裡面的變數的値

```java
public class Student {
    Integer id;
    String name;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

### INSERT

```java
@RestController
public class StudentController {

    @Autowired
    private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

    @PostMapping("/students")
    public String insert() {
        String sql = "INSERT INTO student(id, name) VALUE (3, 'John')";

        Map<String, Object> map = new HashMap<>();

        namedParameterJdbcTemplate.update(sql, map);

        return "執行 INSERT sql";
    }
}
```

動態決定 SQL 語法中的値

```java
@PostMapping("/students")
public String insert(@RequestBody Student student) {
    String sql = "INSERT INTO student(id, name) VALUE (:studentId, :studentName)";

    Map<String, Object> map = new HashMap<>();
    map.put("studentId", student.getId());
    map.put("studentName", student.getName());

    ...
}
```

### DELETE

```java
@DeleteMapping("/students/{studentId}")
public String delete(@PathVariable Integer studentId) {
    String sql = "DELETE FROM student WHERE id = :studentId";

    Map<String, Object> map = new HashMap<>();
    map.put("studentId", studentId);

    namedParameterJdbcTemplate.update(sql, map);

    return "執行 DELETE sql";
}
```