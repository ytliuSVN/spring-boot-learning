# 單元 4 - 使用 CrudRepository 執行資料庫的 CRUD 操作

### Spring Data JPA 提供的 Interface

```text
+-------------------------------+
|        CrudRepository         |  <--- 基本的 CRUD 操作
+-------------------------------+
                ^
                | 繼承
+-------------------------------+
| PagingAndSortingRepository    |  <--- 新增分頁和排序的操作
+-------------------------------+
                ^
                | 繼承
+-------------------------------+
|         JpaRepository         |  <--- 能力最強，新增了 JPA 相關的 flush 操作
+-------------------------------+
```

去查看由 Spring Data JPA 所自動生成的 SQL 語法

application.properties

```properties
spring.jpa.show-sql=true
```

### Create

```java
@PostMapping("/students")
public String insert(@RequestBody Student student) {

    studentRepository.save(student);

    return "執行資料庫的 Create 操作";
}
```

### Update

```java
@PutMapping("/students/{studentId}")
public String update(@PathVariable Integer studentId,
                     @RequestBody Student student) {

    student.setId(studentId);  // 避免誤以為這是一筆新資料
    studentRepository.save(student);

    return "執行資料庫的 Update 操作";
}
```

通常實務上會搭配 `findById()` 先確認資料到底存不存在

```java
@PutMapping("/students/{studentId}")
public String update(@PathVariable Integer studentId,
                     @RequestBody Student student) {

    Student s = studentRepository.findById(studentId).orElse(null);

    if (s != null) {
        s.setName(student.getName());
        studentRepository.save(s);

        return "執行資料庫的 Update 操作";
    } else {
        return "Update 失敗，數據不存在";
    }
}
```

### Delete

```java
@DeleteMapping("/students/{studentId}")
public String delete(@PathVariable Integer studentId) {

    studentRepository.deleteById(studentId);

    return "執行資料庫的 Delete 操作";
}
```

### Read

`findById` 回傳的是 `Optional<T>`

```java
@GetMapping("/students/{studentId}")
public Student read(@PathVariable Integer studentId) {

    Student student = studentRepository.findById(studentId).orElse(null);

    return student;
}
```
