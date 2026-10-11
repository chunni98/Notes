---
title: Vim
lang: zh-CN
sidebar: auto
---

非常感谢 vimtutor，帮我快速入门 vim，同时感谢以下在网上分享学习资源的好心人：

- [YYQ-VIM 学习笔记][2]
- [Coolshell-简明vim练级攻略][3]
- [Easwy-Vim 实用技巧][4]
- [Easwy-Vim 使用进阶][5]
- [jinbo-.vimrc 实用配置][1]
- [像 IDE 一样使用 vim](#)
- [易水博客](#)
- [可能是 windows 下最漂亮的 Gvim][6]

[1]: https://www.jianshu.com/p/793f7ce26281
[2]: https://www.zhihu.com/column/learn-vim
[3]: https://coolshell.cn/articles/5426.html
[4]: https://blog.csdn.net/saying0101_0010_0000/article/details/114528186
[5]: https://blog.easwy.com/archives/advanced-vim-skills-catalog/
[6]: https://keelii.com/2016/06/13/awsome-window-vimrc

## 0 约定

`<KEY>` -- 按下 `KEY` 键

`C-r` -- 同时按下 `Ctrl` 键和 `r` 键。

## 1 vimtutor

### 1.1 移动光标

`h` -- 左移，`l` -- 右移，`k` -- 上移，`j` -- 下移

**提示**: `<ESC>` 返回正常模式（Normal）

### 1.2 VIM 的进入和退出

Normal 模式下，`:q!<回车>` 丢弃所有改动退出。

### 1.3 文本编辑之删除

Normal 模式下，`x` -- 删除光标所在位置的字符。

### 1.4 文本编辑之插入

Normal 模式下，`i` -- 进入 Insert 模式。

### 1.5 文本编辑之添加

Normal 模式下，`A` -- 光标移动到行尾之后，进入 Insert 模式。

### 1.6 编辑文件

命令行中输入：`vim [filename]<回车>` -- 编辑文件 `filename` 。

Normal 模式下，`:wq<回车>` -- 保存并退出。

### 1.7 删除类命令

Normal 模式下，`dw` -- 从光标位置删除到到下一个 `word` 起始处前。

`word` -- 不被空格分隔的连续字母或连续标点符号。

### 1.8 更多删除类命令

Normal 模式下，`d$` -- 从当前光标删除到行末。

### 1.9 关于命令和对象

许多改变文本的命令都由一个操作符和一个动作构成。

Normal 模式下，修改命令格式是：

`operator [number] motion`

- `operator`: 操作符，代表要做的事情，如 d 代表删除。
- `[number]`: 可选的数字，代表动作重复的次数。
- `motion`: 动作，代表所操作的文本上的移动，例如 `w` 代表单词（word），`$` 代表行末等等。

使用删除操作符 d 的删除命令的格式如下：

`d motion`

其中：

`d` - 删除操作符。

`motion` - 操作符的操作对象(在下面列出)。

一个简短的动作列表：

`w` - 从当前光标当前位置直到下一个单词起始处，不包括它的第一个字符。

`e` - 从当前光标当前位置直到单词末尾，包括最后一个字符。

`$` - 从当前光标当前位置直到当前行末，包括最后一个字符。

因此输入 `de` 会从当前光标位置删除到单词末尾。

### 1.10 使用计数指定动作

**在动作前输入数字会使它重复那么多次。**

`0` -- 移动光标到行首。

`2w` -- 光标向前移动两个单词。

`3e` -- 光标向前移动到第三个单词的末尾。

### 1.11 使用计数以删除更多

 **使用操作符时输入数字可以使它重复那么多次。**

上面已经提到过删除操作符和动作的组合，您可以在组合中动作之前插入一个数字以删除更多：
`d number(数字) motion`

输入 `d2w` 以删除两个大写字母单词。

### 1.12 操作整行

`dd` -- 删除光标所在行整行。

`2dd` -- 删除两行。

### 1.13 撤销类命令

`u` -- 撤销最后执行的命令，可以撤销掉 `U`。

`U` -- 撤销对整行的修改。

`C-r` -- 恢复之前的撤销命令，revoer。

### 1.14 置入类命令

`p` -- 将最后一次删除的内容置于光标后。

`dd` 删除整行后，会将改行保存到 `Vim` 的寄存器中。

### 1.15 替换类命令

输入 r 和一个字符替换光标所在位置的字符。

### 1.16 更改类命令

改变文本直到一个单词的末尾，请输入 `ce`。

`cw` 效果类似 `dw` + `i`。

### 1.17 使用 C 更改更多

更改类操作符可以与删除中使用的同样的动作配合使用。

更改类操作符的工作方式跟删除类是一致的。操作格式是：

`c [number] motion`

动作参数(motion)也是一样的，比如 `w` 代表单词，`$` 代表行末等等。

### 1.18 定位及文件状态

`C-g` -- 显示当前编辑文件中的当前光标所在行位置以及文件状态信息。

`[num] G` -- 直接跳转到文件中某一指定行，默认最后一行。

`gg` -- 跳转到文件第一行。

### 1.19 搜索类命令

输入 `/` 加上一个字符串可以用以在当前文件中查找该字符串。

支持正则表达式。

要查找同上一次的字符串，只需要按 `n` 键。要向相反方向查找同上一次的字符串，请输入大写 `N` 即可。

想逆向查找字符串，请使用 `?` 代替 `/` 进行。

要回到之前的位置按 `C-o` 。重复按可以回退更多步。`C-i` 会跳转到较新的位置。

如果查找已经到达文件末尾，查找会自动从文件头部继续查找，

### 1.20 配对括号的查找

输入 `%` 可以查找配对的括号。

### 1.21 替换命令

`:s/old/new/g` 可以替换 `old` 为 `new`，替换全行。

`:s/old/new<回车>` 只改变光标所在行的第一个匹配串。

`:#,#s/old/new/g` `#,#` 代表替换操作的若干行中首尾两行的行号。

`:%s/old/new/g` 替换整个文件中的每个匹配串。

`:%s/old/new/gc` 替换整个文件中的所有匹配串，并且提示是否进行替换。

### 1.22 执行外部命令的方法

输入 `:! <command>` 可以执行该外部命令 `command`。

所有的 `:` 命令都必须以敲 `<Enter>` 结束。

### 1.23 关于保存文件的更多信息

要将对文件的改动保存到文件中，请输入 `:w FILENAME` 。

### 1.24 具有选择性的保存命令

要保存文件的部分内容，请输入 `v motion :w FILENAME`

如 `:'<,'>w TEST` 可将选中的内容保存到新文件 TEST 中。

### 1.25 提取和合并文件

要向当前文件中插入另外的文件的内容，`:r FILENAME`

如：`r !ls` 将把 `ls` 命令的输出放置到光标所在位置下面。

### 1.26 打开类命令

输入 `o` 将在光标的下方打开新的一行并进入插入模式。(open)

`O` 将在光标上方打开新的一行。（大写）

### 1.26 附加类命令

输入 `a` 将可在光标之后插入文本。

### 1.27 置换命令的另外一个版本

`R` 连续替换多个字符。

### 1.28 复制粘贴文本

使用 `y` 复制文本，使用 `p` 粘贴文本。

`yw` 复制一个单词。

`ye`

`y$`

### 1.29 设置类命令的选项

`/word\c` 搜索 `word` 时大小写不敏感。

`:set ic` 临时设置忽略大小写敏感。

`set hlsearch` 搜索时高亮匹配项。

`set nohlsearch` 移除高亮显示。

`set incsearch` 增量搜索。

### 1.30 获取帮助信息

- `<F1>` 键
- 输入 `:help<Enter>`

`C-w C-w` 在不同窗口间跳转。

例：

`:help w`

`help c_CTRL_D`

`help user-manual`

### 1.31 命令补全功能

`C-d` 显示可能的命令列表。

 `<TAB>` 可以进行命令行补全。

`:set nocp` 确保 `Vim` 不是在兼容模式下运行。

`help user-manual` 阅读 `Vim` 的用户手册。

## 2 Vim 学习笔记

## inbox

`:w Filename` **visual** 模式下，将选中内容另存为。

可视化模式下选择操作区域以后，
按下 d会删除选择的区域，
按下 y 会复制选择的区域，按下 p 会黏贴选择的区域。

宏录制的录制操作

先将光标移动到第一行，在普通模式下按下 q 键（宏录制是 q 键启动的）,在按一个 a （字母随意）,表示该宏注册为 a ，按下 I 在行首插入一个 tab 键，按下jj或者 `<ESC>`退出编辑模式,按下 j 将光标移动到下一行行首，最后按下 q 键完成录制操作（宏录制是 q 键结束的）。
总结上面例子的操作流程：
q → a → I → tab → jj → j → q
上面的例子成功地把在行首插入 tab 的功能录制了下来，那么如何应用到其他行呢？


宏录制的使用

上述的例子，在正常模式下，按 @a执行宏录制的一系列动作，将会在第二行执行插入 tab 。
@@ 是对上一次宏使用的重复操作。n@a 就会执行 n 次一系列的动作。使用宏录制可以一次执行一系列的操作，可以针对一些重复度较高的操作进行宏录制。

`vim file +` -- 打开文件，并定位到文件尾部。

`vaw`

`viw`

`vtw`

可视模式下选择文本对象，a 会选择区域结束标识，i 不会。

`;` f 的下一个

`,` f 的上一个

`*` -- 匹配光标当前所在单词，移动光标到下一个匹配单词。

`#` -- 匹配光标当前所在单词，移动光标到上一个匹配单词。

`[num]gt` 指定切换到某个标签页。

`gT`

vim path

`~/src/vim70/**` 在 所有子目录树中搜索。

建议 使用 `set path+=` 而不是 `set path=`

`S-k` 查看系统函数原型。

`C-f` `C-b` 翻页。 `b` back 到word 首。

`<<` 缩进

`>>` 缩进。

`tabnew file` tabpages 打开文件

使用标签页代替 buffers

`:E` 打开文件夹

`c-w H J K L` 移动窗口

`c-w [num] < >` 调整窗口大小

`vim -O file file` 分屏打开多个文件。

`gf` 跳转到头文件，需要设置 path。

`c-w f` 新建窗口打开头文件

`c-w gf` 新建标签页打开头文件

`c-w ]` 新建窗口打开定义。

`g ]` 所有标签列表

`c-6` 返回上个缓冲区。

`[[` 向前寻找函数首括号。

`]]` 向后寻找函数括号首。

`vs`

`sp`

`f ` 向前寻找。

`F` 向后寻找符号。

`M` 中间

`H` 首

`L` low

`gd`

`gD` 跳转到符号定义

`g]` 跳转到定义，列出列表

`c-o` 光标历史位置往前调

`c-i` 光标历史位置往后调

`jumps` -- 打开跳转表
    - `C-o` -- 跳回到上一个位置。
    - `C-i` -- 跳转到下一个位置。

`c-t` 返回上一个标签

`c-6` 返回上个缓冲区

`dt字符` 删除到 字符前

`H` 画面最上方

`M` 画面中间

`L` 画面底部

TODO: path，跳转，path 用于 `c-n` 查找，gf 查找。

vim 的跟踪通常可以通过两种方式实现:

tags: 通过 ctags 工具生成 tags 文件
cscope 数据库: 通过 cscope 或 gtags-cscope 生成 cscope 数据库
两种方法各有优缺点, 而且可以搭配使用, 并不冲突. 下面逐个介绍.




TODO: ctags cscope


[vi/vim使用进阶: 程序员的利器 – cscope](https://blog.easwy.com/archives/advanced-vim-skills-cscope/)

建议安装 Universal Ctags，Exuberant Ctags 已停止更新

`ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .` 为 C++ 生成 tags

`ctags -R --fields=+niazS --extra=+q --c++-kinds=+px --output-format=e-ctags`

`--output-format=e-ctags` 仅 universal ctags 能加。

-R: ctags 循环生成子目录的 tags

--c++-kinds=+pxl: ctags 记录 c++ 文件中的函数声明和各种外部和前向声明 (l 表示记录局部变量, 可以认为是 local 的缩写)

--fields=+iaS: ctags 要求描述的信息, 其中 i 表示如果有继承, 则标识出父类; a 表示如果元素是类成员的话, 要标明其调用权限 (即是 public 还是 private); S 表示如果是函数, 则标识函数的 signature.

extra=+q: 强制要求 ctags 做如下操作: 如果某个语法元素是类的一个成员, ctags 默认会给其记录一行, 可以要求 ctags 对同一个语法元素再记一行, 这样可以保证在 VIM 中多个同名函数可以通过路径不同来区分.

前半部分 ./.tags; 代表在文件的所在目录下查找名字为 .tags 的符号文件, 后面一个分号代表查找不到的话向上递归到父目录, 直到找到 tags 文件或者递归到了根目录还没找到; 逗号分隔的后半部分 tags 是指同时在 vim 的当前目录 (:pwd 命令返回的目录, 可以用 :cd .. 命令改变) 下面查找 tags 文件.

`g ]` 查看所有匹配的 tags，ctrl - t 退栈

**gtags-cscope 使用：**

[在Vim里使用gtags-cscope](https://www.cnblogs.com/cascle/p/5148389.html)

[在Vim中使用gtags](https://www.cnblogs.com/kuang17/p/9449258.html)

[Vim 8 中 C/C++ 符号索引：GTags 篇](https://zhuanlan.zhihu.com/p/36279445)

[介绍一下gnu global，比cscope更方便更快速的索引工具](https://forum.ubuntu.com.cn/viewtopic.php?t=343460)

gtags 是 cscope 的替代品

gtags, 全名为 gnu global, 是一个类似 cscope 的工具(不是 ctags 的替代品!), 也能提供源文件之间的交叉索引. 其独到之处在于, 当生成索引文件以后, 再修改整个项目里的一个文件, 然后增量索引的过程非常快.

gtags 请自行编译安装。

安装好以后, 有 global, gtags, gtags-cscope 三个命令. global 是查询, gtags 是生成索引文件, gtags-cscope 是与 cscope 一样的界面.

gtags 环境配置
gtags 是支持使用 ctags/universal-ctags 或者 pygments 来作为分析前端支持 50+ 种语言. 使用 ctags/universal-ctags 作为前端只能生成定义索引不能生成引用索引, 因此我们要安装 pygments , 保证你的 $PATH 里面有 python, 接着:

pip install pygments
保证在环境里里要设置过如下两个环境变量:

export $GTAGSLABEL = 'native-pygments'
export $GTAGSCONF = '/path/to/share/gtags/gtags.conf'
第一个 GTAGSLABEL 告诉 gtags 默认 C/C++/Java 等六种原生支持的代码直接使用 gtags 本地分析器, 而其他语言使用 pygments 模块. 第二个环境变量必须设置, 否则会找不到 native-pygments 和 language map 的定义, Mac 下的路径为 /usr/local/share/gtags, 可以把它拷贝成 ~/.globalrc

实际使用 pygments 时, gtags 会启动 python 运行名为 pygments_parser.py 的脚本, 通过管道和它通信, 完成源代码分析, 故需保证 gtags 能在 $PATH 里调用 python, 且这个 python 安装了 pygments 模块.

gtags -v 遍历子目录, 从源码文件中提取符号, 这样就生成了整个目录的索引文件, 包括 GTAGS, GRTAGS, GPATH 三个数据库文件.

GTAGS: 定义数据库
GRTAGS: 引用数据库
GPATH: 路径名数据库

查询使用的命令是 global 和 gtags-cscope. 前者是命令行界面, 后者是与 cscope 兼容的 ncurses 界面. 这里就不多介绍了, 重点是如何在 vim 里查询:

gtags-cscope 还有一个优点就是我后台更新了 gtags 数据库, 不需要像 cscope 一样调用 cs reset 重启 cscope 子进程, gtags-cscope 一旦连上永远不用重启, 不管你啥时候更新数据库, gtags-cscope 进程都能随时查找最新的符号.

`ln -s path` 然后 gtags 即可生成外部目录的 gtags

[gtags 详解](https://blog.csdn.net/aaaLG/article/details/121582514)

当我们更改了某个文件以后, 比如 project/subdir1/subdir2/file1.c, 想更新索引文件 (索引文件是 project/GTAGS), 只需这样:

```shell
$ cd project/subdir1/subdir2/
$ vim file1.c
$ global -u
```
global -u 这个命令会自动向上找到 `project/GTAGS`, 并更新其内容. 而 gtags 相对于 cscope 的优势就在这里: 增量更新单个文件的速度极快, 几乎是瞬间完成. 有了这个优势, 我们就可以增加一个 autocmd, 每次 :w 的时候自动更新索引文件.

gtags -i 增量更新，推荐使用 global -u


如果你索引C++代码， 运行 export GTAGSFORCECPP=1 使得global将 .h 文件当作C++文件。

[Ctags 官方手册](https://docs.ctags.io/en/latest/man/ctags.1.html)

```
cs add GTAGS
cs find
```

cscope find 命令：

```
                0 或 s: 查找本符号
                1 或 g: 查找本定义
                2 或 d: 查找本函数调用的函数
                3 或 c: 查找调用本函数的函数
                4 或 t: 查找本字符串
                6 或 e: 查找本 egrep 模式
                7 或 f: 查找本文件
                8 或 i: 查找包含本文件的文件
```


如果你同时使用 cscope 和 ctags，:cstag 允许你在跳转前对两者都进行查询。例
如，你可以选择先查询 cscope 数据库，如果无法找到匹配，再查询标签文件。这种做法
的次序可以通过 csto 的值来调整。

'csto' 的值决定 :cstag 命令查找的次序。如果 'csto' 被设为 0，cscope 数据库先
被搜索，搜索失败的情况下在搜索标签文件。如果 'csto' 被设为 1，标签文件会在
cscope 数据库之前被搜索。缺省值为 0。（实测为 1）

在Linux用vim vi等编辑器编辑文件时，有时遇到突然崩溃或者没有反应时，在编辑文档的目录下就会出现一个交换文件即：.swp文件，这是一个隐藏文件，需要 ls -a 才能显示出来，可以利用vim工具重新恢复原来的文件
vim -r filename 即可恢复到之前的编辑状态

`C-x C-I` 让vim从被包含文件中提取补全项。

`C-x C-f` -- 补全文件名。(filename)
    - 如果当前光标下的文本不包含任何路径信息，那么将显示当前目录下的文件列表。
    - 如果当前光标下的文本包含任何（绝对或相对）路径信息，那么将显示其指定目录下的文件列表。
    - 如果当前光标下的文本包含唯一的路径信息（比如“~”），那么将自动转换为目录的完整名称。

`C-N` CTRL-P一般的含义是向上，因此CTRL-P补全是向上查找以进行补全，而CTRL-N是向下查找以进行补全，在不同场合使用不同的快捷键可以加速补全的速度。

`C-X C-P` 补全局部变量

`C-X C-O` 智能补全 !智能补全不能对局部变量进行补全

如果要支持C++的全能补全，需要到vim主页下载OmniCppComplete插件

`:e` 编辑文件

`ls` 查看缓冲区

`:jumps` 查看跳转表，使用 `C-o` 跳转到下一个

vim C++ 补全

f{char}  :  正向移动到下一个{char}所在位置

F{char}  :  反向移动到上一个{char}所在位置

t{char}  :  正向移动到下一个{char}的前一个字符上

T{char}  :  反向移动到上一个{char}的后一个字符上

Vim会记录上一次执行的查找命令，再次查找时可以使用 ';' 命令来完成相同查找。如果查询跳过头了，可以使用 ',' 命令返回光标之前的位置。

文本对象

'i' 命令可以理解为 inside，即选中匹配符号之间不包含匹配符号的内容。而 'a' 则选中包含匹配项的内容。

```
'a)' 或 'ab'  :  一对()
'a}' 或 'aB'  :  一对{}
a]  :  一对[]
a>  :  一对<>
a'  :  一对''
a"  :  一对""
a`  :  一对``
at  :  一对xml标签

iw  :  当前单词
aw  :  当前单词及一个空格
iW  :  当前字符串
aW  :  当前字符串及一个空格
is  :  当前句子
as  :  当前句子及一个空格
ip  :  当前段落
ap  :  当前段落及一个空行
```

`c-]` ctags 跳转定义

`c-t` 返回。

`gg=G` 调用 indent 格式化文件

`=` 自动缩进

`gU` 大写 `gu` 小写

`g~` 大小写转换

`ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .`

ctags -R --c++-kinds=+px

ctags识别很多元素，但未必全都记录，例如“函数声明”这一语法元素默认是不记录的，可以控制ctags记录的语法元素的种类。如上命令要求ctags记录c++文件中的函数声明和各种外部和前向声明。



–fields=[+|-]flags
–fields指定tags的可用扩展域（extension fields），以包含到tags入口。
i:继承信息Inheritance information
a：类成员的访问控制信息 Access (or export) of class members
S： 常规签名信息，如原型或参数表 Signature of routine(e.g. prototype or parameter list)
–extra=[+|-]flags
指定是否包含某种扩展信息到tags入口。
q：包含类成员信息（如c++,java,Eiffel)。
但就算是C 语言的结构，也需要这两个参数设置才能获取成员信息。

" i 表示如果有继承，要标明父类；
" a 表示如果是类的成员，要标明其access属性（即是public的还是private的）；
" S 表示如果是函数，要标明函数的signature；
" K 表示要显示语法元素类型的全称；
" z 表示在显示语法元素的类型时，使用格式kind:type。

ctags -R --fields=+aiKSz

set tags= ./tags, tags, /usr/include/tags

ctags在记录成员函数时，默认情况下tag的名字只包括该函数的名字，不包括类名，这样很多不同类但同名的函数所对应的tag名字都一样。于是在VIM中使用函数名来定位时就会出现很多选择，很麻烦。如果想用包括类名的函数全名进行定位，就得要求ctags记录全名。

强制ctags给类的成员函数多记一行的命令为：

ctags --extra=+q

`Ctrl+]`           跳转到光标所在符号的定义。


[ctags 使用详解](https://www.cnblogs.com/kelamoyujuzhen/p/11672005.html)



set cino=:0g0t0(sus
设定 C/C++ 风格自动缩进的选项，这里简要介绍一下这段代码里用到的选项的含义，cino 支持的选项还很多，更多选项请看用户手册。

```c
// :0
//
// switch 语句之下的 case 语句缩进 0 个空格，也就是说不缩进，与 switch 块平
// 齐，使用这样风格：
switch (x)
{
case 1:
    a = b;
    break;
default:
}

// g0
//
// class、struct 等之下的访问权限控制语句，如 public、protected、private 等，
// 相对 class、struct 等所在的块缩进 0 个空格，与 class 等块平齐，使用这样的
// 风格：
class foo
{
public:
    int a;
private:
    int b;
};

// t0
//
// 如果函数返回值与函数名不在同一行，则返回值缩进 0 个空格，也就是说不缩进，如
// 下所示：

// set cino=t4
    int
func1()
{
}

// set cino=t0
int
func()
{
}

// (sus
//
// 当一对括号跨越多行时，其后的行缩进前面 sw 指定的距离，效果如下：
int a = (1 + 2 + 3
    + 4 + 5 + 6
    + 7 + 8) * 9;
```

```shell
====命令模式====

==字符间==
[NUM] h	向左NUM个字符
[NUM] l	向左NUM个字符
[NUM] j	向左NUM个字符
[NUM] k	向左NUM个字符

==单词间==
[NUM] w	下NUM个单词
[NUM] e	当前或下NUM个单词词尾
[NUM] b	当前或上NUM个单词词首

==页间==
H	页首
M	页中
L	页底
zt	当前行移到顶
zz	当前行移到中
zb	当前行移到底

==行间、句间、段落间==
^	行首(非空)
0	行首
$	行尾
NUM G	跳到NUM行
G	尾行
gg	首行
(	下一句
)	下一句
{	上一段
}	下一段

==翻屏快捷键==
Ctrl+f 向下一屏
Ctrl+b 向上一屏
Ctrl+d 向下半屏
Ctrl+u 向上半屏

==字符操作==
[NUM] x	删除当前NUM个字符
p	粘贴x删除的字符
~	大小写转换
gu	变小写
gU	变大写
J	删除当前行的换行符
r	替换当前字符
R	替换模式

==删除命令==
[NUM] d	删除命令(结合下面使用),
d$ 或 D	删到尾
d0	删到头
d^	删到头(非空)
dw	删除当前字符
de	后删单词
db	前删单词
[NUM] dd	删除NUM行

==删除命令==
[NUM] y	复制命令(结合下面使用),
y$	复制到尾
y0	复制到头
y^	复制到头(非空)
yw	复制当前字符
ye	复制后单词
yb	复制前单词
[NUM] yy	复制NUM行

==粘贴命令==
p	往后粘贴
P	往前粘贴

==改变命令==
c	修改后进入插入模式(下同)
c$ 或 C	删到尾
c0	删到头
c^	删到头(非空)
cw	删除当前字符
ce	后删单词
cb	前删单词
[NUM] cc	删除NUM行

di"	删除" " 之间内容"
yi(	复制( ) 之间内容
vi[	选中[ ] 之间内容
dtCHAR	删除之后直到CHAR字符
ytCHAR	复制之后直到CHAR字符
==查找==
/PATTERN	向下查找
?PATTERN	向上查找
n	查找方向(对查找结果)
N	查找反向(对查找结果)
==撤消更改==
[NUM] u	撤消NUM次
U	撤消行的所有更改
Ctrl + r	重做
[NUM] .	重复前一个/NUM个操作
====扩展命令模式====
==关闭文件==
:q	退出
:q!	强制退出
:wq	保存退出
:x	保存退出
ZZ	保存退出
ZQ	不保存退出
==地址定界+COMMAND==
==地址定界==
:start_pos,end_pos	地址定界
:NUM	跳转到NUM行
:NUM,+NUM	如:2,+3表示2,5行
:.	当前行
:$	最后行
:%	全文
/STR1/,/STR2/	从匹配到的STR1到STR2
NUM,/STR/	从第NUM行到STR匹配行
/STR/,$	从STR匹配行到结束
==COMMAND==
d	删除
w FILE	选中范围保存到文件FILE
r FILE	选中范围保存到指定FILE
==查找并替换==
格式: s/要查的内容/要替换的内容/修饰符
I	忽略大小写
g	每行替换1次
gc	全部替换
s/string1/string2/g
s@string1@string2@gc
s#string1#string2#i
```

```
选项配置说明

选项书写格式	选项说明
:se[t]	显示所有被改动的选项
:se[t] all	显示所有非 termcap 选项
:se[t] termcap	显示所有 termcap 选项
:se[t] {option}	置位布尔选项(开启) 显示字符串或数值选项
:se[t] no{option}	复位布尔选项(关闭)
:se[t] inv{option}	逆转布尔选项的值
:se[t] {option}={value}	将 {value} 附加到字符串选项里, {value} 加到数值选项上
:se[t] {option}+={value}	将 {value} 附加到字符串选项里， {value} 加到数值选项上
:se[t] {option}-={value}	从 {value} 从字符串选项里删除 ，数值选项里减去
:se[t] {option}?	显示 {option} 的值
:se[t] {option}&	重置 {option} 为其缺省值
:setl[ocal]	同 ":set" ，但对局部选项只设定局部值
:setg[lobal]	同 ":set" ，但对局部选项设定其全局值
:fix[del]	根据 't_kb' 的值设置 't_kD'
:opt[ions]	打开一个新窗口，用来参看并设置选项，选项们以功能分组，有单行的解释，并有指向帮助的链接
各选项的简短说明
A
选项全称	选项简称	选项说明
aleph	al	Aleph 字母(希伯来语) 的 ASCII 代码
allowrevins	ari	允许插入和命令行模式的 CTRL-_
altkeymap	akm	缺省的第二语言(波斯语/希伯来语)
ambiwidth	ambw	如何处理有多种宽度的 Unicode 字符
antialias	anti	Mac OS X:用平滑反锯齿的字体
autochdir	acd	根据当前窗口的文件切换目录
arabic	arab	使用阿拉伯语为缺省的第二语言
arabicshape	arshape	阿拉伯语的字型重整
autoindent	ai	根据上一行决定新行的缩进
autoread	ar	有 Vim 之外的改动时自动重读文件
autowrite	aw	有改动时自动回写文件
autowriteall	awa	类似于 'autowrite' ，但适用于更多命令
B
选项全称	选项简称	选项说明
background	bg	"dark" 或 "light" ，用于色彩的高亮
backspace	bs	在一行开关按退格键如何处理
backup	bk	覆盖文件时保留备份文件
backupcopy	bkc	文件备份使用复制而不是换名
backupdir	bdir	备份文件使用的目录列表
backupext	bex	备份文件使用的扩展名
backupskip	bsk	匹配这些模式的文件不予备份
balloondelay	bdlay	弹出气泡之前的延迟(以毫秒计)
ballooneval	beval	打开气泡表达式求值功能
balloonexpr	bexpr	计算气泡显示内容的表达式
binary	bin	二进制方式读/写/编辑文件
bioskey	biosk	MS-DOS ：用 bios 调用取得字符输入
bomb		文件头附加字节顺序标记(Byte Order Mark)
breakat	brk	可以在此断行的字符
brosedir	bsdir	开始浏览文件的目录
bufhidden	bh	缓冲区不再在窗口显示时的行为
buflisted	bl	缓冲区是否显示在缓冲区列表中
buftype	bt	缓冲区的特殊类型
C
选项全称	选项简称	选项说明
casemap	cmp	指定字母大小写如何改变
cdpath	cd	":cd" 搜索的目录列表
cedit		打开命令行窗口的键
charconvert	ccv	完成字符编码转换的表达式
cindent	cin	实现 C 程序的缩进
cinkeys	cink	设置 'cindent' 时启动缩进的键
cinoptions	cino	设置 'cindent' 时如何缩进
cinwords	cinw	'si' 和 'cin' 在这些词后加入额外的缩进
clipboard	cb	使用剪贴板作为无名的寄存器
cmdheight	ch	命令行使用的行数
cmdwinheight	cwh	命令行窗口的高度
colorcolumn	cc	高亮指定列
columns	co	显示屏幕的列数
comments	com	可以开始注释行的模式
commentstring	cms	注释的样板：用于折叠的标志
compatible	cp	尽可能做到与 Vi 兼容
complete	cpt	指定插入模式的自动补全如何工作
completefunc	cfu	插入模式补全使用函数
completeopt	cot	插入模式补全使用的选项
concealcursor	cocu	是否隐藏光标所有行的可隐藏文本
conceallevel	cole	是否显示可隐藏文本
confirm	cf	询问如何处理未保存/只读的文件
conskey	consk	直接从控制台读入键击(只限于 MS-DOS)
copyindent	ci	使得 'autoindent' 使用已有的缩进结构
cpoptions	cpo	设定 Vi-兼容的行为
cryptmethod	cm	文件写入时所用的加密方法
cscopepathcomp	cspc	显示路径多少部分
cscopeprg	csprg	执行 cscope 的命令
cscopequickfix	csqf	用 quickfix 窗口得到 cscope 的结果
cscoperelative	csre	用 cscope.out 路径目录名作为前缀
cscopetag	cst	用 cscope 处理标签命令
cscopetagorder	csto	决定 ":cstag" 的搜索顺序
cscopeverbose	csverb	增加 cscope 数据库时给出消息
cursorbind	crb	光标移动时同时在其他窗口移动
sursorcolumn	cuc	高亮光标所在屏幕列
cursorline	cul	高亮光标所在屏幕行
D
选项全称	选项简称	选项说明
debug		设为 "msg" 可以看到所有错误消息
define	def	查找宏定义所使用的模式
delcombine	deco	在单独使用时删除组合用字符
dictionary	dict	关键字自动补全所用的文件名
diff		当前窗口使用 diff 模式
diffexpr	dex	得到 diff 文件所用的表达式
diffopt	dip	使用 diff 模式的选项
digraph	dg	允许插入模式时输入二合字母
directory	dir	交换文件所用的目录名列表
display	dy	如何显示文本的标志位列表
E
选项全称	选项简称	选项说明
eadirection	ead	'equalalways' 工作的方向
edcompatible	ed	切换 ":subsitute" 命令的标志位
encoding	enc	内部使用的编码方式
endofline	eol	文件最后一行写入换行符` <EOL>`
equalalways	ea	自动使所有窗口大小相同
equalprg	ep	"=" 命令使用的外部命令
errorbells	eb	有错误信息时响铃
errorfile	ef	QuickFix 模式的错误文件名
errorformat	efm	错误文件行格式的描述
esckeys	ek	插入模式下识别功能键
eventignore	ei	忽略的自动命令事件
expandtab	et	键入 `<Tab>` 时使用空格
exrc	ex	在当前目录里读入 .vimrc 和.exrc
F
选项全称	选项简称	选项说明
fileencoding	fenc	多字节文本的文件编码
fileencodings	fencs	参与自动检测的字符编码
fileformat	ff	文件输入输出使用的格式
fileformats	ffs	参与自动检测的 'fileformat' 的格式
fileignorecase	fic	使用文件名时忽略大小写
filetype	ft	自动命令使用的文件类型
fillchars	fcs	显示特殊项目所使用的字符
fkmap	fk	波斯键盘映射
foldclose	fcl	当光标离开时关闭折叠
foldcolumn	fdc	设定指示折叠的列宽度
foldenable	fen	设置为显示所用打开的折叠
foldexpr	fde	当 'foldmethod' 为 "expr" 时使用的表达式
foldignore	fdi	当 'foldmethod' 为 "indent" 时忽略的行
foldlevel	fdl	当折叠级别高于此值时关闭折叠
foldlevelstart	fdls	开始编辑文件的 'foldlevel'
foldmarker	fmr	当 'foldmethod' 为 "marker" 时的标志
foldmethod	fdm	折叠的类型
foldminlines	fml	折叠关闭所需的最少行数
foldnestmax	fdn	最大折叠深度
foldopen	fdo	打开折叠所使用的命令
foldtext	fdt	显示关闭的折叠所用的表达式
formatlistpat	flp	识别列表头部的模式
formatoptions	fo	自动排版完成的方式
formatprg	fp	"gq" 命令使用的外部程序
formatexpr	fex	"gp" 命令使用的表达式
fsync	fs	文件写回后是否激活 fsync()
G
选项全称	选项简称	选项说明
gdefault	gd	缺省打开 ":substitute" 的 'g' 标志
grepformat	gfm	'grepprg' 的输出格式
grepprg	gp	":grep" 使用的程序
guicursor	gcr	GUI: 光标形状和闪烁的设置
guifont	gfn	GUI: 使用的字体名
guifontset	gfs	GUI: 使用的多字节字体名
guifontwide	gfw	双倍宽度字符的字体名列表
guiheadroom	ghr	GUI: 用于窗口装饰的像素空间
guioptions	go	GUI: 使用的部件和选项
guipty		GUI: ":!" 命令尝试仿终端
guitablabel	gtl	GUI: 标签页定制的标签
guitabtooltip	gtt	GUI: 标签页定制的工具提示
H
选项全称	选项简称	选项说明
helpfile	hf	主帮助文件的完整路径名
helpheight	hh	新帮助窗口的最小高度
helplang	hlg	首选帮助语言
hidden	hid	当缓冲区被放弃 (|abandon|) 时不挂载之
highlight	hl	设置若干场合下的高亮模式
hlsearch	hls	高亮最近的匹配搜索模式
history	hi	记住的命令行的行数
hkmap	hk	希伯来语的键盘映射
hkmapp	hkp	希伯来语的音节 (phonetic) 键盘映射
I
选项全称	选项简称	选项说明
icon		让 Vim 设定窗口图标的文本
iconstring		Vim 图标文本所用的字符串
ignorecase	ic	搜索模式时忽略大小写
imactivatekey	imak	激活 X 输入方法 (X input method) 的键击
imactivatefunc	imaf	激活/关闭 X 输入方法的函数
imcmdline	imc	开始编辑命令行时使用 IM
imdisable	imd	任何模式下不使用 IM
iminsert	imi	插入模式下使用 :lmap 或 IM
imsearch	ims	输入搜索模式时使用 :lmap 或 IM
imstatusfunc	imsf	获得 X 输入方法的状态的函数
include	inc	查找包含文件所使用的模式
includeexpr	inex	处理包含文件行所使用的表达式
incsearch	is	输入搜索模式时同时高亮部分的匹配
indentexpr	inde	得到一行的缩进位置的表达多
indentkeys	indk	使用 'indentexpr' 时启动缩进的键
infercase	inf	关键字自动补全的匹配调整大小写
insertmode	im	开始编辑文件时进入插入模式
isfname	isf	文件和路径名可用的字符
isident	isi	标识符可用的字符
iskeyword	isk	关键字可用的字符
isprint	isp	可显示的字符
J
选项全称	选项简称	选项说明
joinspaces	js	连接命令在句号之后加两个空格
K
选项全称	选项简称	选项说明
key		加密密钥
keymap	kmp	键盘映射名
keymodel	km	允许用键击开始/停止选择
keywordprg	kp	"K" 命令所使用的程序
L
选项全称	选项简称	选项说明
langmap	lmap	其他语言模式用的字母表字符
langmenu	lm	菜单使用的语言
laststatus	ls	当最近的窗口有状态行时提示
lazyredraw	lz	执行宏时不重画
linebreak	lbr	在空白处回绕长行
lines		显示屏幕的行数
linespace	lsp	字符之间的像素行数
lisp		自动 lisp 缩进
lispwords	lw	改变 lisp 缩进方式的单词
list		显示` <Tab>` 和 `<EOL>`
listchars	lcs	list 模式下显示用的字符
loadplugins	lpl	启动时调入插件脚本
M
选项全称	选项简称	选项说明
macatsui		Mac GUI: 使用 ATSUI 文本绘制
magic		改变搜索模式所用的特殊字符
makeef	mef	":make" 所用的错误文件名
makeprg	mp	":make" 命令所用的程序
matchpairs	mps	"%" 能匹配的字符对
matchtime	mat	显示匹配括号的时间 (以十分之一秒计)
maxcombine	mco	显示的最大组合用字符数
maxfuncdepth	mfd	用户函数的最大递归深度
maxmapdepth	mmd	映射的最大递归深度
maxmem	mm	单个缓冲区可用的最大内存 (以千字节计)
maxmempattern	mmp	模式匹配使用的最大内存 (以千字节计)
maxmemtot	mmt	所有缓冲区可用的最大内存 (以千字节计)
menuitems	mis	菜单可用的最大项目数
mkspellmem	msm	在 |:mkspell| 压缩树前可用的内存
modeline	ml	在文件开头或结尾识别模式行
modelines	mls	模式行的检查行数
modifiable	ma	可否修改文本
modified	mod	缓冲区已被修改
more		全屏显示时暂停列表
mouse		允许使用鼠标
mousefocus	mousef	键盘焦点追随鼠标点击
mousehide	mh	输入时隐藏鼠标指针
mousemodel	mousem	改变鼠标按钮的含义
mouseshape	mouses	不同模式下改变鼠标指针的形状
mousetime	moukset	鼠标双击之间的最大时间
mzquantum	mzq	MzScheme 线程的轮询间隔
N
选项全称	选项简称	选项说明
nrformats	nf	CTRL-A 命令识别的数字格式
number	nu	行前显示行号
numberwidth	nuw	行号使用的列数
O
选项全称	选项简称	选项说明
omnifunc	ofu	文件类型特定补全使用的函数
opendevice	odev	MS-Windows 上允许读/写设备
operatorfunc	opfunc	|go@| 操作符调用的函数
osfiletype	oft	不再支持
P
选项全称	选项简称	选项说明
paragraphs	para	分隔段落的 nroff 宏
paste		允许粘贴文本
pastetoggle	pt	切换 'paste' 的键盘代码
patchexpr	pex	用于给文件打补丁的表达式
patchmode	pm	保留文件最老的版本
path	pa	"gf" 等命令搜索用的目录列表
preserveindent	pi	重排时保持原有的缩进结构
previewheight	pvh	预览窗口的高度
previewwindow	pvw	标识预览窗口
printdevice	pdev	用于 :hardcopy 的打印机名
printencoding	penc	用于打印的编码方式
printexpr	pexpr	用于 :hardcopy 打印 PostScript 的表达式
printfont	pfn	用于 :hardcopy 的字体名
printheader	pheader	用于 :hardcopy 的页眉格式
printmbcharset	pmbcs	用于 :hardcopy 的 CJK 字符集
printmbfont	pmbfn	用于 :hardcopy 的 CJK 输出的字体名
printoptions	popt	控制 :hardcopy 输出格式
pumheight	ph	弹出窗口的最大高度
Q
选项全称	选项简称	选项说明
quoteescape	qe	字符串里使用的转义字符
R
选项全称	选项简称	选项说明
readonly	ro	禁止写入缓冲区
redrawtime	rdt	'hlsearch' 和 |:match| 高度的超时
regexpengine	re	使用的缺省正规表达式引擎
relativenumber	rnu	每行前显示相对行号
remap		允许映射可以递归调用
report		报告行改变的行数下限
restorescreen	rs	Win32: 退出时恢复屏幕
revins	ri	字符插入会反向进行
rightleft	rl	窗口为从右到左模式
rightleftcmd	rlc	从右到左模式工作的编辑命令
ruler	ru	标尺，在状态行里显示光标的行号和列号
rulerformat	ruf	定制标尺格式
runtimepath	rtp	用于运行时文件的目录列表
S
选项全称	选项简称	选项说明
scroll	scr	用 CTRL-U 和 CTRL-O 滚动的行数
scrollbind	scb	其他窗口滚动时滚动当前窗口
scrolljump	sj	滚动所需的最少行数
scrolloff	so	光标上下的最少行数
scrollopt	sbo	'scrollbind' 的行为方式
sections	sect	分隔小节的 nroff 宏
secure		在当前目录下以安全模式读入 .vimrc
selection	sel	使用何种选择方式
selectmode	slm	何时使用选择模式而不是可视模式
sessionoptions	ssop	:mksession 的选项
shell	sh	使用外部命令的 shell 程序名字
shellcmdflag	shcf	执行命令所使用的 shell 的参数
shellpipe	sp	把 :make 结果输出到错误文件的字符串
shellquote	shq	括起 shell 命令的字符
shellredir	srr	把过滤命脉的输出存到暂时文件的字符串
shellslash	ssl	shell 文件名使用正斜杠
shelltemp	stmp	shell 命令是否使用临时文件
shelltype	st	Amiga: 影响如何使用 shell
shellxescape	sxe	'shellxquote' 为 ( 时使用的转义字符
shellxquote	sxq	类似于 'shellquote'，但包括重定向
shiftround	sr	缩进列数对齐到 shiftwidth 的整数倍
shiftwidth	sw	(自动) 缩进使用的步进单位，以空白数目计
shortmess	shm	缩短消息长度的标志位列表
shortname	sn	非 MS-DOS: 文件名假定为 8.3字符
showbreak	sbr	用于提示回绕行开始的字符串
showcmd	sc	在状态行里显示 (部分) 命令
showfulltag	sft	自动补全标签时显示完整的标签匹配模式
showmatch	sm	插入括号时短暂跳转到匹配的括号
showmode	smd	在状态行上显示当前模式的消息
showtabline	stal	是否显示标签页行
sidescroll	ss	横向滚动的最少列数
sidescrolloff	siso	在光标左右最少出现列数
smartcase	scs	模式中有大写字母时不忽略大小写
smartindent	si	C 程序智能自动缩进
smarttab	sta	插入 `<Tab>` 时使用 'shiftwidth'
softtabstop	sts	编辑时 `<Tab>` 使用的空格数
spell		打开拼写检查
spellcapcheck	spc	定位句子尾部的模式
spellfile	spf	|zg| 和 |zw| 保存单词的文件
spelllang	spl	拼写检查使用的语言
spellsuggest	sps	提供拼写校正建议的方法
splitbelow	sb	分割窗口时新窗口在当前窗口之下
splitright	spr	新窗口在当前窗口之右
startofline	sol	命令移动光标到行的第一个非空白
statusline	stl	状态行的定制格式
suffixes	su	多个匹配所忽略的后缀
suffixesadd	sua	搜索文件时附加的后缀
swapfile	swf	缓冲区是否使用交换文件
swapsync	sws	和交换文件同步的方式
switchbuf	swb	设置切换到别的缓冲区时的行为
synmaxcol	smc	寻找语法项目的最大列数
syntax	syn	读入当前缓冲区的语法
T
选项全称	选项简称	选项说明
tabstop	ts	`<Tab>` 在文件里使用的空格数
tabline	tal	终端标签页行的定制格式
tabpagemax	tpm	|-p| 和 "tab all" 的最大标签页数
tagbsearch	tbs	标签文件里用二分法查找
taglength	tl	标签里的有效字符数
tagrelative	tr	标签文件里的文件名是相对路径
tags	tag	标签命令使用的文件名列表
tagstack	tgst	把标签推入标签栈
term		终端名
termbidi	tbidi	终端支持双向文本
termencoding	tenc	终端使用的编码方式
terse		简化部分消息
textauto	ta	废止，用 'fileformats'
textmode	tx	废止，用 'fileformat'
textwidth	tw	插入文本的最大宽度
thesaurus	tsr	关键字自动补全手忙脚乱的同义词字典
tildeop	top	波浪命令 "~" 以操作符方式工作
timeout	to	映射和键盘代码等待超时
timeoutlen	tm	超时时间 (以毫秒计)
title		让 Vim 设置窗口标题
titlelen		用于窗口标题 'columns' 比例
titleold		旧的标题，用于退出时恢复
titlestring		用于 Vim 窗口标题的字符串
toolbar	tb	GUI: 工具栏显示何种项目
toolbariconsize	tbis	工具栏图标的大小 (只适用于 GTK 2)
ttimeout		映射等待超时
ttimeoutlen	ttm	键盘代码超时时间 (以毫秒计)
ttybuiltin	tbi	在外部 termcap 之前先用内建的 termcap
ttyfast	tf	指示一个快速的终端链接
ttymouse	ttym	鼠标产生代码的类型
ttyscroll	tsl	滚动的最大行数
ttytype	tty	'term' 的别名
U
选项全称	选项简称	选项说明
undodir	udir	保存撤销文件的位置
undofile	udf	把撤销信息写入一个文件里
undolevels	ul	最多可以撤销的改变个数
undoreload	ur	保存缓冲区重载撤销的最大行数
updatecount	uc	刷新交换文件所需的字符数
updatetime	ut	刷新交换文件所需的毫秒数
V
选项全称	选项简称	选项说明
verbose	vbs	给出详细信息
verbosefile	vfile	消息写入的文件
viewdir	vdir	:mkview 存储文件的所在目录
viewoptions	vop	指定 :mkview 保存的内容
viminfo	vi	启动和退出时使用 .viminfo 文件
virtualedit	ve	何时使用虚拟编辑
visualbell	vb	使用可视铃声而不是响铃
W
选项全称	选项简称	选项说明
warn		当缓冲区改变时，对 shell 命令给出警告
weirdinvert	wiv	用于有特殊反转方法的终端
whichwrap	ww	允许指定键跨越行边界
wildchar	wc	用于符扩展的命令行字符
wildcharm	wcm	同 'wildchar'，但对映射情况也适用
wildignore	wig	匹配这些模式的文件不会参与自动补全
wildignorecase	wic	匹配文件名时忽略大小写
wildmenu	wmnu	命令行自动补全所使用的菜单
wildmode	wim	'wildchar' 命令行扩展所用的模式
wildoptions	wop	指定如何完成命令行补全
winaltkeys	wak	休时窗口系统处理 ALT 键
window	wi	CTRL-F 和 CTRL-B 滚动的行数
winheight	wh	当前窗口的最少行数
winfixheight	wfh	打开/关闭窗口时保持窗口高度
winfixwidth	wfw	打开/关闭窗口时保持窗口宽度
winminheight	wmh	任何窗口的最少行数
winminwidth	wmw	任何窗口的最少列数
winwidth	wiw	当前窗口的最少列数
wrap		长行回绕并在下一行继续
wrapmargin	wm	使 (硬) 回绕开始的从右侧起算的字符数
wrapscan	ws	搜索在文件尾折回文件头
write		允许写入文件
writeany	wa	写入文件不需 "!" 强制
writebackup	wb	覆盖文件时建立备份
writedelay	wd	每个字符延迟 (以毫秒计) (用于调试)
Vim专业手册339页
```


为 vim 安装 dracula 后无法高亮函数，与 vscode 不一致，在网上查找解决方案：

参考：

- 知乎： kevin bright Vim C/C++ 函数名，宏定义和变量的高亮
- invisprings.github.io Vim 函数高亮
- cnblogs VIM C 语言函数高亮


vim 默认无法高亮函数名，可修改 Vim\vim90\syntax\c.vim 文件
在最后加入：

```
syn match cFunctions "\<[a-zA-Z_][a-zA-Z_0-9]*\>[^()]*)("me=e-2
syn match cFunctions "\<[a-zA-Z_][a-zA-Z_0-9]*\>\s*("me=e-1
"hi cFunctions guifg=green gui=bold cterm=None ctermfg=None
hi cFunctions guifg=green
```
**括号自动补全配置**

```sh
function CloseBracket()
 if match(getline(line('.') + 1), '\s*}') < 0
 return "\<CR>}"
 else
 return "\<Esc>j0f}a"
 endif
endf

function! AutoPair(open, close)
        let line = getline('.')
        if col('.') > strlen(line) || line[col('.') - 1] == ' '
                return a:open.a:close."\<ESC>i"
        else
                return a:open
        endif
endf

 function! ClosePair(char)
         if getline('.')[col('.') - 1] == a:char
                 return "\<Right>"
         else
                 return a:char
         endif
 endf

 function! SamePair(char)
         let line = getline('.')
         if col('.') > strlen(line) || line[col('.') - 1] == ' '
                 return a:char.a:char."\<ESC>i"
         elseif line[col('.') - 1] == a:char
                 return "\<Right>"
         else
                 return a:char
         endif
 endf

inoremap ( <c-r>=AutoPair('(', ')')<CR>
inoremap ) <c-r>=ClosePair(')')<CR>
inoremap { {<CR>}<ESC>O
"inoremap } <c-r>=ClosePair('}')<CR>
inoremap } <c-r>=CloseBracket()<CR>
inoremap [ <c-r>=AutoPair('[', ']')<CR>
inoremap ] <c-r>=ClosePair(']')<CR>
inoremap " <c-r>=SamePair('"')<CR>
inoremap ' <c-r>=SamePair("'")<CR>
inoremap ` <c-r>=SamePair('`')<CR>
```
参考： https://www.douban.com/note/299644770/?_i=1701686uJvjPfr

https://www.cnblogs.com/huanlei/archive/2012/04/02/2430153.html

https://segmentfault.com/a/1190000000640039

`:term` 打开 vim 内置终端

`exit` 退出终端

`c-w :hide` 隐藏终端。

`ls` 在缓冲区中找到，`:sp` `:bnum` 恢复终端。

`c-w :q!` 强制退出，但实际上还在缓冲区。

折叠：

`Marker Fold`

`set foldmethod=marker` 默认是 `{{{` 以及 `}}}`

```perl
# {{{
function do_something {

}
# }}}
```

若设置为 手动折叠

`set foldmethod=manual`

手动建立折叠区块，zf 建立。

可以利用 autocmd 加上 mkview loadview 储存手动建立的折叠区块，会被放到 `~/.vim/view` 里。

```
autocmd BufWinLeave *.* silent mkview
autocmd BufWinEnter *.* silent loadview
```

`set equalprg=perltidy` 针对特定区域格式化程序，选择文件区块后，`=` 可使用 perltidy 程序来做格式化处理。

`autocmd Filetype perl :set equalprg=perltidy` 针对文件类型做 equalprg 设定。

`autocmd Filetype c :set equalprg=indent` c 语言使用外部的 GNU indent 做格式化处理

`autocmd Filetype sql :set equalprg=sql-beautify.pl` sql 格式化例子

**QuickFix**

填充quickfix列表的一些命令

:make

:grep

:vimgrep

:Ag

`:copen` 打开 quickfix 窗口。

`:cclose` 关闭 quickfix 窗口。

`:make` 默认 gnu-make，并把 make 执行结果 显示到 quickfix 中

`:grep`  默认 vimgrep

[vi/vim使用进阶: 剑不离手 – quickfix](https://blog.easwy.com/archives/advanced-vim-skills-quickfix-mode/)
[vim quickfix——最灵活的quickfix](https://blog.csdn.net/niuiic/article/details/115800729)
[vim 能帮我们什么](https://www.doc88.com/p-8778593994701.html)

[vim 对长行的处理](http://blog.chinaunix.net/uid-20147410-id-311663.html)

用gVim来写文章，一个自然段就是一行，常常会碰到由于是文章的一段话，这一行字会特别长的情况，打开自动折行，要好几行甚至十多行才能显示完全。这这 种情况下，vim只会在在当前窗口下能把整个段落完全显示的时候，才将其显示；而在不能完整显示的情况，它会用@来代替，set display=lastline 让vim在当前窗口能显示这行字的多少就显示多少，而不是等整行字都能显示时才将其显示出来。
另外还可以用gj和gk可以上下移动屏幕显示的一行。

新的问题出现了：如果一行文本有几千汉字时，gVim的支持非常差，右边滚动条滚动和鼠标滚动毫不自然，有时很难凭借滚动来移动到自己想要到的位 置。如果用gj和gk来移动，尤如隔靴搔痒，gVim的高效性荡然无存。

在模式行中加上set fo+=mM，然后就能自动对中文换行了，注意是真正的换行，不是折行，如果修改后可以用gq命令重新格式化，用起来相当方便。

[vim 格式化代码](https://www.cnblogs.com/AI-Algorithms/p/3774409.html)

" 采用 C 风格的缩进，适用于大多数语言
" 细节调整见下面的 `cinoptions`
" 你也可以尝试 smartindent 和 autoindent
set cindent

" 细节调整，主要为了适应 Google C++ Style
" t0: 函数返回类型声明不缩进
" g0: C++ "public:" 等声明缩进一个字符
" h1: C++ "public:" 等声明后面的语句缩进一个字符
" N-s: C++ namespace 里不缩进
" j1: 合理的缩进 Java 或 C++ 的匿名函数，应该也适用于 JS
  (N 在没有结束的括号内，相对没有结束的括号所在行进行 N 个字符的缩
              进。对每一个额外没有结束的括号增加 'shiftwidth' 的缩进。如果 N
              为 0，或没有结束的括号是其所在行的首个非空白字符，和括号之后下一
              个非空白字符对齐。
set cinoptions=t0,g1,h1,N-s,j1


**cscope 函数跳转后返回,按ctrl+t 没有用?**

`set cscopetagorder=1`

因为默认使用 cscope 的数据库。

`:X` 文本加密


vim -u 配置文件或gvim -U 配置文件。

**normal命令**


在~/.vim/ftplugin/ 目录下面找到特定语言对应的配置文件。
比如在我的ubuntu下找到了~/.vim/ftplugin/cpp.vim ，在最后一行加上了

`:imap { {<CR>}<ESC>O`

这样对于所有的cpp 文件这个设置都会生效。但是如果是其它扩展名的文件则不生效。

或者 /usr/share/vim/vim82/syntax/c.vim 中

```
syn match cFunctions "\<[a-zA-Z_][a-zA-Z_0-9]*\>[^()]*)("me=e-2
syn match cFunctions "\<[a-zA-Z_][a-zA-Z_0-9]*\>\s*("me=e-1
"hi cFunctions guifg=green gui=bold cterm=None ctermfg=None
hi cFunctions guifg=green

function! ClosePair(char)
        if getline('.')[col('.') - 1] == a:char
                return "\<Right>"
        else
                return a:char
        endif
endf

inoremap { {<CR>}<ESC>O
inoremap } <c-r>=CloseBracket()<CR>
```

[vim 如何对不同的语言采用不同的键映射](https://segmentfault.com/q/1010000010011493)

:Ex 开启目录浏览器，可以浏览当前目录下的所有文件，并可以选择
:Sex 水平分割当前窗口，并在一个窗口中开启目录浏览器
:Vex 垂直切割当前窗口
:ls 显示当前buffer情况

`:term` vim 中打开内置终端。

`:shell` 当前目录调用命令终端

`zR` 打开所有折叠以及嵌套折叠

`zM` 关闭所有折叠以及嵌套折叠。

`zO` 对所在范围内所有嵌套的折叠点展开

`zC` 对所在范围内所有嵌套的折叠点进行折叠

`w !sudo tee %` sudo 保存文件。

`Man` 命令带高亮和跳转。

```
text-object

动词 : c(hange) d(elete)
副词 : i(nside) a(round) t(o) f(orward)
名词 : w(ord) s(entence) p(aragraph) t(ag) ` ‘ “ [ ( {
tag 是 markup 语言中的 tag，例如 <h2> hi </h2>
```

`ctags` 对 c++ 的支持：

` ctags -R --kinds-c++=+p --fields=+aiKSz --extra=+q --langmap=c++:+.inl .`

https://blog.csdn.net/superbobpig/article/details/2533904

`ctags -R --kinds-c++=+p --fields=+iaS --extra=+q --language-force=c++ .` 直接当作 c++ 文件处理

https://blog.csdn.net/superbobpig/article/details/2533904

`ctags -R --languages=c++ --langmap=c++:+.inl -h +.inl --c++-kinds=+px --fields=+aiKSz --extra=+q --exclude=lex.yy.cc --exclude=copy_lex.yy.cc`

原文链接：https://blog.csdn.net/ch122633/article/details/54348576

`ctags -R --sort=yes --c++-kinds=+p --fields=+iaS --extra=+q --language-force=C++ -f <生成的tag文件名> .`

https://timothyqiu.com/archives/using-omnicomplete-for-c-cplusplus-in-vim/

[vim 中OmniCppComplete的安装和使用](https://blog.csdn.net/duguteng/article/details/7417181)

`c-e` 停止补全。

`c-y` 接受补全并停止。

我常用的 ctags 命令：

`ctags -R --sort=yes --c++-kinds=+px --fields=+iaKSz --extras=+q`

接着，执行 ctags 生成标准库的标签文件：

```
cd /usr/include/c++/4.8
ctags -R --c++-kinds=+l+x+p --fields=+iaSl --extra=+q --language-force=c++ -f stdcpp.tags
sudo ctags -R --sort=yes --c++-kinds=+px --fields=+iaKSz --extras=+q --language-force=C++ -f stdcpp.ctags
然后，让 OmniCppComplete 成功识别标签文件中的标准库接口。C++ 标准库源码文件中使用了 _GLIBCXX_STD 名字空间
（GNU C++ 标准库的实现是这样，如果你使用其他版本的标准库，需要自行查找对应的名字空间名称），
标签文件里面的各个标签都嵌套在该名字空间下，所以，要让 OmniCppComplete 正确识别这些标签，
必须显式告知 OmniCppComplete 相应的名字空间名称。在.vimrc中增加如下内容：

let OmniCpp_DefaultNamespaces = ["_GLIBCXX_STD"]
最后，在 VIM 中引入该标签文件。在 .vimrc 中增加如下内容：

set tags+=/usr/include/c++/4.8/stdcpp.tags
```

-- [像IDE 一样使用 Vim](https://github.com/yangyangwithgnu/use_vim_as_ide)


[Vim 中使用 OmniComplete 为 C/C++ 自动补全](https://timothyqiu.com/archives/using-omnicomplete-for-c-cplusplus-in-vim/)

`:find filename` 查找文件。



```
ma 书签
delmarks 删除书签
`a
'a 跳转
```