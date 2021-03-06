在日常工作中，可以将一些常用的操作通过 Node.js 开发成命令行工具来完成。开发 Node.js 命令和一般的 Node.js 代码并没有什么不同，主要是 package.json 配置文件的不同。

### 配置 bin 字段

一个 npm 模块，如果在`package.json`中指定了`bin`字段，那说明该模块提供了可在命令行执行的命令，这些命令就是在`bin`字段中指定的，如下：

```json
{
  "bin": {
    "myapp": "./cli.js"
  }
}
```

如果 npm 包只提供了一个可执行的命令，也可以直接将`bin`字段设置为目标文件，此时命令行中可执行的 CLI 命令名为 npm 包名（即`name`字段）。比如，上面的配置也可以使用如下的方式配置：

```JavaScript
{
    "name": "myapp",
    "bin": "./cli.js"
}
```

将这样的 npm 包安装之后，就可以在命令行中执行`myapp`命令来完成相关操作了。执行该命令的时候，实际执行的是`bin`字段中命令对应的 JavaScript 文件(在这里就是`./cli.js`文件)。如果是全局安装，会将这个目标 js 文件映射到`prefix/bin`目录下，而如果是在项目中安装，则映射到`./node_modules/.bin/`目录下。

### 开发

命令的开发就是正常的 JavaScript 代码的编写，这些代码最终会在 Node 环境中执行，所以可以使用 Node 支持的功能，而且也能够引入其他的包依赖。

同时，命令还支持参数的传递，与调用 JavaScript 方法类似。

在代码中能够通过`process.argv`获取到来自命令行的输入。但需要注意它返回的参数列表中前两位是 Node.js 的路径和当前项目的路径，**从第三个元素开始才是命令中用户输入的数据**。

### 调试

开发时，可以通过在当前开发目录中执行`npm link`操作，进行本地调试。

执行 link 操作相当于在本地安装了开发的命令，所以就可以在命令行中执行自己的开发的命令，核验效果、调试处理。

### 发布

开发完成之后，就可以使用 npm 工具将其发布：

```shell
npm publish --access public
```

### 第三方工具

* [chalk](https://github.com/chalk/chalk) 命令行工具能够打印帮助和使用信息是很重要的，如果自己输出的话，会面临格式化这些内容的麻烦。该工具可以将输出信息进行高亮加彩色进行展示。
* [commander.js](https://github.com/tj/commander.js/) 该工具可以提供参数的描述、校验、提取等功能，方便命令开发时的基础功能的编写。



