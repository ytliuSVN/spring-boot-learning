# 單元 3 - 第一個 Spring Data JPA 程式

```sql
CREATE DATABASE myjpa

CREATE TABLE student (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(30)
)
```

創建一個 Java class 可以和 Student table 去一一對應

```java
@Entity
@Table(name = "student")
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    Integer id;

    @Column(name = "name")
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

在 Spring Data JPA 的 `CrudRepository<T, ID>` 中，兩個泛型參數分別代表：

1. **`T`**：對應的 Entity 實體類別（Class）
2. **`ID`**：該 Entity 的 主鍵（Primary Key, `@Id`）資料型態

```java
public interface StudentRepository extends CrudRepository<Student, Integer> {
}
```

`save` 方法可以同時包辦新增還有修改

```java
@RestController
public class StudentController {

    @Autowired
    private StudentRepository studentRepository;

    @PostMapping("/students")
    public String insert(@RequestBody Student student) {

        studentRepository.save(student);

        return "執行資料庫的 Create 操作";
    }
}
```