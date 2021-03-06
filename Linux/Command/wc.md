`wc`是 Linux 系统中的一个统计工具，可以用于统计每个输入文件内容的行数、词数、字符数、Bytes 数。

### 1. 语法

语法如下：

```shell
wc [-clmw][--help][--version][文件...]
```

### 2. 选项

* `-c` 统计字节数，如果还指定了`-m`参数，则该参数不起作用。
* `-l` 统计行数。
* `-m` 统计字符数。这个标志不能与`-c`标志一起使用。非 ASCII 字符会被当做多个字符。
* `-w` 统计字词数。一个字词被定义为由空白、跳格或换行字符分隔的字符串。

需要注意的是，`-w`统计的字词并非常见意义中的词，必须要通过这三种空白符号分隔才会被作为不同的字词，而且对于非 ASCII 内容进行字词统计常会有不符合预期的情况。比如，中文的`你好`会被作为两个词，而`你好吗`依旧是两个词。

### 3. 参数

`wc`命令可以一次提供零个或多个文件进行统计。如果没有提供文件，则默认统计标准输入中的内容。

### 4. 使用

有一个名为`test.txt`的文本文件，内容如下：

```
hnlinux
peida.cnblogs.com
ubuntu
ubuntu linux
redhat
Redhat
linuxmint
你好！
```

分别执行如下的命令：

```shell
wc -c test.txt  # 输出： 81 test.txt
wc -l test.txt  # 输出：  8 test.txt
wc -m test.txt  # 输出： 74 test.txt
wc -w test.txt  # 输出： 10 test.txt
```

这里由于有中文字符存在，所以统计结果会有点不太准确，如果没有最后一行中文，则统计结果依次为：70、7、70、8。

### 5. 技巧

**只输出统计数字不输出文件名**

使用 wc 命令对一个文件做统计的时候，会同时输出文件的名称，而直接从标准输入中进行统计则不会输出文件名。所以可以考虑使用管道来达成这个需求：

```shell
wc -l test.txt        # 输出：  8 test.txt
cat test.txt | wc -l  # 输出： 8
```

**统计当前目录下的文件数**

```shell
ls -l | wc -l
```


