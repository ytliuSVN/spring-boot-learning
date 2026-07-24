# 單元 8 - 取得請求參數（二）@RequestBody

### @RequestBody

- 用法：只能加在方法的參數上
- 用途：取得 request body 裡面的參數（將 Json 轉為 Java object）
- 多傳自動忽略、少傳補 `null`

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

```java
@RestController
public class MyController {

    @RequestMapping("/test2")
    public String test2(@RequestBody Student student) { // 將 Json 轉為 Java object
        System.out.println("id: " + student.getId());
        System.out.println("name: " + student.getName());
        return "Hello test2";
    }
}
```