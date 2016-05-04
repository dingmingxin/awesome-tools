工具说
======

工欲善其事，必先利其器

人和动物的最大区别就是，人能使用、创造工具 程序员的能力高低，也能通过其创造、利用工具的能力来评判

这些我个人在平时的工作中用到的一些工具，它们让我的工作 更加高效。下面我讲一一介绍:

注，本文介绍的武器基本都属于命令行下的应用程序

配置文件
========

本文介绍的工具，配置文件请参考:[dmxdotfiles-v0.1.0](https://github.com/dingmingxin/dotfiles/releases/tag/v0.1.0)

七种武器
========

zsh
---

### 简介

1.  家族: \*nix
2.  出生: 1990s
3.  wikipedia: <https://en.wikipedia.org/wiki/Z_shell>

### zsh vs bash : 特点及优势

bash是大多数linux发行版的默认shell环境，是最通用、最流行的shell

大多数用过bash的同学肯定有同感，bash的自动提示功能太弱了，即使有了bash-completion, 补全功能也很有限，下面我总结了一下zsh优于bash的一些特点:

1.  强大的补全功能
    1.  cd补全
    2.  命令选项补全
    3.  path completion and expansion
    4.  git completion
    5.  其他各种好用的补全提示
2.  错误检查自动更正
3.  命令行右提示
4.  自定义命令
    1.  normal alias like bash
    2.  global alias
    3.  前缀替换
5.  可编程式文件批量重命名 : zmv
6.  zsh-history-substring-search
7.  功能强大的开源库：[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

### 具体特点详述

zsh特性繁多，在此我只简单介绍一两个我熟悉并且经常使用的特性
#### 自动补全
##### cd 自动补全
###### 路径缩写补全

cd /d/w/t/0 -\> cd /data/work/test/01

###### 路径替换

1.  cd /usr/local/bin && cd bin share -\> cd /usr/local/bin && cd ../share
2.  cd *data/www/site1/apps/common/logic/test && cd site1 site2 相当于 cd *data/www/site1/apps/common/logic/test && cd ..*..*../../site2/apps/common/logic/test

##### 命令选项补全

examples: ls -s \<TAB\> --TODO pic here

#### zsh-history-substring-search

相比bash中的Ctrl-R，这个插件很好用

启用: 在\~/.zshrc中添加: plugins=(history-substring-searc h) --TODO pic here

##### 结合fzf更好用

#### 提示主题

zsh自身对终端提示有很好的支持接口，并且自带了对版本控制工具的信息接口 比如可以获取当前git 库的分支、当前分支是否是clean，都可以获得 --TODO pic here

### oh-my-zsh

zsh在开源社区，有个很著名的仓库: [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

#### Install

sh -c "\$(curl -fsSL <https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh>)" 或者： sh -c "\$(wget <https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh> -O -)"

#### 简介

oh-my-zsh 安装完成后，会有\~/.zshrc \~/.oh-my-zsh 所有的插件、命令alias、主题等都在 \~/.oh-my-zsh

\~/.oh-my-zsh :

1.  /custom : 用于用户自定义的内容
2.  /plugin : oh-my-zsh 自带的插件
3.  /themes : 主题

主题就是shell 的prompt 提示，zsh比其他shell多出来一个右提示， 提示的可定制性也很强

主题、使用哪些插件、自定义插件，都可以在 oh-my-zsh 安装完之后带的\~/.zshrc 里进行配置

### 我的zsh配置

有现成的轮子，就不必费劲自己再去创造，暂且用拿来主义来伪装自己吧。 我自己维护了一份基于zsh的配置 dotfiles:

#### 安装

1.  download release file: dmxdotfiles.tar.gz
2.  untar
3.  cp -r dmxdotfiles \~/dotfiles && cd \~/dotfiles && ./deploy zsh

#### 配置文件介绍

##### \~/.zsh<sub>alias</sub>.zsh

全局的alias

##### \~/.zsh<sub>custom</sub>

存放一些自定义的配置，和zsh自定义的插件

##### \~/.zsh<sub>env</sub>.zsh

环境变量在这个目录

##### \~/.zshrc

zsh的配置文件

##### \~/.zprofile

#### 文件引用顺序

在我的配置下，zsh启动时依次会source:

1.  \~/.zprofile
2.  \~/.zshrc

我在\~/.zshrc里手动source了\~/.zsh<sub>env</sub>.zsh 和 \~/.zsh<sub>custom</sub> 下的一些文件

注意，除了\~/.zshrc \~/.zprofile, 其他的都是我自定义的，非zsh标准文件

tmux
----

终端会话管理工具

你还在为开了好多终端窗口记不住那条命令在哪里运行着吗？ 你还在为终端窗口的管理而烦恼吗？

有了tmux，你再也不用发愁了，它不会很复杂，一个server, 一个client, 一个配置文件而已

具体使用请参考man tmux

### 示例图

--TODO pic here

### tmuxinator

[github:tmuxinator](https://github.com/tmuxinator/tmuxinator) : Manage complex tmux sessions easily 从配置文件中读取tmux configuration,然后启动一个会话

#### Install

由于国内网络原因, rubygems.org 访问很慢，甚至访问不了. 还好国内有个镜像网站 ruby.taobao.org

##### 首先设置gem sources list

gem sources --remove <https://rubygems.org/> --add <https://ruby.taobao.org/>

##### 安装

gem install tmuxinator

#### Usage

tmuxinator有个alias: mux 配置文件在 \~/.tmuxinator

假如有个配置文件在\~/.tmuxinator/dotfiles.yml mux start dotfiles 就会启动这个会话, 会话的窗口、pane，以及每个窗口创建 时的执行命令以及布局，都可以在dotfiles.yml 中配置 这样就省去了手动去创建每个窗口了

##### 配置文件示例

``` {.yaml}
  # ~/.tmuxinator/dotfiles.yml
  name: dotfiles
  root: ~/dotfiles/

  windows:
    - vim:
        layout: even-vertical
        panes:
          -
          -
    - bash:
        layout: even-vertical
        panes:
          -
          -
    - tmux:
        layout: even-vertical
        panes:
          -
          -
```

详解： session name :dotfiles session 默认路径 \~/dotfiles session 启动时启动三个窗口，窗口名分别为：vim, bash, tmux 每个窗口开两个面板，布局都是竖向均分布局

the<sub>silversearcher</sub>(ag)
--------------------------------

github: [the<sub>silversearcher</sub>](https://github.com/ggreer/the_silver_searcher) 比ack快的终端文件内容搜索工具 当你打开终端，面对一个很大很复杂的工程，想去找一个函数的定义或者调用，ag就能帮上忙

### ag vs ack

A code searching tool similar to ack, with a focus on speed.

### Help

ag --help

### Usage

ag [FILE-TYPE] [OPTIONS] PATTERN [PATH] FILE-TYPE 如果忽略，ag会搜索它支持的所有文件类型(按后缀名) PATH可以是dir,也可以是filename, 如果忽略，就会搜索当前路径下的所有支持的文件

#### 查看支持的文件类型

ag --list-file-types

#### Examples

##### 搜索所有lua脚本

###### 方式1：

ag --lua search<sub>pattern</sub>

###### 方式2:

ag -G .lua search<sub>pattern</sub> -G 选项是搜索文件名匹配某些pattern的文件的 此处.lua，是匹配文件名中包含.lua 的所有文件

##### 搜索版本控制系统忽略的文件

ag 搜索时，默认忽略了 .gitignore .hgignore .svnignore等版本控制系统所指定 的忽略的文件，如果想搜索那里面的内容,需要用到 -U选项 ag -U some<sub>pattern</sub>

##### 使用正则搜索

ag正则搜索使用的是[PCRE's JIT compiler](http://sljit.sourceforge.net/pcre.html), 兼容perl 的正则表达式 正则的使用内容很多，要展开讲的话需要单独的篇幅，这里只举一两个简单的例子

###### 搜索单词

ag "\\bword\\b" --搜索单词

###### 正则分组匹配

ag "(\\bkey<sub>word</sub>\\b):\\1:\\1" --支持分组搜索 这个搜索是，搜索 keyword:keyword:keyword 这种的

ctags
-----

site: [Exuberant Ctags](http://ctags.sourceforge.net/)

基于正则表达式的文本tag生成器。 不光可以过滤代码文件，普通的有格式的纯文本都可以用。

### tag文件的作用

一般用于编辑器的代码跳转和查找 比如vim 和emacs

### tag文件格式

ctags生成的tag格式: {tagname}\<Tab\>{tagfile}\<Tab\>{tagaddress}

#### example

AddTeamExp /data/script/AddTeamExp.lua *<sup>newClass</sup>('AddTeamExp', BaseNode)\$*;"

#### vim 支持的tag文件格式

vim支持的必须是下面三三种的一种

1.  {tagname} {TAB} {tagfile} {TAB} {tagaddress}
2.  {tagfile}:{tagname} {TAB} {tagfile} {TAB} {tagaddress}
3.  {tagname} {TAB} {tagfile} {TAB} {tagaddress} {term} {field} ..

### 版本

ctags，我们目前所指的是它的一个多语言实现 Exuberant Ctags，原生支持多达41中编程语言 ctags还可以通过配置文件，增加语言扩展，定制自己的语言类型过滤器

### 简单使用

ctags -R . 对当前的路径的文件生成tags

### 定制自己的类型过滤器

``` {.shell}
  ctags -R . \
          -f ./tags\
          --tag-relative=yes \
          --langdef=MYLUA \
          --langmap=MYLUA:.lua \
          --regex-MYLUA="/newClass\(\'([^ ]+)\',.*/\1/c/" \
          --regex-MYLUA="/.*subclass\([\'\"]([^ ]+)[\'\"]\)/\1/c/" \
          --regex-MYLUA="/[ ]?([a-zA-Z_]+)Layout[ ]?=.*/\1/c/" \
          --regex-MYLUA="/[ ]?([a-zA-Z_]+Layout)[ ]?=.*/\1/c/" \
          --regex-MYLUA="/^([^:.= ]+)[ =]+\{\}/\1/c/" \
          --regex-MYLUA="/^function[ ]+[^:]+:([^ \(]+)/\1/f/" \
          --regex-MYLUA="/^function[ ]+([^:. ]+)\(/\1/f/" \
          --regex-MYLUA="/^function[ ]+[^:]+\.([a-zA-Z_]+)\(/\1/f/" \
          --regex-MYLUA="/^function[ ]+[^:.]+\.class:([a-zA-Z_]+)\(/\1/f/" \
          --regex-MYLUA="/[ ]?local[ ]+function[ ]+([^:.= ]+)\(/\1/f/" \
          --regex-MYLUA="/[ ]?local[ ]+([a-zA-Z_]+)[ ]?=[ ]?function\(/\1/f/" \
          --regex-MYLUA="/([^ ]+)[ ]+=[a-zA-z_ ]+or[ ]+{}/\1/m/" \
          --regex-MYLUA="/.*:mapEvent\(([^,:]+)[, ]+[^ ,:_]+\).*/\1/e/" \
          --regex-MYLUA="/([ ]?[a-zA-Z_-]+)[ ]?=[ ]?InitStaticInt.*/\1/e/"

    # 简单解释
    # c : newClass; subclass
    # c : 匹配 A={} 类似这种的类定义
    # m : 匹配新的Model --> 类似于这种：PveModel = PveModel or {}
    # e : 匹配event和command-->目前只针对于旧代码，evt和command对应的那些
    # f :
    # function A:b(..);        --regex-MYLUA="/^function[ ]+[^:]+:([^ \(]+)/\1/f/" \
    # function aaa(..);        --regex-MYLUA="/^function[ ]+([^:. ]+)\(/\1/f/" \
    # function A.bb(...);      --regex-MYLUA="/^function[ ]+[^:]+\.([a-zA-Z_]+)\(/\1/f/" \
    # function A.class:b(..);  --regex-MYLUA="/^function[ ]+[^:.]+\.class:([a-zA-Z_]+)\(/\1/f/" \
    # local function aa(...);  --regex-MYLUA="/[ ]?local[ ]+function[ ]+([^:.= ]+)\(/\1/f/"
    # local aa = function(..); --regex-MYLUA="/[ ]?local[ ]+([a-zA-Z_]+)[ ]?=[ ]?function\(/\1/f/"
```

### 配合vim

在\~/.vimrc中加入 set tags+=./tags 这样vim就可以用当前路径下的tag文件来定位和跳转了 具体跳转方式，在vim中查看文档 :h tags

### 配合emacs

生成emacs能是别的tag文件，需要用到-E 选项

``` {.bash}
  ctags -R -E .
```

Editors
-------

### 编辑器之神 - Vim

VIM is "Vi IMproved" 介绍vim之前，先介绍下vi

#### vi

vi是一款由加州大学伯克利分校，Bill Joy 研究开发的文本编辑器

如果再往前追根溯源，能从vi的操作中看出流编辑器ed的身影

vi是一款模式编辑器，有一下三种模式:

1.  Command mode
2.  Visual mode
3.  Insert mode

#### vim

vim 是vi的衍生版本，在vi的基础上改进和增加了很多特性 vi的衍生版本有很多，但是vim是这些版本中易用性最好，可扩展度高，用户基础最大的 一个版本

##### 介绍

Link-org: [vim.org](http://www.vim.org) Link-wikipedia: [Vim(text editor)](https://en.wikipedia.org/wiki/Vim_(text_editor))

##### 如何学习

学习vim最便捷、最高效的方式，就是在阅读vim的文档 在vim输入:help或者:h 查看帮助

##### 模式

vim是模式编辑器，有以下几种不同的模式

###### Normal mode

打开之后就处于正常模式 用于浏览和修改文本(插入除外)，主要是删除、粘贴等

###### Insert mode

插入模式 这个模式用于正常的写入字符。 在这个模式下，vim的行为和普通的文本编辑器没有太大区别

###### Visual mode

可视模式 也可以理解为选中模式，相当于选中的高亮的文本处于正常模式下

####### 行选中

V

####### 自由选中

v -\> h j k l....

####### 块选中

Ctrl-v

###### Command-Line mode

按: 进入，一般用于高级的用于操作文件的，比如打开、关闭... 还可以用于高级的编辑 还可以用于设置编辑的选项等等

###### 模式间的转换

####### Normal-\>Insert

在normal模式下按下这些键可以进入insert模式 下面是这些按下这些键，进入insert模式之后光标的位置说明

-   i 光标前
-   I 行首
-   a 光标后
-   A 在行末尾
-   o 在当前行下面新建行进入插入状态
-   O 在当前行之上新建行进入插入状态
-   s 删除光标下的字符进入插入状态
-   S 删除所在行

####### Normal-\>Visual

v V C-v

####### Normal-\>Command-Line

:

####### Visual-\>Command-Line

:

####### Other-mode -\> Normal

ESC

##### 编辑

大部分的编辑技巧在于normal状态，Insert状态下 做好提示的配置就可以了 这里只做简单介绍，具体可参考vim的帮助文件

###### 移动

:h usr<sub>03</sub>.txt Normal 模式下的光标移动

####### - h j k l: 光标往左、下、上、右移动

####### w b e ge

w 移动到下一个单词的开头 b 上一个单词的开头 e 移动到下一个单词的末尾 ge 移动到上一个单词的末尾

####### W B E gE

跟w/b/e/ge 的移动方向相同 只不过这里的移动单位不一样，W/B/E/gE将不包含空格的 一串字符认为是一个移动单位 举例：1bcd;abcd;abc9 光标在9的位置时按下B就会跳转到1位置，中间略过了分号

####### t T f F

####### 0 \^ \$

####### % parenthesis

配对的括号间相互移动

###### 修改 - Making some changes

:h usr<sub>04</sub>.txt

####### oprators

一般大小写之间区别就是：作用范围大小，作用区域相反(一个向前一个向后...)

######## d D

-   dd 删除一行
-   diw 删除一个单词，不包括单词靠着的空格、括号等
-   D 删除光标到行尾的字符

######## c C

-   ciw 删除一个单词并进入插入状态
-   C 删除光标到行尾的字符

######## s S

-   s 删除光标所在字符并进入插入状态
-   S 删除光标所在行并进入插入状态

######## x X

-   x 删除光标下的字符
-   X 删除光标前的字符

######## copy and paste

v p ; V p

####### 文本对象

:h objects

####### 命令计数

4w 光标向后移动四个单词的位置 d2w 删除2单词

##### 搜索及替换

这部分涉及到正则表达式的内容

###### Search

Normal 模式下 按 / 就可以Search :h pattern

###### Replace

全局替换 :%s/origin/new/options 选中之后替换 :'\<,'\>s/origin/new/options

##### 高阶使用

:g vimcast

###### 配合*ctags*

##### 配置部署

cd \~/dotfiles && ./deploy vim

##### 编辑器定制及扩展

files: \~/.vimrc \~/.vim

###### setting

:h vimrc \~/.vimrc

###### Plugin

####### Plugins System

-   default
-   Pathogen <https://github.com/tpope/vim-pathogen> <http://www.vim.org/account/profile.php?user_id=9012>
-   Vundle <https://github.com/VundleVim/Vundle.vim>
-   NeoBundle

个人推荐使用Vundle,具体可参见我的dotfiles/config<sub>vim</sub>/vimrc文件

####### Writting Plugins

:h usr<sub>41</sub>.txt

#### 关于正则表达式

使用vim一定要了解正则表达式，这样会让自己的编辑更有效率 :h pattern

### 神之编辑器 - Emacs

我个人刚刚接触Emacs编辑器不到半年，所以此处只简单介绍下 我了解的Emacs的特点

#### 学习Emacs的初衷

Emacs 有个模式，org-mode，结构性很强，我发现用它记笔记很方便 于是我就踏上了学习Emacs的不归路

Emacs的学习曲线很陡，而且它的理念跟我用了3\~4年的vim截然不同， 因为是无模式的编辑器，要实现某个操作必须按着Ctrl Alt 组合键才能做到，这让我 很不适应，所以，刚接触Emacs，我的内心其实是拒绝的，但是为了org-mode，我艰难 的存活了下来，并且在这过程中学了点emacs-lisp的编程经验

#### Ctrl到死的编辑器

Emacs的快捷键很复杂，大多数需要Ctrl Alt Shift 的组合 所以我给它起了个名字，叫Ctrl到死的编辑器

#### Evil-mode

Emacs下模拟vim操作的包有很多，Evil-mode是目前最流行，我个人认为功能比较 全面的Emacs vim插件。

基于Evil-mode，开源社区衍生出了好多插件，比如evil-leader......

Evil-mode 支持vim的模式编辑、查找替换、快捷键映射等等初级、中级的功能

### 神神编辑器 - spacemacs(emacs+evil-mode and more)

刚在Emacs中存活下来，我就急不可耐的去找有没有在Emacs中模拟vim 操作的插件，果不其然，已经有人做了这个大轮子:Evil-mode 在使用spacemacs这套配置之前，我一直是用evil-mode，然后其他功能 依然用Emacs的快捷键，Ctrl到死的操作

如果没有Evil-mode，我学习使用Emacs没有那么快 它是我在Emacs中存活的关键

#### 与spacemacs邂逅

在我的Emacs配置稳定下来之后，我开始逐渐了解Emacs，为了配置Emacs 我专门花时间学了下common lisp，声明不止，折腾不息。

在github上浏览Emacs相关的内容，高级搜索，按照star从高到低排序这么看， 很快我就发现了spacemacs 这个git仓库

#### spacemacs

1.  [spacemacs github](https://github.com/syl20bnr/spacemacs)
2.  [spacemacs documents](https://github.com/syl20bnr/spacemacs/tree/master/doc)

#### spacemacs原理

引用一句名言：

计算机科学领域的任何问题都可以通过增加一个间接的中间层来解决 Any problem in computer science can be solved by another layer of indirection

spacemacs中很多配置是通过layer来实现的，每层layer约定自己的如下文件：

1.  packages.el --约定layer引用了emacs哪些package(相当于vim中的plugin)
2.  config.el --顾名思义，选项配置文件
3.  funcs.el --自定义函数
4.  keybindings.el --快捷键绑定
5.  README.org --该layer的说明

而使用spacemacs这套配置只需要指定自己使用那些layer就可以了。 当然也能够自己创建layer

分层的结果是，配置起来更加规范，如果想禁用或者开启某些功能不用在 很多配置文件中查找了。还有就是spacemacs对emacs启动速度做了优化，增加了 缓存和延迟加载，比如启动的时候并不是加载所有layer，而是按照需求来加载相关 的layer，尤其是在Emacs daemon模式下，启动速度更快

#### spacemacs使用简单介绍

spacemacs中有一个key sequences的概念，利用它，我们就可以像 访问应用程序的菜单一样，一级一级的拿到自己想要的功能

比如，在应用里，通常有File-\>OpenRecentFiles 这个菜单 那么在spacemacs中就有这样的快捷键:\<space\>fr,依次按下 空格、f、r，spacemacs就会在底部打开一个helm buffer,里面是 最近打开的文件。而\<space\>ff 则代表要打开文件，会让你输入 文件的路径。

通过上面简单的两个例子，spacemacs的使用跟用鼠标点击菜单栏 的功能是很类似的:

\<space\> --1.告诉emacs我要使用菜单了 f --2.告诉emacs我要使用一级菜单下的Files 菜单项 r --3.告诉emacs我要使用Files-\>OpenRecentFiles菜单项，请给我一份最近打开的文件列表

虽然和鼠标操作原理很类似，但是比鼠标操作高效很多很多，而且这些key sequences都是有意义的 很容易记住

当然，这些快捷键菜单是自己可以配置的，具体配置请翻阅spacemace的官方文档

##### examples

\<space\>sj --jump in buffer \<space\>pf --search file in project for open

#### spacemacs gifs and videos

##### gifs

##### videos

fzf
---

github 地址: [fzf-github](https://github.com/junegunn/fzf) 这是一个go语言写的工具，用于命令行的fuzzy finder 他的输入是一个数组，输出是用户的选择项。

Alfred.app
----------

很多的workflow，和电脑更好、更快捷的交互

总结
====
