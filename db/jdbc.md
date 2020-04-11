# setAutoCommit
当进行 jdbc 批量数据插入时，应关闭自动提交模式，即设置`conn.setAutoCommit(false)`，执行完sql后再手动提交事务。
> 在自动提交模式下，每个sql将被当做**单个事务**进行提交（每执行一个sql就会被自动提交到db）。

```java
conn.setAutoCommit(false);
ps = conn.prepareStatement(sql);
...
ps.addBatch();
ps.executeBatch();
conn.commit();
```
