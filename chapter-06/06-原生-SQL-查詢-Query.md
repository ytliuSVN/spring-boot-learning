# 單元 6 - 原生 SQL 查詢 - @Query

### @Query

- 目的：用來解決 `findByXxx` 無法寫出複雑的査詢邏輯的問題
- 用途：在 Spring Data JPA 中，執行原生的 SQL 語法
- 在問號後面加上數字，指定要載入第幾個參數的值
- `nativeQuery = true`：一般的 SQL語法; `false`: `JPQL`

```java
public interface StudentRepository extends CrudRepository<Student, Integer> {

    @Query(value = "SELECT id, name FROM student WHERE id = ?1 AND name = ?2", nativeQuery = true)
    Student test1(Integer id, String name);
}
```

### @Query vs findByXxx

- 優先使用 `findByXxx` 的命名規則
- 複雜的邏輯才使用 `@Query`