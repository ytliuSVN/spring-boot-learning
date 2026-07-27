# 單元 1 - Spring JDBC 簡介

### Spring Boot 操作資料庫的方式

- 第 5 章節：Spring JDBC
    - 在 Spring Boot 中執行原始的SQL 語法，去操作資料庫
- 第 6 章節：Spring Data JPA
    - 使用 ORM 的概念，透過操作 Java object 的方式，去操作資料庫

### 資料庫的 CRUD

CRUD 是 Create、Read、Update、Delete 操作的統稱，用以表示最基礎的資料庫操作

| 資料庫操作 | 對應的 sql 語法 | 對應的 Http method | 說明 |
| --- | --- | --- | --- |
| Create（新増） | INSERT sql | POST | 新增一個資源 |
| Read（查詢） | SELECT sql | GET | 取得一個資源 |
| Update（修改） | UPDATE sql | PUT | 更新一個已存在的資源 |
| Delete（刪除） | DELETE sql | DELETE | 刪除一個資 |

補充：比較進階的實作

- 如何處理 同時間、高流量 湧入的問題？
- 如何加快資料庫的查詢效能？