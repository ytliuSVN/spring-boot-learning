# 單元 13 - 驗證請求參數 - @Valid、@Validated、@NotNull…

```java
@PostMapping("/students")
public String create(@RequestBody Student student) {
    if(student.getId() == null) { // 寫法冗長
        throw new RuntimeException("id 不可為 null");
    }
    return "執行資料庫的 Create 操作";
}
```

### @Valid

使用 `@RequestBody` 時，要在該參數上加上 `@Valid` 註解，才能讓這個 class 裡的驗證請求參數的註解生效

```java
@PostMapping("/students")
public String create(@RequestBody @Valid Student student) {
    return "執行資料庫的 Create 操作";
}
```

### @NotNull

使用驗證請求參數的註解需要在 `pom.xml` 額外設定

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

```java
public class Student {

    @NotNull
    Integer id;

    // 省略 getter and setter
```

### Spring Boot 中驗證請求參數的註解（上）

| 註解 | 詳細資訊 |
| --- | --- |
| `@NotNull` | 不能為 null |
| `@NotBlank` | 不能為null、且不能為空白的字串，用在驗證 String 類型的參數上 |
| `@NotEmpty` | 不能為 null、且size 必須>0，用在驗證集合類型（List、Set、Map）的參數上 |
| `@Min(value)` | 值必須>=value，用在驗證數字類型的參數上 |
| `@Max(value)` | 值必須<=value，用在驗證數字類型的參數上 |

### @NotBlank

```java
public class Student {

    @NotBlank
    String name;

    // 省略 getter and setter
```

### @NotEmpty

```java
public class Student {

    @NotEmpty
    List<String> courseList;

    // 省略 getter and setter
```

```json
{
  "id": 123,
  "name": "Judy",
  "courseList": ["math"]
}
```

### @Min(value)

```java
public class Student {

    @NotNull // 順序不影響
    @Min(100)
    Integer id;

    // 省略 getter and setter
```

```json
{
  "id": 150,
  "name": "Judy"
}
```

### Spring Boot 中驗證請求參數的註解（下）

| 註解 | 詳細資訊 |
| --- | --- |
| `@Size(min, max)` | min <= 字串長度 or 集合的 size <=max，可以只設 max or min |
| `@Email` | 必須符合電子郵件的格式 |
| `@Pattern(regexp)` | 必須符合正規表達式 regexp |
| `@Past` | 必須比當前時間早，也就是被註解的參數必須是以前的時間 |
| `@Future` | 必須比當前時間晚，也就是被註解的參數必須是未來的時間 |
| `@AssertTrue` | 必須為 true，用在驗證 boolean 類型的參數上 |
| `@AssertFalse` | 必須為 false，用在驗證 boolean 類型的參數上 |
| `@Null` | 必須為 null |

---

### @Validated

使用以下三種註解時

- `@RequestParam`
- `@RequestHeader`
- `@PathVariable`

需要在 Controller 上加上 @Validated 註解，才能夠讓驗證請求參數的註解生效

```java
@RestController
@Validated
public class StudentController {

    @GetMapping("/students/{studentId}")
    public String read(@PathVariable @Min(100) Integer studentId) {
        return "執行資料庫的 Read 操作";
    }
```