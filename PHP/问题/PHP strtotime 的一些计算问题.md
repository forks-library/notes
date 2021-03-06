> 转摘：[PHP 获取周一，上个月的正确做法](https://www.tuicool.com/articles/vEbuIvQ)

### 日期不存在的问题

`strtotime()`方法可以对一个基础日期进行处理，从而得到另一个日期，但是计算时可能得到的结果并非预期。

如下：

```php
$now = strtotime('2018-01-31');
echo date('Y-m-d', strtotime('+1 month', $now));
```

这是计算 2018-01-31 下一个月的日期，本应该是 2 月某一天，但会得到 2018-03-03。

这是由于，增加一个月时会得到 2018-02-31 这个结果，但是由于 2018 年 2 月只有 28 天，所以这个结果是不存在的日期，会被自动修正为对应的 2018-03-03。

### 周一问题

`strtotime()`在计算星期的时候，认为周日是一周的开始，而不是按照 ISO-8601 标准认为，周一才是一周的开始。所以在使用`strtotime()`计算下周、上周等情况的时候，结果会不是预期的结果。

比如：

```php
$now = strtotime('2018-05-20'); // 这一天是周日
echo date('Y-m-d', strtotime('this monday', $now));
```

2018-05-20 这一天是周日，预期得到的结果应该 2018-05-14，但得到的却是 2018-05-21，也就是下一个周一。

获取本周一的正确方式应该是：

```php
$now = strtotime('2018-05-20');
// 先计算当前是周几，再减去相应的天数，就得到对应的本周一的时间戳了
$time = $now - 86400 * (date('N', $now) - 1);
echo date('Y-m-d', $time) . "\n"; // 2018-05-14

// 以本周一为基础，求出 3 周以前的那个周一
strtotime('-3 week', $time);
```


