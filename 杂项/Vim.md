## 一、基础

### 1.1 模式

* 命令行模式：命令行模式可以理解为一个快速运行各种命令的模式，按`esc`键进入。
* 插入模式：这是大家最熟悉的了，这时的 Vim 相当于普通编辑器，按`i`进入。
* 可视(Visual)模式：这个模式中，可以用光标键高亮选择文本。光标所在字符是包含在选区中的。当在可视模式下输入了命令以后，Vim 将回到普通模式，这时可以按`p`或`P`进行粘贴。
* 选择模式：和可视模式类似。

从一般模式切换到编辑模式，可用的按键如下：

|  按键   |  说明                                                                |
|--------|----------------------------------------------------------------------|
| `i, I` | `i`在目前光标所在处插入；`I`在目前所在行的第一个非空格符处开始插入             |
| `a, A` | `a`在目前光标所在的下一个字符处开始插入；`A`在从光标所在行的最后一个字符处开始插入|
| `o, O` | `o`在目前光标所在的下一行处插入新的一行；`O`在目前光标所在的上一行处插入新的一行  |
| `r, R` | `r`只替换光标所在的那个字符一次；`R`会一直替换光标所在的文字，直到按下`Esc`键   |

### 1.2 语法高亮

可以在 Vim 中输入命令`:syntax on`激活语法高亮。若需要 Vim 启动时自动激活语法高亮，在`~/.vimrc`文件中添加一行`syntax on`即可。

一般情况，Vim 的配色最好和终端的配色保持一致，不然会很别扭。复制 solarized 配色方案，并编辑`~/.vimrc`文件：

```shell
cd solarized
cd vim/colors/solarized/colors
mkdir -p ~/.vim/colors
cp solarized.vim ~/.vim/colors/

vim ~/.vimrc
syntax enable
set background=dark
colorscheme solarized
```

## 二、命令行模式下可用的命令

在命令行模式下，Vim 有很多命令可以使用。

### 2.1 基本命令

|  按键                 |  说明                                           |
|----------------------|-------------------------------------------------|
| `:w`                 | 将编辑的数据写入文件中。                            |
| `:w!`                | 若文件属性为“只读”时，强制写入该文件。                |
| `:q`                 | 离开 Vim。                                       |
| `:q!`                | 强制离开 Vim，不保存文件。                          |
| `:wq`                | 强制保存后离开 Vim。                               |
| `:x`                 | 保存文件并离开 Vim                                |
| `ZZ`                 | 若文件没改动，则不保存离开；若文件被改动，则保存后离开。 |
| `:w[filename]`       | 将编辑后的数据另存为一个新的文件（另存为）。           |
| `:r[filename]`       | 将`[filename]`这个文件的内容追加到光标所在行之后。    |
| `:n1,n2 w[filename]` | 将 n1~n2 行之间的内容保存到`[filename]`文件。       |
| `:!command`          | 暂时离开 vim 到命令行模式下执行 command 的显示结果    |
| `:set nu`            | 显示行号。还可以使用`:set number`。                |
| `:set nonu`          | 取消行号。                                       |

> 强制写入时，能否写入成功，与用户对该文件的文件权限有关。

### 2.2 跳跃命令

下面的命令能够快速的把光标快速定位到特定的地方。

|  按键       | 说明                                                             |
|------------|------------------------------------------------------------------|
| `h/j/k/l`  | 移动光标：左、下、上、右                                             |
| `0`        | 数字零，到行头                                                      |
| `^`        | 到本行第一个不是空字符的位置                                          |
| `$`        | 到本行行尾                                                         |
| `g_`       | 到本行最后一个不是空字符的位置                                         |
| `gg`或`[[` | 到第一行                                                           |
| `G`或`]]`  | 到最后一行                                                          |
| `:N`       | 到第 N 行                                                          |
| `NG`       | 到倒数第 N 行                                                      |
| `w`        | 到下一个单词                                                        |
| `b`        | 到上一个单词                                                        |
| `fa`       | 到当前行中的下一个字符`a`，其他字符类似，区分大小写                       |
| `Fa`       | 到当前行中的上一个字符`a`，其他字符类似，区分大小写                       |
| `t,`       | 到当前行中下一个`,`前面的字符。逗号可以变成其它字符，区分大小写             |
| `T,`       | 到当前行中上一个`,`后面的字符。逗号可以变成其它字符，区分大小写             |
| `*`        | 到文件中下一个当前光标所在单词                                         |
| `#`        | 到文件中上一个当前光标所在单词                                         |
| `%`        | 匹配`{`的对应`}`，像单引号等其它成对存在的也一样                         |
| `/pattern` | 搜索 pattern 对应的字符串。如果搜索出多个匹配，按`n`键到下一个，`N`到上一个 |
| `Ctrl+u`   | 上下翻半页                                                         |
| `Ctrl+b`   | 下翻半页                                                           |
| `Ctrl+d`   | 屏幕向下移动半页。                                                   |
| `Ctrl+u`   | 屏幕向上移动半页。                                                   |

> 空字符：空格、Tab、换行、回车等。

### 2.3 编辑命令

| 按键      | 说明              |
|-----------|-------------------|
| `yy`      | 复制当前行          |
| `p`       | 在当前行下方粘贴一行  |
| `dd`      | 删除当前行          |
| `:nd`     | 删除第 n 行         |
| `:n1,n2d` | 删除 n1~n2 行       |
| `:%d`     | 删除所有内容         |
| `U`       | 撤销上一步的删除      |
| `Ctrl+R`  | 恢复上一步撤销的删除  |

## 三、可视模式

### 3.1 常用的可视模式命令

| 按键    | 说明                              |
|--------|-----------------------------------|
| `x`    | 删除                               |
| `dd`   | 剪切当前行                          |
| `cc`   | 剪切当前行                          |
| `y`    | 复制                               |
| `r字符` | 所有字符替换为新字符                  |
| `u U`  | 分别是所有字母变小写、变大写、反转大小写 |

### 3.2 选中命令

`命令 ＋ a + 字符`或者`命令 ＋ i ＋ 字符`是很实用的一个组合。其中快速选中正是一个用这个组合的例子。

假设有一个字符串`(map (+) ("foo")).`，而光标键在第一个`o`的位置。

* `vi"` － 会选择`foo`
* `va"` － 会选择`"foo"`
* `vi)` － 会选择`"foo"`
* `va)` － 会选择`("foo")`
* `v2i)` － 会选择`map (+) ("foo")`
* `v2a)` － 会选择`(map (+) ("foo"))`

## 四、一些规律

### 4.1 数字

Vim 中的数字使用非常普通，基本场景都是代表重复多少次的意思。比如：

* `3yy` 复制 3 行
* `3p`  粘贴 3 次
* `3fa` 跳转到当前行光标所在处后面的第三个字符 a

上面只是一些简单的例子，基本上了解了命令，很大部分命令都支持 数字 ＋ 命令 的组合。

### 4.2 大小写

大小写在很多场景都是相反命令的意思，了解了小写命令的含义，很多场景相反的含义就是该命令的大写。比如：

* `fa`和`Fa` 分别表示到当前行下一个和上一个字符`a`处。
* `t,`和`T,` 分别表示到当前行的上一个/下一个`,`符号的前/后面的字符处。

## 查找和替换
### 查找
在 normal 模式下按下`/`即可进入查找模式，输入要查找的字符串并按下回车。Vim 会跳转到第一个匹配。按下`n`查找下一个，按下`N`查找上一个。

Vim 查找支持正则表达式，例如`/vim$`匹配行尾的"vim"。 需要查找特殊字符需要转义，例如`/vim\$`匹配"vim$" 。

> 注意查找回车应当用`\n` ，而替换为回车应当用`\r`(相当于 <CR>)。

在查找模式中加入`\c`表示大小写不敏感查找，`\C`表示大小写敏感查找。如`/foo\c`将会查找所有的 "foo" , "FOO" , "Foo" 等字符串。

> Vim 默认采用大小写敏感的查找，为了方便我们常常将其配置为大小写不敏感。将上述设置粘贴到你的`~/.vimrc`，重新打开Vim即可生效：
> ```
> " 设置默认进行大小写不敏感查找
> set ignorecase
> " 如果有一个大写字母，则切换到大小写敏感查找
> set smartcase
```

**gd**

另外，还可以使用`gd`来选中当前光标所在位置的关键词。

### 查找当前单词
在 normal 模式下按下`*`即可查找光标所在单词（word），要求每次出现的前后为空白字符或标点符号。例如当前为`foo`， 可以匹配`foo bar`中的`foo`，但不可匹配`foobar`中的`foo`。 这在查找函数名、变量名时非常有用。

按下`g*`即可查找光标所在单词的字符序列，每次出现前后字符无要求。即`foo bar`和`foobar`中的`foo`均可被匹配到。

### 查找与替换
`:s`(substitute)命令用来查找和替换字符串。语法如下：

```
:{作用范围}s/{目标}/{替换}/{替换标志}
```

例如`:%s/foo/bar/g`会在全局范围(`%`)查找`foo`并替换为`bar`，所有出现都会被替换(`g`)。

**作用范围**
作用范围分为当前行、全文、选区等等。

* 当前行：`:s/foo/bar/g`
* 全文：`:%s/foo/bar/g`
* 选区：`:'<,'>s/foo/bar/g`
* 行数：`:5,12s/foo/bar/g` 表示 5 - 12 行
* 相对行：`:.,+2s/foo/bar/g` 表示 当前行`.`与接下来两行`+2`

> 在 Visual 模式下选择区域后输入 : ，Vim即可自动补全为 :'<,'> 。

**替换标志**
上面命令结尾的`g`即是替换标志之一，表示全局`global`替换（即替换目标的所有出现）。 还有很多其他有用的替换标志：

* 空替换标志表示只替换从光标位置开始，目标的第一次出现：`:%s/foo/bar`
* `i`表示大小写不敏感查找，`I`表示大小写敏感，等效于模式中的`\c`（不敏感）或`\C`（敏感）：`:%s/foo/bar/i`
* `c`表示需要确认，例如全局查找"foo"替换为"bar"并且需要确认：`:%s/foo/bar/gc`。

> 使用`c`标志回车后，Vim 会将光标移动到每一次"foo"出现的位置，并提示`replace with bar (y/n/a/q/l/^E/^Y)?`。按下`y`表示替换，`n`表示不替换，`a`表示替换所有，`q`表示退出查找模式，`l`表示替换当前位置并退出。`^E`与`^Y`是光标移动快捷键。

### 高亮设置
**高亮颜色设置**
将下面的配置粘贴到`~/.vimrc`，重新打开 vim 即可生效：

```
highlight Search ctermbg=grey ctermfg=black
```

上述配置指定 Search 结果的前景色（foreground）为黑色，背景色（background）为灰色。 更多的 CTERM 颜色可以查阅：[Xterm256 color names for console Vim](http://vim.wikia.com/wiki/Xterm256_color_names_for_console_Vim)。

**禁用/启用高亮**
有木有觉得每次查找替换后 Vim 仍然高亮着搜索结果？可以手动让它停止高亮，在 normal 模式下输入：`:nohighlight`或`:nohl`。

其实上述命令禁用了所有高亮，正确的命令是`:set nohlsearch`。 下次搜索时需要`:set hlsearch`再次启动搜索高亮。怎么能够让 Vim 查找/替换后自动取消高亮，下次查找时再自动开启呢？

```
" 当光标一段时间保持不动了，就禁用高亮
autocmd cursorhold * set nohlsearch
" 当输入查找命令时，再启用高亮
noremap n :set hlsearch<cr>n
noremap N :set hlsearch<cr>N
noremap / :set hlsearch<cr>/
noremap ? :set hlsearch<cr>?
noremap * *:set hlsearch<cr>
```

将上述配置粘贴到`~/.vimrc`，重新打开 vim 即可生效。


## 多窗口功能
### 打开新分隔窗口
```
:sp [filename]  // 在新窗口打开新文件
:sp             // 默认打开同一个文件
:new            // 打开一个新窗口，并开始*编辑一个空的缓冲区*
```

### 关闭窗口
```
:close     // 关闭当前窗口
```

实际上，任何退出文件编辑的命令象`:q`和`ZZ`都会关闭窗口，但是用`:close`可以阻止你关闭最后一个 Vim，以免以意外地关闭整个 Vim。

如果想关闭除当前窗口外的所有其它窗口，可以使用：

```
:only
```

### 新窗口高度初始化
```
:nsp
```

其中，n是数字，表示新窗口的行数。譬如，打开了一个高度为3行的新窗口：`:3sp`。

### 已打开窗口高度设置
* 增加当前窗口高度：`CTRL-W +`
* 减小当前窗口高度：`CTRL-W -`

这两个命令都可以接受一个命令记数，用以一次将窗口的高度增减指定的行数。`4Ctrl + w +`将使当前窗口增加 4 行高度。将窗口高度指定为一个固定的高度：`{height}CTRL-W_`。让窗口达到它可能的最大高度：不指定命令记数直接使用`CTRL-W`。

### 多窗口之间的光标移动
|    按键     |    说明    |
|------------|------------|
| CTRL-W + h | 到左边的窗口 |
| CTRL-W + j | 到下面的窗口 |
| CTRL-W + k | 到上面的窗口 |
| CTRL-W + l | 到右边的窗口 |
| CTRL-W + t | 到顶部窗口  |
| CTRL-W + b | 到底部窗口  |

## 常用配置
```
syntax on
set background=dark
colorscheme solarized

" 设置默认进行大小写不敏感查找
set ignorecase
" 如果有一个大写字母，则切换到大小写敏感查找
set smartcase
set number
set cindent
set backspace=indent,eol,start
set tabstop=4
set shiftwidth=4
let &termencoding=&encoding
set fileencodings=utf-8
set hls
```


## 参考
1. [Vim 初探](http://imweb.io/topic/579deaee93d9938132cc8d88)
2. [在 Vim 中优雅地查找和替换](http://harttle.com/2016/08/08/vim-search-in-file.html)
3. [使用Vim](http://www.wushxin.top/2016/08/15/%E4%BD%BF%E7%94%A8Vim.html)
4. [学习笔记：vim基础 —— 命令行备忘录](http://www.dengzhr.com/frontend/tools/990)

