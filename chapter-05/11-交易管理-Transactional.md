# 單元 11 - 交易管理 - @Transactional

### 什麼是交易 (Transaction)

- 交易（Transaction） 是資料庫中的一種用法
- 用途：可以在一個交易裡包含多個資料庫操作，這些資料庫操作，會同時成功，否則就全部失敗
    - All or Nothing 原則
- Rollback
    - 當交易過程中發生失敗時，就會撤銷已執行的資料庫操作，確保數據恢復原狀

### @Transactional

- 用法：加在 class 上或方法上（通常是加在方法上）
    - 交易的英文為 Transaction，加上 al 變成形容詞，形容這是一個具有交易特性的方法
    - 通常用在 `Service` 層上面
- 用途：使用交易來管理這個方法中的資料庫操作

```java
@Component
public class AccountServiceImpl implements AccountService {

    @Autowired
    private AccountDao accountDao;

    @Transactional
    @Override
    public void transfer(Integer fromAccountId, Integer toAccountId, Integer money) {

        // User A 扣除轉帳金額
        accountDao.decreaseMoney(fromAccountId, money);

        // 失敗，噴出 exception
        Integer a = 1/0;

        // User B 收到轉入金額
        accountDao.addMoney(toAccountId, money);
    }
}
```

### 資料庫中的 ACID

滿足 ACID 特性的資料庫，才能夠執行交易管理

| 特性 | 描述 |
| --- | --- |
| Atomicity（原子性） | 交易是一個不可被分割的單元 |
| Consistency（一致性） | 交易執行的前後，數據的完整性必須保持一致 |
| Isolation（隔離性） | 資料庫同時處理多個交易時，一個交易的執行不應該去影響其他交易的執行 |
| Durability（永久性） | 交易一旦提交之後，其對資料庫所做的改變永久有效，不會因為系統重啟或錯誤而改變 |