# 單元 7 - 撰寫 Controller 層測試 (上) – MockMvc

## Controller 層的測試

* 目的：模擬前端的行為，測試 API 是否運行正確
* 不能直接注入 bean 來測試，需要透過模擬真實的 API call 來測試

## MockMvc

* 用途：模擬真實的 API call

在測試用的 class 上加上 `@SpringBootTest` 和 `@AutoConfigureMockMvc`
注入 `MockMvc`

```java
@SpringBootTest
@AutoConfigureMockMvc
public class StudentControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void getById() throws Exception {
        // build request
        RequestBuilder requestBuilder = MockMvcRequestBuilders
                .get("/students/3");

        // send request and verify response
        mockMvc.perform(requestBuilder)
                .andExpect(MockMvcResultMatchers.status().is(200));
    }
}
```

## MockMvc 主體架構

* RequestBuilder：創建 Http request，設定 url 路徑、請求參數、header
* mockMvc.perform()：執行 Http request
* `andDo()`, `andExpect()`, `andReturn()`：處理 Http response，輸出結果、驗證結果、取得結果