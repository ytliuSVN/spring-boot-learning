# 單元 8 - MVC 架構模式 - Controller-Service-Dao 三層式架構

### MVC 架構模式（Model-View-Controller）

- Model： 負責業務邏輯、數據處理
- View： 使用 Html 模板呈現數據，但近幾年因為前後端分離的關係，多數使用 Json 格式傳遞數據
- Controller： 負責轉發 Http request

### MVC 架構模式 in Spring Boot

- MVC 架構模式是抽象的概念
- 實際套用到 Spring Boot 時，會轉化為 Controller-Service-Dao 三層式架構
    - Controller：負責接收 Http request ，並且驗證請求參數
    - Service：負責業務邏輯
    - Dao：負責和資料庫溝通

### 使用三層式架構之後

1. Class 的命名需要以 Controller、Service、或是 Dao 做結尾，用來表示這個 Class 是屬於哪一層
2. 將 Controller、Service、Dao 這些 Class 變成 Bean，並使用 `@Autowired` 注入
3. Controller 不能直接 call Dao，Controller 只能 call Service，再透過 Service 去 call Dao
4. Dao 只能去執行 sql，去存取資料庫內部的數據，不能添加任何業務邏輯