# 單元 16 - 攔截器 Interceptor

### Override methods `preHandle`

撰寫攔截器

```java
@Component
public class MyInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("執行 MyInterceptor 的 preHandle 方法");
        return true; // 攔截器允許這個 http request 通過
    }
}
```

指定這個攔截器要套用到哪一些 url 路徑上面

```java
@Configuration
public class MyConfig implements WebMvcConfigurer {

    @Autowired
    private MyInterceptor myInterceptor;

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(myInterceptor).addPathPatterns("/**");
    }
}
```

```java
@RestController
public class MyController {

    @RequestMapping("/test1")
    public String test1() {
        System.out.println("執行 test1 方法");
        return "Hello test1";
    }

    @RequestMapping("/test2")
    public String test2() {
        System.out.println("執行 test2 方法");
        return "Hello test2";
    }
}
```

Console

```markdown
執行 MyInterceptor 的 preHandle 方法
執行 test1 方法
```

---

在攔截器裡面去定義返回給前端的錯誤訊息，寫上一些身份驗證的程式

```java
@Component
public class MyInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("執行 MyInterceptor 的 preHandle 方法");

        response.setStatus(401); // 401 Unauthorized
        return false;
    }
}
```