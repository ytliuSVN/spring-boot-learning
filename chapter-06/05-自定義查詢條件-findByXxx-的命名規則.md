# 單元 5 - 自定義查詢條件 - findByXxx 的命名規則

Spring Data JPA 會自動生成相對應的 SQL 語法

```java
public interface StudentRepository extends CrudRepository<Student, Integer> {

    // SELECT * FROM Student WHERE name = ?
    List<Student> findByName(String name);
}
```

返回的類型可以自定，通常是返回 `Student` 或是 `List<Student>`

```java
public interface StudentRepository extends CrudRepository<Student, Integer> {

    // SELECT * FROM Student WHERE id = ? AND name = ?
    Student findByIdAndName(Integer id, String name);
}
```

參數按照順位傳進去，參數名字不重要