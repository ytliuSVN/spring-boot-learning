# 單元 5 - 使用 NamedParameterJdbcTemplate（二）- update 的進階用法

`update()` 的進階用法

1. 當 table 的 id 會自動增加時，要如何去取得 id 的值
    - 使用 KeyHolder
2. 要如何大量的執行一批 INSERT/UPDATE/DELETE sql
    - 使用 `batchUpdate()` 方法

### AUTO_INCREMENT

```java
CREATE TABLE student (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(30)
)
```

### KeyHolder

去取得 MySQL 為這筆數據所自動生成的 id

```java
@RestController
public class StudentController {

    @Autowired
    private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

    @PostMapping("/students")
    public String insert(@RequestBody Student student) {
        String sql = "INSERT INTO student(name) VALUE (:studentName)";

        Map<String, Object> map = new HashMap<>();
        map.put("studentName", student.getName());

        KeyHolder keyHolder = new GeneratedKeyHolder();

        namedParameterJdbcTemplate.update(sql, new MapSqlParameterSource(map), keyHolder);

        int id = keyHolder.getKey().intValue();

        System.out.println("mysql 自動生成的 id 為: " + id);

        return "執行 INSERT sql";
    }
}
```

```java
// 1. 資料庫欄位為 INT AUTO_INCREMENT
int id = keyHolder.getKey().intValue();

// 2. 資料庫欄位為 BIGINT (或 LONG) AUTO_INCREMENT
long id = keyHolder.getKey().longValue();
```

### batchUpdate

使用 `batchUpdate`（批次更新）比循環調用單一的 `update()` 效率高出許多

```java
@PostMapping("/students/batch")
public String insertList(@RequestBody List<Student> studentList) {
    String sql = "INSERT INTO student(name) VALUE (:studentName)";

    MapSqlParameterSource[] parameterSources = new MapSqlParameterSource[studentList.size()];

    for (int i=0; i<studentList.size(); i++) {
        Student student = studentList.get(i);

        parameterSources[i] = new MapSqlParameterSource();
        parameterSources[i].addValue("studentName", student.getName());
    }

    namedParameterJdbcTemplate.batchUpdate(sql, parameterSources);

    return "執行一批 INSERT sql";
}
```

```json
[
  {
    "name": "test1"
  },
  {
    "name": "test2"
  },
  {
    "name": "test3"
  }
]
```