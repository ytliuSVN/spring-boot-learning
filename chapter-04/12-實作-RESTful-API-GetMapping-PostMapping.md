# 單元 12 - 實作 RESTful API - @GetMapping、@PostMapping…

設計 Student 的 RESTful API

| Http method | url 路徑 | 對應到資料庫 | 意義 |
| --- | --- | --- | --- |
| POST | /students | Create | 創建一個新的 student |
| GET | /students/123 | Read | 查詢 student id 為123的資訊 |
| PUT | /students/123 | Update | 更新 student id 為123的資訊 |
| DELETE | /students/123 | Delete | 刪除 student id 為123的 student |

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

### POST /students

限制前端只能夠使用 `POST` 方法，來請求這個 url 路徑 `/students`

```java
@RestController
public class StudentController {

    @PostMapping("/students") // 建議寫法
    // @RequestMapping(value = "/students", method = RequestMethod.POST)
    public String create(@RequestBody Student student) {
        return "執行資料庫的 Create 操作";
    }
}
```

### GET /students/123

```java
@RestController
public class StudentController {

    @GetMapping("/students/{studentId}")
    public String read(@PathVariable Integer studentId) {
        return "執行資料庫的 Read 操作";
    }
}
```

### PUT /students/123

```java
@RestController
public class StudentController {

    @PutMapping("/students/{studentId}")
    public String update(@PathVariable Integer studentId,
                         @RequestBody Student student) { // 可混用
        return "執行資料庫的 Update 操作";
    }
}
```

### DELETE /students/123

```java
@RestController
public class StudentController {

    @DeleteMapping("/students/{studentId}")
    public String delete(@PathVariable Integer studentId) {
        return "執行資料庫的 Delete 操作";
    }
}
```