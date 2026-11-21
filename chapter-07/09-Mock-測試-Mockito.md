# 單元 9 - Mock 測試 – Mockito

## Mock 測試

- 目的：避免為了測試某一個單元測試，而去構建了整個 bean 的 dependency
- 做法：創造一個假的 bean，去替換掉 Spring 容器中原有的 bean

```mermaid
flowchart LR
    A(["Bean A"])
    B(["Mock Bean B"])
    C["使用 Mock Bean 返回<br/>指定的結果，專注在<br/>測試 Bean A 的邏輯"]
    D["想要測試 Bean A<br/>的實作是否正確"]

    A --> B
    B --- C
    D --> A

    classDef bean fill:#DCE5F5,stroke:#5479B9,stroke-width:2px,color:#000
    classDef mock fill:#D3D3D3,stroke:#222,stroke-width:2px,color:#000
    classDef note fill:transparent,stroke:transparent,color:#D22
    classDef description fill:transparent,stroke:transparent,color:#5479B9

    class A bean
    class B mock
    class C note
    class D description

    linkStyle 1 stroke:transparent
```

## Mockito

- Mockito 是在 Spring Boot 中進行 Mock 測試的工具
- 功能：
    - 模擬方法的返回值
    - 模擬拋出 Exception
    - 記錄方法的使用次數、順序

src/test/java/com/example/demo/service/StudentServiceImplMockTest.java

```java
@SpringBootTest
public class StudentServiceImplMockTest {

    @Autowired
    private StudentService studentService;

    @MockBean
    private StudentDao studentDao;

    @Test
    public void getById() {
        Student mockStudent = new Student();
        mockStudent.setId(100);
        mockStudent.setName("I'm mock");

        // Mockito.when(studentDao.getById(3)).thenReturn(mockStudent);
        // another way to mock for widely use, any() means any parameter, not just 3
        Mockito.when(studentDao.getById(Mockito.any())).thenReturn(mockStudent);

        Student student = studentService.getById(3);
        assertNotNull(student);
        assertEquals(100, student.getId());
        assertEquals("I'm mock", student.getName());
    }
}
```

## @BeforeEach

每個 `@Test` 執行前都會執行一次建立 Mock 物件，讓每個測試都能使用相同的初始化設定。

```java
@SpringBootTest
public class StudentServiceImplMockTest {

    @Autowired
    private StudentService studentService;

    @MockBean
    private StudentDao studentDao;

    @BeforeEach
    public void setupMockStudent() {
        Student mockStudent = new Student();
        mockStudent.setId(100);
        mockStudent.setName("I'm mock");

        // Mockito.when(studentDao.getById(3)).thenReturn(mockStudent);
        // another way to mock for widely use, any() means any parameter, not just 3

        // 第一種寫法 when...thenReturn
        // Mockito.when(studentDao.getById(Mockito.any())).thenReturn(mockStudent);
        // 第二種寫法 doReturn...when
        Mockito.doReturn(mockStudent).when(studentDao).getById(Mockito.any());
    }

    @Test
    public void getById() {
        Student student = studentService.getById(3);
        assertNotNull(student);
        assertEquals(100, student.getId());
        assertEquals("I'm mock", student.getName());
    }

    @Test
    public void getById2() {
        Student student = studentService.getById(3);
        assertNotNull(student);
        assertEquals(100, student.getId());
        assertEquals("I'm mock", student.getName());
    }
}
```

## Mockito 的用法

- `@MockBean`：產生一個假的 bean，替換掉 Spring 容器中的 bean
    - 沒有定義的方法，預設返回 null
- 模擬方法的返回值

```java
Student mockStudent = new Student();
mockStudent.setId(100);
mockStudent.setName("I'm mock");

// 第一種寫法 when...thenReturn
// Mockito.when(studentDao.getById(Mockito.any())).thenReturn(mockStudent);

// 第二種寫法 doReturn...when
Mockito.doReturn(mockStudent).when(studentDao).getById(Mockito.any());
```

- 模擬噴出 Exception

```java
// 方法不返回 void 的寫法 when...thenThrow
Mockito.when(studentDao.insert(Mockito.any())).thenThrow(new RuntimeException());

// 方法返回為 void 的寫法 doThrow...when...
Mockito.doThrow(new RuntimeException()).when(studentDao).deleteById(Mockito.any());
```

- 紀錄方法的使用次數,順序

```java
Mockito.verify(studentDao, Mockito.times(2)).getById(Mockito.any());
```

- 限制：
    - 不能 mock `static` 方法
        - 不需要 `new`，可以直接透過 `Class.method()` 呼叫。
    - 不能 mock `private` 方法
    - 不能 mock `final class` 方法
        - 禁止被繼承