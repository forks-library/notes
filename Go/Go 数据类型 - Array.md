数组具有固定的长度、可以容纳固定类型元素的数据结构。

### 1. 数组的长度

数组的长度是在声明时就确定的固定值。可以通过显示声明长度，也可以由 Go 自动推断长度：

* `[N]type{value1, value2, ..., valueN}` 声明长度
* `[...]type{value1, value2, ..., valueN}` 自动推断

比如：

```go
numbers := [5]int{1, 2, 3, 4, 5}
numbers := [...]int{1, 2, 3, 4, 5}
```

### 2. 数组的类型

数组的大小也属于类型的一部分。如果尝试将`[4]int`类型的变量作为`[5]int`类型的参数传入函数，是不能通过编译的，因为他们是不同的类型，就像尝试将`string`当做`int`类型的参数传入函数一样。

因为这个原因，所以数组比较笨重，大多数情况下都不会使用它。

而 Go 的切片(slice)类型不会将集合的长度保存在类型中，因此其尺寸也就可以是不固定的。

### 3. 数组循环

数据可以使用`for`语句进行循环，并使用`array[index]`语法来访问数组中指定索引对应的值。

还可以使用`range`语法来迭代数组中的每一个值。每次迭代都会返回数组元素的索引和值。

> 如果不需要使用索引，可以使用`_`空白标识符来忽略索引。

```go
for _, number := range numbers {
    //
}
```

