# shell脚本笔记

Shell 是一个命令行解释器，它为用户提供了一个向 Linux 内核发送请求以便运行程序的界面系统级程序，用户可以用 Shell 来启动、挂起、停止甚至是编写一些程序。

```
硬件 > 内核 > Shell命令解释器 > 外层应用程序
```

Shell 还是一个功能相当强大的编程语言，易编写、易调试、灵活性强。Shell是解释执行的脚本语言，在 Shell 中可以调用 Linux 系统命令。

在线工具：https://www.runoob.com/try/runcode.php?filename=helloworld&type=bash



## 基础



### 什么是 shell

**shell 解释**：引用别人的话说：“Shell 是一个用 C 语言编写的程序，它是用户使用 Linux 的桥梁。Shell 既是一种命令语言，又是一种程序设计语言。”

简而言之，shell 是命令解释器之外的一种编程语言。

**shell 可以做什么**：批处理、自动化管理、监控管理、日志数据处理、自动数据备份等等。



### Shell 的种类

Shell 编程跟 JavaScript、php 编程一样，只要有一个能编写代码的文本编辑器和一个能解释执行的脚本解释器就可以了。

Linux 的 Shell 脚本解释器种类众多，一个系统可以存在多个 shell  脚本解释器，可以通过 `cat /etc/shells` 命令查看系统中安装的 shell 脚本解释器。

```
cat /etc/shells

/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

bash 由于易用和免费，在日常工作中被广泛使用。同时，Bash 也是大多数 Linux 系统默认的 Shell 脚本解释器。

下面的命令可以查看当前运行的 Shell：

```
echo $SHELL
```

切换 **bash** 和 **zsh**

```
chsh -s /bin/bash
chsh -s /bin/zsh
```

执行切换命令后，要重新打开终端才能生效。



### shell 脚本组成部分

- 1）注释：注释等说明信息，要以#开头

- 2）命令：shell 基本语法

- 3）变量：shell 支持字符串变量和整数变量。

- 4）结构控制语句：流程控制语句

脚本的第一行调用时表明基于 bash 的方式执行（如果系统默认是 bash 执行，不写也行）：

```
#!/bin/bash
# 我是注释 ：-e特殊字符（\a、\n）转义
echo -e "Hello World!\a\n" 
exit 0
```

退出时最好写上：`exit 0`



### 运行脚本的方法

**1、作为可执行程序**

输入脚本的绝对路径或相对路径执行。

```
chmod u+x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本
```



**2、作为解释器参数**

这种运行方式是，直接运行解释器，其参数就是 shell 脚本的文件名，如：

```
/bin/sh helloworld.sh
sh helloworld.sh
```



**在当前环境下执行命令**

source 命令(从 C Shell 而来)是 bash shell 的内置命令。点命令，就是个点符号，(从Bourne Shell而来)是source的另一名称。同样的，当前脚本中设置的变量也将作为脚本的环境，source(或点)命令通常用于重新执行刚修改的初始化文件，如 .bash_profile 和 .profile 等等。

source命令是shell的一个内部命令，它从指定的shell 文件中读入所有命令语句并在当前进程中执行。





### 变量

运行 shell 时，会同时存在三种变量：

- **1) 局部变量** 局部变量在脚本或命令中定义，仅在当前 shell 实例中有效，其他 shell 启动的程序不能访问局部变量。
- **2) 环境变量** 所有的程序，包括 shell 启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候 shell 脚本也可以定义环境变量。
- **3) shell 变量** shell 变量是由 shell 程序设置的特殊变量。shell 变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了 shell 的正常运行。



#### 定义变量

语法：

```
变量名=变量值
your_name="dandan"
```

注意，变量名和等号之间不能有空格，这可能和你熟悉的所有编程语言都不一样。同时，变量名的命名须遵循如下规则：

- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
- 中间不能有空格，可以使用下划线（_）。
- 不能使用标点符号。
- 不能使用bash里的关键字（可用help命令查看保留关键字）。



#### 使用变量

使用一个定义过的变量，只要在变量名前面加美元符号即可，如：

```
your_name="qinjx"
echo $your_name
echo ${your_name}
```

变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界，比如下面这种情况：

```
for skill in Ada Coffe Action Java; do
    echo "I am good at ${skill}Script"
done
```

如果不给skill变量加花括号，写成echo "I am good at $skillScript"，解释器就会把$skillScript当成一个变量（其值为空）。推荐给所有变量加上花括号，这是个好的编程习惯。

已定义的变量，可以被重新定义，如：

```
your_name="tom"
echo $your_name
your_name="alibaba"
echo $your_name
```

这样写是合法的，但注意，第二次赋值的时候不能写 `$your_name="alibaba"`，使用变量的时候才加美元符（$）。



#### 只读变量

使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。

```
#!/bin/bash
myUrl="https://www.google.com"
readonly myUrl
myUrl="https://www.runoob.com"
/bin/sh: NAME: This variable is read only.
```



#### 删除变量

使用 unset 命令可以删除变量。语法：

```
unset variable_name
```

unset 命令不能删除只读变量。



## 学习资源

[shell脚本基础教程](https://www.cnblogs.com/tianhei/p/8083332.html)

https://blog.csdn.net/weixin_37490221/article/details/80869792

[linux与shell基础](https://www.cnblogs.com/f-ck-need-u/p/7048359.html#blogshell)

https://www.runoob.com/linux/linux-shell-variable.html



```
#!/bin/bash
# 提交到 gerrit
#
# 使用方式：
# 在项目文件的同级目录创建 commit.sh 文件并复制此内容
# 输入命名 ../commit.sh '<commit msg>' [dev/test] 运行此脚本

commitMsg=$1                # 脚本传入的第一个参数为提交信息
branchName=${2:-"dev"}      # 脚本传入的第二个参数为需要提交到到分支，默认值为 dev，可修改为 test。 
devBranchName="dev2.0-hcf"  # 注意：需要将 dev2.0-hcf 替换为自己的分支名称）

echo "commit shell: start commit.sh ..."

if [ -n "$commitMsg" ]
then

  if [ $branchName == dev ]
  then
    # echo "commit shell: git checkout -- config/index.js"
    # git checkout -- config/index.js

    echo "commit shell: git add ."
    git add .

    echo "commit shell: git commit -m '${commitMsg}'"
    git commit -m "${commitMsg}"

    echo "commit shell: git pg $devBranchName"
    git pg $devBranchName

    echo "commit shell: 是否上传到 test 分支[1/0]: "
    read toTest

    if [ $toTest == 1 ]
    then
      echo "commit shell: git checkout test"
      git checkout test

      echo "commit shell: git pull"
      git pull

      echo -e "commit shell: \n   本次脚本执行结束，需先在 gerrit 上 review 代码，后再手动执行 git mg <dev分支名称> 合并代码"
      echo -e "commit shell: \n   若需继续提交代码到 test，请在代码合并后执行：../commit.sh '<commit msg>' test"
    fi

  elif [ $branchName == test ]
  then
    echo "commit shell: 本次合并是否存在冲突[1/0]: "
    read hasErr

    if [ $hasErr == 1 ]
    then
      echo "commit shell: git add ."
      git add .

      echo "commit shell: git commit -m '${commitMsg}'"
      git commit -m "${commitMsg}"
    fi

    echo "commit shell: git pg test"
    git pg "test"

    echo "commit shell: git checkout $devBranchName"
    git checkout $devBranchName

  else
    echo "commit shell: 分支只能是：dev/test"
  fi

else
    echo "commit shell: 请传入提交信息"
fi

echo "commit shell: 脚本执行结束"
```



## bash 参考手册

https://www.gnu.org/software/bash/manual/html_node/index.html#SEC_Contents