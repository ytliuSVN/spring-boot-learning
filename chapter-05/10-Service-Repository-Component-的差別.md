# 單元 10 - @Service、@Repository、@Component 的差別

### Controller-Service-Dao 三層式架構

實際運作的效果相同，都是產生一個 bean

|  | 寫法一：<br>除了 `Controller` 層之外，其他都是 `@Component` | 寫法二：<br>每一層都有專屬的註解可以使用 |
| --- | --- | --- |
| Controller | `@RestController` | `@RestController` |
| Service | `@Component` | `@Service` |
| Dao<br>(Data Access Object) | `@Component` | `@Repository` |

```java
@Repository
public class StudentDaolmpl implements StudentDao {
```

```java
@Service
public class StudentServicelmpl implements StudentService {
```