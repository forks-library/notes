`tr`命令可以对来自标准输入的字符进行替换、压缩和删除。它可以将一组字符替换成另一组字符，类似于各种编程语言中对字符的`replace`操作，但是会更强大。

### 1. 语法

```
tr <-Ccsuds> <string1> [string2]
```

常用方式如下：

```
tr [-Ccsu] string1 string2
tr [-Ccu] -d string1
tr [-Ccu] -s string1
tr [-Ccu] -ds string1 string2
```

### 2. 选项

* `-c` 替换所有不属于第一字符集合(`string1`)中的字符
* `-C` 同`-c`
* `-d` 删除所有属于第一字符集合(`string1`)中的字符
* `-s` 把连续重复的字符以单独一个字符表示
* `-u` 不缓存输出

### 3. 参数

* `string1` 字符集 1，指定要转换或删除的原字符集。
* `string2` 字符集 2，指定要转换成的目标字符集。当执行转换操作时，必须使用该参数指定转换的目标字符集。但执行删除操作时，不需要该参数。

字符集合是可以自己制定的，例如：`'ABD-}'`、`'bB.,`'、`'a-de-h'`、`'a-c0-9'`都属于集合，集合里可以使用`'\n'`、`'\t'`，可以可以使用其他 ASCII 字符。

对英文字母中间使用`-`符号，表示从起始字母到结束字母中间的全部字母集合，对数字中间使用`-`符号，表示从起始数字到结束数字中间的全部集合。如下：

* `a-z` 表示全部从字母`a`开始到`z`的全部 26 个小写英文字母。
* `1-9` 表示从 1 到 9 的 9 个数字。

### 4. 字符类

除了可以将一个个的指定字符，还可以使用字符类来表示某一种类别的字符，简化操作。`tr`支持的字符类如下：

* `[:alnum:]` 英文字母和数字
* `[:alpha:]` 英文字母
* `[:cntrl:]` 控制（非打印）字符
* `[:digit:]` 数字
* `[:graph:]` 图形字符
* `[:lower:]` 小写字母
* `[:print:]` 可打印字符
* `[:punct:]` 标点符号
* `[:space:]` 空白字符
* `[:upper:]` 大写字母
* `[:xdigit:]` 十六进制字符

比如，将标准输入中的小写字符变成大写，可以使用如下命令：

```shell
$ tr '[:lower:]' '[:upper:]'
Question
QUESTION
```

这样，当输入`Question`的时候，就可以输出为`QUESTION`。

### 5. 实例

**将输入字符由大写转换为小写**

```shell
echo "HELLO WORLD" | tr 'A-Z' 'a-z'  # 输出 hello world
```

**删除字符**

```shell
echo "hello 123 world 456" | tr -d '0-9' # 输出 hello  world 
```

**将制表符转换为空格**

```shell
cat text | tr '\t' ' '
```

**字符集补集，从输入文本中将不在补集中的所有字符删除**

```shell
echo "aa.,a 1 b#$bb 2 c*/cc 3 ddd 4" | tr -d -c '0-9 \n' # 输出 1  2  3  4
```

> 此例中，补集中包含了数字 0~9、空格和换行符`\n`，所以没有被删除，其他字符全部被删除了。

**压缩输入中重复的字符**

```shell
echo "thissss is      a text linnnnnnne." | tr -s ' sn' # 输出 this is a text line.
```
