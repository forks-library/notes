### 1. 数据结构

Redis 使用动态字符串 SDS 来表示字符串值，使用`sdshdr`数据结构：

```c
struct sdshdr{

    // 字节数组，用于保存字符串
    char buf[];

    // 记录 buf 数组中已使用的字节数量，也是字符串的长度
    int len;

    // 记录 buf 数组未使用的字节数量
    int free;
} sdshdr;
```

示意图：

![](http://cnd.qiniu.lin07ux.cn/markdown/1558799609988.png)

### 2. 特点

SDS 的好处如下：

1.	`sdshdr`数据结构中用`len`属性记录了字符串的长度。获取字符串的长度时，时间复杂度为`O(1)`。
2.	SDS **不会发生溢出**的问题，如果修改 SDS 时空间不足，先会扩展空间，再进行修改(内部实现了**动态扩展**机制)。
3.	SDS 可以**减少内存分配的次数** (空间预分配机制)。在扩展空间时，除了分配修改时所必要的空间，还会分配额外的空闲空间(free 属性)。
4.	SDS 是**二进制安全**的 ，所有 SDS API 都会以处理二进制的方式来处理 SDS 存放在 buf 数组里的数据。

SDS 的动态扩展和预分配内存机制如下：

* 如果修改后，SDS 的长度(也就是`len`属性的值)将小于 1MB，那么 Redis 预分配和`len`属性相同大小的未使用空间。
* 如果修改后，SDS 的长度将大于 1MB ，那么 Redis 会分配 1MB 的未使用空间。 
类似的，当 SDS 缩短其保存的字符串长度时，并不会立即释放多出来的字节，而是等待之后使用。


