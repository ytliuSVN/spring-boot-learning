# 單元 4 - 結構化的呈現數據 Json

```java
// Pet.java
public class Pet {
    String name;
    Integer age;
}
```

```java
// Student.java
public class Student {
    Integer id;
    String name;
    Double store;
    boolean graduated;
    Integer age;
    List<String> courseList;
    Pet pet;
    List<Pet> petList;
}
```

```json
// test.json
{
  "id": 123,
  "name": "Judy",
  "score": 95.5,
  "graduated": true,
  "age": null,
  "courseList": ["math", "english"],
  "pet": {
    "name": "black",
    "age": 5
  },
  "petList": [
    {
      "name": "white",
      "age": 3
    },
    {
      "name": "orange",
      "age": 1
    }
  ]
}
```

### Json 轉換練習

人類語言

> 第一個是蘋果、第二個是橘子
>

```java
public class Store {
    List<String> productList;
}

```

```json
{
	"productList"：［"蘋果"，"橘子"］
}
```