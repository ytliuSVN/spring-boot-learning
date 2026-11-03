# 單元 6 - 撰寫 Service 層、Dao 層測試 – @SpringBootTest、@Transactional

## 使用 JUnit 5 測試 Spring Boot 程式

* 只要在測試的 class 上加上 `@SpringBootTest`，則在運行單元測試時，Spring Boot 就會去啟動 Spring 容器，創建所有的 bean 出來

## 撰寫 DAO 層單元測試

src/test/java/com/example/demo/dao/StudentDaoImplTest.java

```java
@SpringBootTest
public class StudentDaoImplTest {

    @Autowired
    private StudentDao studentDao;

    @Test
    public void getById() {
       Student student = studentDao.getById(1);
       assertNotNull(student);
       assertEquals("Amy", student.getName());
       assertEquals(90.3, student.getScore());
       assertTrue(student.isGraduate());
       assertNotNull(student.getCreateDate());
    }
}
```

## `@Transactional`（for 單元測試）

* 用法：可以加在方法上、也可以加在 class 上
* 用途：在單元測試結束後，rollback 所有資料庫操作，將數據恢復原狀

```java
@Transactional
@Test
public void deleteById() {
    studentDao.deleteById(3);
    Student student = studentDao.getById(3);
    assertNull(student);
}

@Test
@Transactional
public void insert() {
    Student student = new Student();
    student.setName("Kevin");
    student.setScore(66.2);
    student.setGraduate(true);

    Integer studentId = studentDao.insert(student);

    Student result = studentDao.getById(studentId);
    assertNotNull(result);
    assertEquals("Kevin", result.getName());
    assertEquals(66.2, result.getScore());
    assertTrue(result.isGraduate());
    assertNotNull(result.getCreateDate());
}

@Test
@Transactional
public void update() {
    Student student = studentDao.getById(3);
    student.setName("John");

    studentDao.update(student);

    Student result = studentDao.getById(3);
    assertNotNull(result);
    assertEquals("John", result.getName());
}
```

## 意義不同的 `@Transactional`

- `@Transactional` 在 main 資料夾（正常程式）
    - 交易管理
    - 程式運行中途發生錯誤的話，才 rollback 已經執行的資料庫操作，將數據恢復原狀

- `@Transactional` 在 test 資料夾（單元測試）
    - 在該單元測試結束後，強制 rollback 所有執行的資料庫操作，將數據恢復原狀
