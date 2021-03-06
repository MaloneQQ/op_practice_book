# Linux 工具篇

<!-- vim-markdown-toc GFM -->
* [vim](#vim)
    * [快捷键](#快捷键)
        * [Movement](#movement)
        * [Search](#search)
        * [Deletion](#deletion)
        * [Yank & Put](#yank--put)
        * [Insert Mode](#insert-mode)
        * [Visual Mode](#visual-mode)
        * [Other](#other)
    * [技巧](#技巧)
        * [shell 多行注释](#shell-多行注释)
        * [自动补全](#自动补全)
        * [左右分割打开 help 文档](#左右分割打开-help-文档)
        * [逐个替换](#逐个替换)
        * [关于 search/replace 中的换行符](#关于-searchreplace-中的换行符)
    * [vim IDE 工具](#vim-ide-工具)
* [sed](#sed)
* [awk](#awk)
    * [历史](#历史)
    * [基础知识](#基础知识)
        * [分隔符](#分隔符)
        * [内建变量](#内建变量)
        * [转义](#转义)
        * [模式](#模式)
        * [单引号](#单引号)
    * [脚本](#脚本)
    * [运算与编程](#运算与编程)
    * [Example](#example)
        * [统计](#统计)
* [Git- 分布式管理系统](#git--分布式管理系统)
    * [Git 基础](#git-基础)
        * [环境配置](#环境配置)
        * [基本操作](#基本操作)
        * [分支](#分支)
        * [标签](#标签)
        * [Git shortcuts/aliases](#git-shortcutsaliases)
    * [知识点](#知识点)
        * [文件的几种状态](#文件的几种状态)
        * [快照和差异](#快照和差异)
        * [Git 数据结构](#git-数据结构)
    * [其他操作](#其他操作)
        * [解决 GitHub commit 次数过多.git 文件过大](#解决-github-commit-次数过多git-文件过大)
        * [fatal: HTTP request failed](#fatal-http-request-failed)
* [curl](#curl)
    * [curl 基础](#curl-基础)
        * [直接获取（GET）一个 url](#直接获取get一个-url)
        * [post，put 等](#postput-等)
        * [form 表单提交](#form-表单提交)
    * [curl 深入](#curl-深入)
        * [显示头信息](#显示头信息)
        * [详细显示通信过程](#详细显示通信过程)
        * [设置头信息](#设置头信息)
        * [Referer 字段](#referer-字段)
        * [包含 cookie](#包含-cookie)
        * [自动跳转](#自动跳转)
        * [http 认证](#http-认证)
* [screen](#screen)
    * [screen 使用](#screen-使用)
        * [新建一个 Screen Session](#新建一个-screen-session)
        * [将当前 Screen Session 放到后台](#将当前-screen-session-放到后台)
        * [唤起一个 Screen Session](#唤起一个-screen-session)
        * [分享一个 Screen Session](#分享一个-screen-session)
        * [终止一个 Screen Session](#终止一个-screen-session)
        * [查看一个 screen 里的输出](#查看一个-screen-里的输出)
    * [开启 screen 状态栏](#开启-screen-状态栏)
* [tcpdump](#tcpdump)
    * [tcp 三次握手和四次挥手](#tcp-三次握手和四次挥手)
        * [三次握手](#三次握手)
        * [四次挥手](#四次挥手)
    * [tcpdump 使用](#tcpdump-使用)
        * [针对特定网口抓包(-i选项)](#针对特定网口抓包-i选项)
        * [指定抓包端口](#指定抓包端口)
        * [抓取特定目标ip和端口的包](#抓取特定目标ip和端口的包)
        * [增加抓包时间戳(-tttt选项)](#增加抓包时间戳-tttt选项)

<!-- vim-markdown-toc -->

# vim
## 快捷键

### Movement
* `h`  - Move *left*
* `j`  - Move *down*
* `k`  - Move *up*
* `l`  - Move *right*
* `0`  - Move to *beginging* of line, 也可以使用 `Home`.
* `^`  - 在有 tab 或 space 的代码行里，`0` 是移到最行首，而 `^` 是移到代码行首
* `$`  - Move to *end* of line
* `gg` - Move to *first* line of file
* `G`  - Move to *last* line of file
* `ngg`- 移动到指定的第 n 行，也可以用 `nG`
* `w`  - Move *forward* to next word
* `b`  - Move *backward* to next word
* `%`  - 在匹配的括号、块的首尾移动
* `C-o`- 返回到上次移动前的位置，也可以用两个单引号 `'`
* `C-i`- 前进到后一次移动的位置
* `f`  - 后接字符，移动到当前行的下一个指定字符，然后按 `;` 继续搜索下一个
* `F`  - 同上，移动到上一个
* `|`  - 竖线，前接数字，移动到当前行的指定列，如 `30|` ，移动到当前行的第 30 列

### Search
* `*`     - Search *forward* for word under cursor
* `#`     - Search *backward* for word under curor
* `/word` - Search *forward* for *word*. Support *RE*
* `?word` - Search *backward* for *word*. Support *RE*
* `n`     - Repeat the last `/` or `?` command
* `N`     - Repeat the last `/` or `?` command in opposite direction

在搜索后，被搜索的单词都会高亮，一般想取消那些高亮的单词，可以再次搜索随便输入一些字母，搜索不到自然就取消了。另外也可以使用 `nohl` 取消这些被高亮的词。

### Deletion
* `x`  - Delete character *forward*(under cursor), and remain in normal mode
* `X`  - Delete character *backward*(before cursor), and remain in normal mode
* `r`  - Replace single character under cursor, and remain in normal mode
* `s`  - Delete single character under cursor, and *switch* to insert mode
* `shift+~` - 这个可以把光标下的单词转换为大写 / 小写，并自动移到下一个字符
* `dw` - Delete a *word* forward
* `daw`- 上面的 `dw` 是删除一个单词的前向部分，而这个是删除整个单词，不论 cursor 是否在单词中间
* `db` - Delete a *word* backward
* `dd` - Delete *entire* current line
* `D`  - Delete until end of line


### Yank & Put
* `y`   - Yank(copy)
* `yy`  - Yank current line
* `nyy` - Yank `n` lines form current line
* `p`   - Put(paste) yanked text *below* current line
* `P`   - Put(paste) yanked text *above* current line

### Insert Mode ###
* `i` - Enter insert mode to the *left* of the cursor
* `a` - Enter insert mode to the *right* of the cursor
* `o` - Enter insert mode to the line *below* the current line
* `O` - Enter insert mode to the line *above* the current line

### Visual Mode
* `v`   - Enter visual mode, highlight characters
* `V`   - Enter visual mode, highlight lines
* `C-v` - Enter visual mode, highlight block

### Other
* `u`   - Undo
* `U`   - Undo all changes on current line
* `C-r` - Redo

## 技巧

### shell 多行注释

命令行模式下，注释掉 line1 与 line2 之间的行

    line1,line2s/^/#/g


### 自动补全

    Ctrl+n Ctrl+p
    Ctrl+x Ctrl+?{....}

### 左右分割打开 help 文档

默认是上下分割来打开文档，但是对于宽屏，左右分割反而更加方便

    :vert help xxx


### 逐个替换

全文直接替换：

    :%s/old_str/new_str/g

加上参数 c 可以逐个替换，这样可以对每一个再确认：

    :%s/old_str/new_str/gc


### 关于 search/replace 中的换行符

Search:

`\n` is `newline`, `\r` is `CR`(carriage return = Ctrl-M = ^M)

Replace:

`\r` is newline, `\n` is a null byte(0x00)

比如字符串 test1,test2,test3 把逗号换成换行：

    %s/,/\r/g

## vim IDE 工具

* [VIM 一键 IDE](https://github.com/BillWang139967/Vim)


# sed

# awk
## 历史

AWK 是贝尔实验室 1977 年搞出来的文本处理工具。

之所以叫 AWK 是因为其取了三位创始人 Alfred Aho，Peter Weinberger, 和 Brian Kernighan 的 Family Name 的首字符

## 基础知识
### 分隔符

默认情况下， awk 使用空格当作分隔符。分割后的字符串可以使用 $1, $2 等访问。

上面提到过，我们可以使用 -F 来指定分隔符。
fs 如果是一个字符，可以直接跟在 -F 后面，比如使用冒号当作分隔符就是 -F: .
如果分隔符比较复杂，就需要使用正则表达式来表示这个分隔符了。
正则表达式需要使用引号引起来。
比如使用‘ab’  当作分隔符，就是 -F 'ab' 了。
使用 a 或 b 作为分隔符，就是 -F '\[ab]' 了。
关于正则表达式这里不多说了。

### 内建变量

```text
$0	当前记录（这个变量中存放着整个行的内容）
$1~$n	当前记录的第 n 个字段，字段间由 FS 分隔
FS	输入字段分隔符 默认是空格或 Tab
NF	当前记录中的字段个数，就是有多少列
NR	已经读出的记录数，就是行号，从 1 开始，如果有多个文件话，这个值也是不断累加中。
FNR	当前记录数，与 NR 不同的是，这个值会是各个文件自己的行号
RS	输入的记录分隔符， 默认为换行符
OFS	输出字段分隔符， 默认也是空格
ORS	输出的记录分隔符，默认为换行符
FILENAME	当前输入文件的名字
```

### 转义

一般字符在双引号之内就可以直接原样输出了。
但是有部分转义字符，需要使用反斜杠转义才能正常输出。

```
\\   A literal backslash.
\a   The “alert” character; usually the ASCII BEL character.
\b   backspace.
\f   form-feed.
\n   newline.
\r   carriage return.
\t   horizontal tab.
\v   vertical tab.
\xhex digits
\c   The literal character c.
```
### 模式

```text
~ 表示模式开始
/ / 中是模式
! 模式取反
```

### 单引号

当需要输出单引号时，直接转义发现会报错。
由于 awk 脚本并不是直接执行，而是会先进行预处理，所以需要两次转义。
awk 支持递归引号。单引号内可以输出转义的单引号，双引号内可以输出转义的双引号。

比如需要输出单引号，则需要下面这样：

```
> awk 'BEGIN{print "\""}'
"
>  awk 'BEGIN{print "'\''"}'
'
```

当然，更简单的方式是使用十六进制来输出。

```
awk 'BEGIN{print "\x27"}'
```

## 脚本

```text
BEGIN{ 这里面放的是执行前的语句 }
END {这里面放的是处理完所有的行后要执行的语句 }
{这里面放的是处理每一行时要执行的语句}
```

## 运算与编程

awk 是弱类型语言，变量可以是串，也可以是数字，这依赖于实际情况。
所有的数字都是浮点型。

例如

```bash
//9
echo 5 4 | awk '{ print $1 + $2 }'

//54
echo 5 4 | awk '{ print $1 $2 }'

//"5 4"
echo 5 4 | awk '{ print $1, $2 }'

0-1-2-3-4-5-6
echo 6 | awk '{ for (i=0; i<=$0; i++){ printf (i==0?i:"-"i); }printf "\n";}'
```

## Example

假设我们有一个日期 2014/03/27, 我们想处理为 2014-03-27.
我们可以使用下面的代码实现。

```bash
echo "2014/03/27" | awk -F/  '{print $1"-"$2"-"$3}'
```

假设 处理的日期都在 date 文件里。
我们可以导入文件来操作

文件名 date

```text
2014/03/27
2014/03/28
2014/03/29
```

命令
```bash
awk -F/ '{printf "%s-%s-%s\n",$1,$2,$3}'  date
```

输出
```text
2014-03-27
2014-03-28
2014-03-29
```

### 统计

```bash
awk '{sum+=$5} END {print sum}'
```

# Git- 分布式管理系统

## Git 基础

### 环境配置

+ `git config user.name your_name` : 设置你的用户名，提交会显示
+ `git config user.email your_email` : 设置你的邮箱
+ `git config core.quotepath false` : 解决中文文件名显示为数字问题

### 基本操作

+ `git init` : 初始化一个 git 仓库
+ `git add <filename>` : 添加一个文件到 git 仓库中
+ `git commit -m "commit message"`: 提交到本地
+ `git push [remote-name] [branch-name]` : 把本地的提交记录推送到远端分支
+ `git pull`: 更新仓库 `git pull` = `git fetch` + `git merge`
+ `git checkout -- <file>` : 还原未暂存 (staged) 的文件
+ `git reset HEAD <file>...` : 取消暂存，那么还原一个暂存文件，应该是先 `reset` 后 `checkout`
+ `git stash` : 隐藏本地提交记录，恢复的时候 `git stash pop`。这样可以在本地和远程有冲突的情况下，更新其他文件

### 分支

+ `git branch <branch-name>` : 基于当前 commit 新建一个分支，但是不切换到新分支
+ `git checkout -b <branch-name>` : 新建并切换分支
+ `git checkout <branch-name>` : 切换分支
+ `git branch -d <branch-name>` : 删除分支
+ `git push origin <branch-name>` : 推送本地分支
+ `git checkout -b <local-branch-name> origin/<origin-branch-name>` : 基于某个远程分支新建一个分支开发
+ `git checkout --track origin/<origin-branch-name>` : 跟踪远程分支（创建跟踪远程分支，Git 在 `git push` 的时候不需要指定 `origin` 和 `branch-name` ，其实当我们 `clone` 一个 repo 到本地的时候，`master` 分支就是 origin/master 的跟踪分支，所以提交的时候直接 `git push`)。
+ `git push origin :<origin-branch-name>` : 删除远程分支

### 标签

+ `git tag -a <tagname> -m <message>` : 创建一个标签
+ `git tag` : 显示已有的标签
+ `git show tagname`: 显示某个标签的详细信息
+ `git checkout -b <tag-name>` : 基于某个 tag 创建一个新的分支

### Git shortcuts/aliases

    git config --global alias.co checkout
    git config --global alias.br branch
    git config --global alias.ci commit
    git config --global alias.st status

## 知识点

基本命令让你快速的上手使用 Git，知识点能让你更好的理解 Git。

### 文件的几种状态

+ untracked: 未被跟踪的，没有纳入 Git 版本控制，使用 `git add <filename>` 纳入版本控制
+ unmodified: 未修改的，已经纳入版本控制，但是没有修改过的文件
+ modified: 对纳入版本控制的文件做了修改，git 将标记为 modified
+ staged: 暂存的文件，简单理解：暂存文件就是 add 之后，commit 之前的文件状态

理解这几种文件状态对于理解 Git 是非常关键的（至少可以看懂一些错误提示了）。

### 快照和差异

详细可看：[Pro Git: Git 基础](http://iissnan.com/progit/html/zh/ch1_3.html) 中有讲到 *直接记录快照，而非差异比较*，这里只讲我个人的理解。

Git 关心的是文件数据整体的变化，其他版本管理系统（以 svn 为例）关心的某个具体文件的*差异*。这个差异是好理解的，也就是两个版本具体文件的不同点，比如某一行的某个字符发生了改变。

Git 不保存文件提交前后的差异，不变的文件不会发生任何改变，对于变化的文件，前后两次提交则保存两个文件。举个例子：

SVN:

1. 新建 3 个文件 a, b, c，做第一次提交 ->  `version1 : file_a file_b file_c`
2. 修改文件 b， 做第二次提交（真正提交的是 修改后的文件 b 和修改前的 `file_b` 的 diff) -> `version2: diff_b_2_1`
3. 当我要 checkout version2 的时候，实际上得到的是 `file_a file_b+diff_b_2_1 file_c`

Git:

1. 新建 3 个文件 a, b, c，做第一次提交 ->  `version1 : file_a file_b file_c`
2. 修改文件 b （得到`file_b1`), 做第二次提交 -> `version2: file_a file_b1 file_c`
3. 当我要用 version2 的时候，实际上得到的是 `file_a file_b1 file_c`

上面的 `file_a file_b1 file_c` 就是 version2 的 *快照*。

### Git 数据结构

Git 的核心数是很简单的，就是一个链表（或者一棵树更准确一些？无所谓了），一旦你理解了它的基本数据结构，再去看 Git，相信你有不同的感受。继续用上面的例子（所有的物理文件都对应一个 SHA-1 的值）

当我们做第一次提交时，数据结构是这样的：


    sha1_2_file_map:
        28415f07ca9281d0ed86cdc766629fb4ea35ea38 => file_a
        ed5cfa40b80da97b56698466d03ab126c5eec5a9 => file_b
        1b5ca12a6cf11a9b89dbeee2e5431a1a98ea5e39 => file_c

    commit_26b985d269d3a617af4064489199c3e0d4791bb5:
        base_info:
            Auther: "JerryZhang(chinajiezhang@gmail.com)"
            Date: "Tue Jul 15 19:19:22 2014 +0800"
            commit_content: "第一次提交"
        file_list:
            [1]: 28415f07ca9281d0ed86cdc766629fb4ea35ea38
            [2]: ed5cfa40b80da97b56698466d03ab126c5eec5a9
            [3]: 1b5ca12a6cf11a9b89dbeee2e5431a1a98ea5e39
            pre_commit: null
        next_commit: null

当修改了 `file_b`, 再提交一次时，数据结构应该是这样的：

    sha1_2_file_map:
        28415f07ca9281d0ed86cdc766629fb4ea35ea38 => file_a
        ed5cfa40b80da97b56698466d03ab126c5eec5a9 => file_b
        1b5ca12a6cf11a9b89dbeee2e5431a1a98ea5e39 => file_c
        39015ba6f80eb9e7fdad3602ef2b1af0521eba89 => file_b1

    commit_26b985d269d3a617af4064489199c3e0d4791bb5:
        base_info:
            Auther: "JerryZhang(chinajiezhang@gmail.com)"
            Date: "Tue Jul 15 19:19:22 2014 +0800"
            commit_content: "第一次提交"
        file_list:
            [1]: 28415f07ca9281d0ed86cdc766629fb4ea35ea38
            [2]: ed5cfa40b80da97b56698466d03ab126c5eec5a9
            [3]: 1b5ca12a6cf11a9b89dbeee2e5431a1a98ea5e39
        pre_commit: commit_a08a57561b5c30b9c0bf33829349e14fad1f5cff
        next_commit: null

    commit_a08a57561b5c30b9c0bf33829349e14fad1f5cff:
        base_info:
            Auther: "JerryZhang(chinajiezhang@gmail.com)"
            Date: "Tue Jul 15 22:19:22 2014 +0800"
            commit_content: "更新文件 b"
        file_list:
            [1]: 28415f07ca9281d0ed86cdc766629fb4ea35ea38
            [2]: 39015ba6f80eb9e7fdad3602ef2b1af0521eba89
            [3]: 1b5ca12a6cf11a9b89dbeee2e5431a1a98ea5e39
        pre_commit: null
        next_commit: commit_26b985d269d3a617af4064489199c3e0d4791bb5

当提交完第二次的时候，执行 `git log`，实际上就是从 `commit_a08a57561b5c30b9c0bf33829349e14fad1f5cff` 开始遍历然后打印 `base_info` 而已。

实际的 git 实际肯定要比上面的结构 (（的信息）的）要复杂的多，但是它的核心思想应该是就是，每一次提交就是一个新的结点。通过这个结点，我可以找到所有的快照文件。再思考一下，什么是分支？什么是 Tags，其实他们可能只是某次提交的引用而已（一个 `tag_head_node` 指向了某一次提交的 node)。再思考怎么回退一个版本呢？指针偏移！依次类推，上面的基本命令都可以得到一个合理的解释。

**理解 git fetch 和 git pull 的差异**

上面我们说过 `git pull` 等价于 `git fetch` 和 `git merge` 两条命令。当我们 `clone` 一个 repo 到本地时，就有了本地分支和远端分支的概念（假定我们只有一个主分支），本地分支是 `master`，远端分支是 `origin/master`。通过上面我们对 Git 数据结构的理解，`master` 和 `origin/master` 可以想成是指向最新 commit 结点的两个指针。刚 `clone` 下来的 repo，`master` 和 `origin/master` 指针指向同一个结点，我们在本地提交一次，`origin` 结点就更新一次，此时 `master` 和 `orgin/master` 就不再相同了。很有可能别人已经 commit 改 repo 很多次了，并且进行了提交。那么我们的本地的 `origin/master` 就不再是远程服务器上的最新的位置了。 `git fetch` 干的就是从服务器上同步服务器上最新的 `origin/master` 和一些服务器上新的记录 / 文件到本地。而 `git merge` 就是合并操作了（解决文件冲突）。`git push` 是把本地的 `origin/master` 和 `master` 指向相同的位置，并且推送到远程的服务器。

## 其他操作

### 解决 GitHub commit 次数过多.git 文件过大

完全重建版本库

```
# rm -rf .git
# git init
# git add .
# git cm "first commit"
# git remote add origin <your_github_repo_url>
# git push -f -u origin master
```
### fatal: HTTP request failed


使用 git clone 失败

```
[root@localhost ~]# git clone https://github.com/BillWang139967/Vim.git
Initialized empty Git repository in /root/Vim/.git/
error:  while accessing https://github.com/BillWang139967/Vim.git/info/refs

fatal: HTTP request failed
```
解决方法
```
#git config --global http.sslVerify false

```
# curl
## curl 基础
在介绍前，我需要先做两点说明：

1. 下面的例子中会使用 [httpbin.org](http://httpbin.org/) ，httpbin 提供客户端测试 http 请求的服务，非常好用，具体可以查看他的网站。
2. 大部分没有使用缩写形式的参数，例如我使用 `--request` 而不是 `-X` ，这是为了好记忆。

下面开始简单介绍几个命令：

### 直接获取（GET）一个 url

直接以个 GET 方式请求一个 url，输出返回内容：

``` sh
curl httpbin.org
```

返回
``` html
<!DOCTYPE html>
<html>
<head>
  <meta http-equiv='content-type' value='text/html;charset=utf8'>
  <meta name='generator' value='Ronn/v0.7.3 (http://github.com/rtomayko/ronn/tree/0.7.3)'>
  <title>httpbin(1): HTTP Client Testing Service</title>
  <style type='text/css' media='all'>
  /* style: man */
  body#manpage {margin:0}
  .mp {max-width:100ex;padding:0 9ex 1ex 4ex}
  .mp p,.mp pre,.mp ul,.mp ol,.mp dl {margin:0 0 20px 0}
  .mp h2 {margin:10px 0 0 0}
......
```

<!--more-->

### post，put 等

使用 `--request` 指定请求类型， `--data` 指定数据，例如：

``` sh
curl httpbin.org/post --request POST --data "name=keenwon&website=http://keenwon.com"
```

返回：

``` html
{
  "args": {},
  "data": "",
  "files": {},
  "form": {
    "name": "tomshine",
    "website": "http://tomshine.xyz"
  },
  "headers": {
    "Accept": "*/*",
    "Content-Length": "41",
    "Content-Type": "application/x-www-form-urlencoded",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.43.0"
  },
  "json": null,
  "origin": "121.35.209.62",
  "url": "http://httpbin.org/post"
}
```

这个返回值是 httpbin 输出的，可以清晰的看出我们发送了什么数据，非常实用。

### form 表单提交

form 表单提交使用 `--form`，使用 `@` 指定本地文件，例如我们提交一个表单，有字段 name 和文件 f：

``` sh
curl httpbin.org/post --form "name=tomshine" --form "f=@/Users/tomshine/test.txt"
```

返回：

``` json
{
  "args": {},
  "data": "",
  "files": {
    "f": "Hello Curl!\n"
  },
  "form": {
    "name": "tomshine"
  },
  "headers": {
    "Accept": "*/*",
    "Content-Length": "296",
    "Content-Type": "multipart/form-data; boundary=------------------------3bd3dc24dca6daf2",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.43.0"
  },
  "json": null,
  "origin": "112.95.153.98",
  "url": "http://httpbin.org/post"
}
```

## curl 深入
### 显示头信息

使用 `--include` 在输出中包含头信息，使用 `--head` 只返回头信息，例如：

``` sh
curl httpbin.org/post --include --request POST --data "name=tomshine"
```

返回：

``` html
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 18 Sep 2016 01:23:28 GMT
Content-Type: application/json
Content-Length: 363
Connection: keep-alive
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true

{
  "args": {},
  "data": "",
  "files": {},
  "form": {
    "name": "tomshine"
  },
  "headers": {
    "Accept": "*/*",
    "Content-Length": "13",
    "Content-Type": "application/x-www-form-urlencoded",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.43.0"
  },
  "json": null,
  "origin": "121.35.209.62",
  "url": "http://httpbin.org/post"
}
```

再例如，只显示头信息的话：

``` sh
curl httpbin.org --head
```

返回：

``` html
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 18 Sep 2016 01:24:29 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 12150
Connection: keep-alive
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true
```

### 详细显示通信过程

使用 `--verbose` 显示通信过程，例如：

``` sh
curl httpbin.org/post --verbose --request POST --data "name=tomshine"
```

返回：

``` html
*   Trying 54.175.219.8...
* Connected to httpbin.org (54.175.219.8) port 80 (#0)
> POST /post HTTP/1.1
> Host: httpbin.org
> User-Agent: curl/7.43.0
> Accept: */*
> Content-Length: 13
> Content-Type: application/x-www-form-urlencoded
>
* upload completely sent off: 13 out of 13 bytes
< HTTP/1.1 200 OK
< Server: nginx
< Date: Sun, 18 Sep 2016 01:25:03 GMT
< Content-Type: application/json
< Content-Length: 363
< Connection: keep-alive
< Access-Control-Allow-Origin: *
< Access-Control-Allow-Credentials: true
<
{
  "args": {},
  "data": "",
  "files": {},
  "form": {
    "name": "tomshine"
  },
  "headers": {
    "Accept": "*/*",
    "Content-Length": "13",
    "Content-Type": "application/x-www-form-urlencoded",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.43.0"
  },
  "json": null,
  "origin": "121.35.209.62",
  "url": "http://httpbin.org/post"
}
* Connection #0 to host httpbin.org left intact
```

### 设置头信息

使用 `--header` 设置头信息，`httpbin.org/headers` 会显示请求的头信息，我们测试下：

``` sh
curl httpbin.org/headers --header "a:1"
```

返回：

``` html
{
  "headers": {
    "A": "1",
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.43.0"
  }
}
```

同样的，可以使用 `--header` 设置 `User-Agent` 等。

### Referer 字段

设置 `Referer` 字段很简单，使用 `--referer` ，例如：

``` sh
curl httpbin.org/headers --referer http://tomshine.xyz
```

返回：

``` html
{
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "Referer": "http://tomshine.xyz",
    "User-Agent": "curl/7.43.0"
  }
}
```

### 包含 cookie

使用 `--cookie` 来设置请求的 cookie，例如：

``` sh
curl httpbin.org/headers --cookie "name=tomshine;website=http://tomshine.xyz"
```

返回：

``` html
{
  "headers": {
    "Accept": "*/*",
    "Cookie": "name=tomshine;website=http://tomshine.xyz",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.43.0"
  }
}
```

### 自动跳转

使用 `--location` 参数会跟随链接的跳转，例如：

``` sh
curl httpbin.org/redirect/1 --location
```

httpbin.org/redirect/1 会 302 跳转，所以返回：

``` html
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.43.0"
  },
  "origin": "121.35.209.62",
  "url": "http://httpbin.org/get"
}
```

### http 认证

当页面需要认证时，可以使用 `--user` ，例如：

``` sh
curl httpbin.org/basic-auth/tomshine/123456 --user tomshine:123456
```

返回：

``` html
{
  "authenticated": true,
  "user": "tomshine"
}
```


# screen

现在很多时候我们的开发环境都已经部署到云端了，直接通过 SSH 来登录到云端服务器进行开发测试以及运行各种命令，一旦网络中断，通过 SSH 运行的命令也会退出，这个发让人发疯的。

好在有 screen 命令，它可以解决这些问题。我使用 screen 命令已经有三年多的时间了，感觉还不错。

## screen 使用

### 新建一个 Screen Session

```
$ screen -S screen_session_name
```

### 将当前 Screen Session 放到后台

```
$ CTRL + A + D
```

### 唤起一个 Screen Session

```
$ screen -r screen_session_name
```

### 分享一个 Screen Session

```
$ screen -x screen_session_name
```

通常你想和别人分享你在终端里的操作时可以用此命令。

### 终止一个 Screen Session

```
$ exit
$ CTRL + D
```

### 查看一个 screen 里的输出

当你进入一个 screen 时你只能看到一屏内容，如果想看之前的内容可以如下：

```
$ Ctrl + a ESC
```

以上意思是进入 Copy mode，拷贝模式，然后你就可以像操作 VIM 一样查看 screen session 里的内容了。

可以 Page Up 也可以 Page Down。

## 开启 screen 状态栏

```
#curl -o screen.sh https://raw.githubusercontent.com/BillWang139967/op_practice_code/master/Linux/tools/screen.sh
#sh screen.sh
```

# tcpdump


## tcp 三次握手和四次挥手

### 三次握手

**A主动打开连接，B被动打开连接**

(1) 第一次握手：建立连接时，客户端A发送SYN包(SYN=x)到服务器B，并进入SYN_SEND状态，等待服务器B确认。

(2) 第二次握手：服务器B收到SYN包，必须确认客户A的SYN(ACK=x+1)，同时自己也发送一个SYN包(SYN=y)，即SYN+ACK包，此时服务器B进入SYN_RECV状态。

(3) 第三次握手：客户端A收到服务器B的SYN＋ACK包，向服务器B发送确认包ACK(ACK=y+1)，此包发送完毕，客户端A和服务器B进入ESTABLISHED状态，完成三次握手。
完成三次握手，客户端与服务器开始传送数据。

**为什么A还要发送一次确认呢？**

主要是为了防止已失效的连接请求报文段突然有传送到B，因而产生错误。

***正常情况***

A发出连接请求，但是因为连接请求报文丢失为未收到确认。于是A在重传一次连接请求，后来收到了确认，建立了连接。数据传输完毕后，就释放了连接。A共发送两个连接请求报文段，其中第一个丢失第二个到达了B。

***异常情况***
A发出的第一个连接请求报文段并没有丢失，而是在某些网络节点长时间滞留，导致延误到连接释放之后才到达了B，本来这是一个早已经失效的报文段，但是B收到此失效的连接请求报文段之后，误以为是A又发出一次新的连接请求，于是就向A发送确认报段，同意建立连接。假如不采用三次握手，那么只要B发出确认，新的连接就建立了。由于现在A并没有发出建立连接的请求，因此不会理睬B的确认，也不会向B发送数据，但B却以为新的运输连接已经建立了，并且一直等待A发来数据。B的资源就这样白白的浪费了，
采用三次握手的办法可以防止上述现象的发生。例如刚才的情况，A不会向B的确认发出确认。B由于接收不到确认，就知道A并没有要求建立连接。

使用tcpdump来验证TCP的三次握手

使用ssh localhost来连接主机，使用使用tcpdump来验证TCP的三次握手

    
    [root@localhost apue]# tcpdump -i lo tcp -S                                         
    tcpdump: verbose output suppressed, use -v or -vv for full protocol decode          
    listening on lo, link-type EN10MB (Ethernet), capture size 65535 bytes              
    1 15:08:03.039511 IP6 localhost.44910 > localhost.ssh: Flags [S], seq 3120401438, win 32752, options [mss 16376,sackOK,TS val 1319756 ecr 0,nop,wscale 7], length 0                                                                            
    2 15:08:03.039546 IP6 localhost.ssh > localhost.44910: Flags [S.], seq 404185237, ack 3120401439, win 32728, options [mss 16376,sackOK,TS val 1319756 ecr 1319756,nop,wscale 7], length 0                                                               
    3 15:08:03.039576 IP6 localhost.44910 > localhost.ssh: Flags [.], ack 404185238, win 256, options [nop,nop,TS val 1319756 ecr 1319756], length 0                                                                                                                              
    4 15:08:03.064809 IP6 localhost.ssh > localhost.44910: Flags [P.], seq 404185238:404185259, ack 3120401439, win 256, options [nop,nop,TS val 1319781 ecr 1319756], length 21                                                                                                  
    15:08:03.064944 IP6 localhost.44910 > localhost.ssh: Flags [.], ack 404185259, win 256, options [nop,nop,TS val 1319781 ecr 1319781], length 0


第一行就是第一次握手，客户端向服务器发送SYN标志(Flags [S])，其中seq = 3120401438；
第二行就是第二次握手，服务器向客户端进行SYN+ACK响应(Flags [S.]),其中seq 404185237, ack 3120401439(是客户端的seq+1的值)
第三行就是第三次握手，客户端向服务器进行ACK响应(Flags [.]),其中ack 404185238(就是服务器的seq+1的值)。

### 四次挥手
通信传输结束后，通信的双方都可以释放连接，现在A和B都处于ESTABLISHED状态。

由于TCP连接是全双工的，因此每个方向都必须单独进行关闭。这个原则是当一方完成它的数据发送任务后就能发送一个FIN来终止这个方向的连接。收到一个 FIN只意味着这一方向上没有数据流动，一个TCP连接在收到一个FIN后仍能发送数据。首先进行关闭的一方将执行主动关闭，而另一方执行被动关闭。

(1)客户端A发送一个FIN包，用来关闭客户A到服务器B的数据传送。序列号seq = u，它等于前面已传送过的数据的最后一个字节的序号加1.这时A进入FIN-WAIT-1(终止等待1)状态，等待B的确认。

(2)服务器B收到这个FIN，它发回一个ACK，确认序号是ack = u +1。和SYN一样，一个FIN将占用一个序号。这个报文段自己的序号是v，等于B前面已经传送过的数据的最后一个字节的序号加1。然后B进程进入CLOSE-WAIT(关闭等待)状态。TCP服务器进程这时应通知高层应用进程，因而从A到B的这个方向的连接就释放了，这时的TCP连接处于半关闭(half-close)状态， 即A已经没有数据要发送了，但是B若发送数据，A仍要接收，也就是说从B到A这个方向的连接并没有关闭，这个状态可能会持续一些时间。A收到来到B的确认后就进入FIN-WAIT-2(终止等待2)状态,等待B发出的连接释放报文段。

(3)若B已经没有要向A发送的数据，其应用进程就会通知TCP释放连接，这时B发出的连接释放报文段必须使FIN = 1。现假定B的序号为w(在半关闭状态B可能要发送一些数据)。B还必须重复上次发送过的确认号ack = u +１。这时Ｂ就进入了LAST-ACK(最后确认)状态，等待A的确认。

(4)A在收到B的连接释放报文段后，必须对此发出确认。在确认报文段中把ACK置1，确认号ack = ｗ + 1，而自己的序号是seq = u + 1(根据TCP标准，前面发送过的FIN报文段要消耗一个序号)，然后进入到TIME-WAIT(时间等待)状态。

**此时的TCP还没有完全的释放掉。必须经过时间等待计时器(TIME-WAIT timer)设置的时间2MSL后，A才进入到CLOSED状态。**

> MSL叫做最长报文段寿命，它是任何报文段被丢弃前在网络内的最长时间。

2MSL也就是这个时间的两倍，RFC建议设置为2分钟，但是2分钟可能太长了，因此TCP允许不同的实现使用更小的MSL值。

因此从A进入到TIME-WAIT状态后，要经过4分钟才能进入CLOSED状态，此案开始建立下一个新的连接。当A撤销相应的传输控制块TCP后，就结束了TCP连接。

使用tcpdump来验证TCP的四次挥手

退出ssh连接的主机，使用使用tcpdump来验证TCP的四次挥手

    
    15:14:58.836149 IP6 localhost.44911 > localhost.ssh: Flags [P.], seq 1823848744:1823848808, ack 3857143125, win 305, options [nop,nop,TS val 1735551 ecr 1735551], length 64
    15:14:58.836201 IP6 localhost.44911 > localhost.ssh: Flags [F.], seq 1823848808, ack 3857143125, win 305, options [nop,nop,TS val 1735551 ecr 1735551], length 0
    15:14:58.837850 IP6 localhost.ssh > localhost.44911: Flags [.], ack 1823848809, win 318, options [nop,nop,TS val 1735554 ecr 1735551], length 0
    15:14:58.842130 IP6 localhost.ssh > localhost.44911: Flags [F.], seq 3857143125, ack 1823848809, win 318, options [nop,nop,TS val 1735559 ecr 1735551], length 0
    15:14:58.842150 IP6 localhost.44911 > localhost.ssh: Flags [.], ack 3857143126, win 305, options [nop,nop,TS val 1735559 ecr 1735559], length 0

**seq start:end意思是初始序列号：结束序列号，end = start + length, 但是接受包的结束序号应该是end - 1。**
比如start = 1，length = 3，那么真正的结束序号是1+3-1 = 3,因为开始序号也算在内的！

seq 1823848744:1823848808意思是初始序列号：结束序列号，其实后面那个就是前面那个加上包长度length = 64，实际上结束序列号是没有使用的，真正使用的序号是开始序号到结束序号-1，也就是1823848807

第一次挥手中客户端发送FIN即[F.] seq u = 1823848808，也就是上次发送的数据的最后一个字节的序号加1

第二次挥手中服务器发送ACK即[.] ack 1823848809 = u + 1

第三次挥手中服务器发送FIN即[F.] seq v = 3857143125， ack 1823848809 = u + 1

第四次挥手中客户端发送ACK即[.] ack 3857143126 = v + 1


1.默认情况下(不改变socket选项)，当你调用close函数时，如果发送缓冲中还有数据，TCP会继续把数据发送完。

2.发送了**FIN只是表示这端不能继续发送数据(应用层不能再调用send发送)**，但是还可以接收数据。

3.应用层如何知道对方关闭？

在最简单的阻塞模型中，当调用recv时，如果返回0，则表示对方关闭，

在这个时候通常的做法就是也调用close，那么TCP层就发送FIN，继续完成四次握手；

**如果不调用close，那么对方就会处于FIN_WAIT_2状态，而本端则会处于CLOSE_WAIT状态；**

4.在很多时候，TCP连接的断开都会由TCP层自动进行，例如你CTRL+C终止你的程序，TCP连接依然会正常关闭。

## tcpdump 使用

### 针对特定网口抓包(-i选项)

> tcpdump -i eth0

### 指定抓包端口

> tcpdump -i eth0 port 22

### 抓取特定目标ip和端口的包

> tcpdump -i eth0 dst 10.70.121.92 and port 22

### 增加抓包时间戳(-tttt选项)

> tcpdump -n -tttt -i eth0
