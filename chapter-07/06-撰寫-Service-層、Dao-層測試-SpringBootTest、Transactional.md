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
    }
}
```