## 一、简介

LIMIT 子句用来限制返回的结果的数量。其格式如下：

`LIMIT [位置偏移量]，行数`

其中，位置偏移量可以省略，省略时表示偏移量为 0，也就是从选择到的结果中的第一条进行选择；行数用来限制返回的结果的数量，也即是返回的结果最多不能超过指定的行数，当然，可以少于指定的行数。

> 注意：位置偏移量是从 0 开始计数的，也即是，0 表示从第一条结果开始选择。

```sql
SELECT * FROM fruits LIMIT 4,3
```

上面的语句表示，从选择到的结果中的第 5 条开始，选择 3 条结果返回。

MySQL 5.6 之后，可以使用`LIMIT pos OFFSET rows`的方式来选择结果，和前面的方式的意义是相同的。


