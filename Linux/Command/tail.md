tail 命令可以查看文件的内容，并默认输出到标准输出中。利用该命令可以监听文件的变动，并实时的输出最新的内容，方便的查看最新日志。

### 选项

#### 1. -f 和 -F 的区别

这两个选项都可以用来指定一直监听文件，即便已经到达文件末尾了。不同点在于：

* `-f` 根据文件描述符进行追踪，即便文件被重命名，也会继续监听重命名后的文件；
* `-F` 根据文件名进行追踪，如果文件被重命名，那么会继续尝试重新监听指定的名称的文件。

比如，对一个日志文件，想每天都重新生成一个文件来记录，可以通过定时方式，将日志文件重命名，然后新建一个空的日志文件的方式来实现，对应如下的操作：

```shell
mv access.log access-2020-11-05.log
touch access.log
```

如果使用`-f`和`-F`分别来监听 access.log 文件，再执行上面的命令的过程中，两者的表现就会出现差异了：

* `-f` 使用该选项的时候，重命名文件之前会监听 access.log 文件的变动；重命名之后，会监听重命名后的 access-2020-11-05.log 文件的变动；
* `-F` 使用该选项的时候，重命名文件之前会监听 access.log 文件的变动；重命名之后，会重试对 access.log 文件的监听；新创建 access.log 文件之后，会自动继续监听新的 access.log 文件的变动。

> 转摘：[别小看tail 命令，它难倒了技术总监](https://mp.weixin.qq.com/s/q7zRiye8ufX34ayGKjy1Rw)


