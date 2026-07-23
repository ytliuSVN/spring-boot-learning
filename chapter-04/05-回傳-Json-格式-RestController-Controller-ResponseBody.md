# 單元 5 - 回傳 Json 格式 - @RestController、@Controller + @ResponseBody

### @Controller/@RestController

- 用法：只能加在 class 上
- 用途：將該 class 變成 bean，並且可以使用 `@RequestMapping`
    - 可以想像成 `@Component` 的加強版

```java
@RestController // 另一種可以創建 bean 的註解
public class MyController {

    @RequestMapping("/test")
    public String test() {
        return "Hello World";
    }
}
```

在 response body 中返回 Json 格式

### @Controller + @ResponseBody

每個方法上都必須得加上 `@ResponseBody` 註解 (比較舊的 project)

```java
@Controller
public class MyController {

    @ResponseBody
    @RequestMapping("/product")
    public String product() {
        return "第一個是蘋果，第二個是橘子";
    }

    @ResponseBody
    @RequestMapping("/user")
    public String user() {
        return "名字為Judy";
    }
}
```

### @RestController

```java
@RestController
public class MyController {

    @RequestMapping("/product")
    public String product() {
        return "第一個是蘋果，第二個是橘子";
    }

    @RequestMapping("/user")
    public String user() {
        return "名字為Judy";
    }
}
```

### 練習一

```json
{
    "id": null,
    "name": "Judy"
}

```

```java
// Student.java
public class Student {
    String name;
    Integer id;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }
}
```

Spring Boot 使用 Jackson library 轉換 Java class 和 Json 格式

```java
@RestController
public class MyController {

    @RequestMapping("/user")
    public Student user() { // 返回類型是自定義的 class
        Student student = new Student();
        student.setName("Judy");
        return student; // Java class 轉換成 Json 格式
    }
}
```

### 練習二

```json
{
    "productList": [
        "蘋果",
        "橘子"
    ]
}
```

```java
// Store.java
public class Store {
    List<String> productList;

    public List<String> getProductList() {
        return productList;
    }

    public void setProductList(List<String> productList) {
        this.productList = productList;
    }
}
```

```java
public class MyController {

    @RequestMapping("/product")
    public Store product() {
        Store store = new Store();
        List<String> list = new ArrayList<>();
        list.add("蘋果");
        list.add("橘子");
        store.setProductList(list);
        return store;
    }
}
```