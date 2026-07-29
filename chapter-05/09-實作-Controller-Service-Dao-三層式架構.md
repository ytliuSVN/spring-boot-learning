# 單元 9 - 實作 Controller-Service-Dao 三層式架構

New Package，使用小寫英文來命名

- controller
- service (New Java Class → `interface`)
- dao (New Java Class → `interface`)
    - Data Access Object (DAO)
- model
- mapper

### dao

根據 `studentld` 的値，去查詢資料庫裡面的數據

方法的命名沒有硬性規定，開頭使用 `find`、`query`、`get` 均可

```java
public interface StudentDao {

    Student getById(Integer studentId);
}
```

`lmpl`：Implement 的縮寫

```java
@Component
public class StudentDaolmpl implements StudentDao {

    @Autowired
    private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

    @Override
    public Student getById(Integer studentId) {
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
}
```

### service

```java
public interface StudentService {

    Student getById(Integer studentId);
}
```

```java
@Component
public class StudentServicelmpl implements StudentService {

    // 使用 Interface 作為變數類型
    @Autowired
    private StudentDao studentDao;

    @Override
    public Student getById(Integer studentId) {
        return studentDao.getById(studentId);
    }
}
```

### controller

```java
@RestController
public class StudentController {

    @Autowired
    private StudentService studentService;

    @GetMapping("/students/{studentId}")
    public Student select(@PathVariable Integer studentId) {
        return studentService.getById(studentId);
    }
}
```