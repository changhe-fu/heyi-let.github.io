# Linux 常用命令

常用快捷键：

1）ctrl + c：停止进程

2）ctrl+l：清屏

3）ctrl + q：退出

4）善于用 tab 键

5）上下键：查找执行过的命令

6）ctrl +alt：linux和Windows之间切换



## man 获得帮助信息

基本语法：

```
man [命令或配置文件]
```

例子

```powershell
> man man

man(1)                                                                  man(1)

NAME
       man - format and display the on-line manual pages

SYNOPSIS
       man  [-acdfFhkKtwW]  [--path]  [-m system] [-p string] [-C config_file]
       [-M pathlist] [-P pager] [-B browser] [-H htmlpager] [-S  section_list]
       [section] name ...


DESCRIPTION
       man formats and displays the on-line manual pages.  If you specify sec-
       tion, man only looks in that section of the manual.  name  is  normally
       the  name of the manual page, which is typically the name of a command,
       function, or file.  However, if name contains  a  slash  (/)  then  man
       interprets  it  as a file specification, so that you can do man ./foo.5
       or even man /cd/foo/bar.1.gz.

       See below for a description of where man  looks  for  the  manual  page
       files.
```

显示说明：

- NAME 命令的名称和单行描述

- SYNOPSIS 怎样使用命令

- DESCRIPTION 命令功能的深入讨论

- EXAMPLES  怎样使用命令的例子

- SEE ALSO  相关主题（通常是手册页）

数字说明：

- 1.用户在shell环境中可以操作的命令或是可执行的文件

- 2.系统内核(kernel)可以调用的函数

- 3.常用的函数or函数库

- 4.设备配置文件

- 5.配置文件的格式

- 6.游戏相关

- 7.linux网络协议和文件系统

- 8.系统管理员可以用的命令

- 9.跟内核有关系的文件



##  help 获得 shell 内置命令的帮助信息

基本语法：

```
 help 命令
```

help 是内部命令的帮助，比如 cd
man 是外部命令的帮助，比如 ls



## 目录/文件类命令

pwd：显示当前工作目录的绝对路径



### ls 列出目录的内容

基本语法：

```
ls [选项] [目录或是文件]
```

选项：

-a ：全部的文件，连同隐藏档( 开头为 . 的文件) 一起列出来(常用)

-l ：长数据串列出，包含文件的属性与权限等等数据；(常用)

 每行列出的信息依次是：

1. 文件类型与权限
2. 链接数
3. 文件属主
4. 文件属组
5. 文件大小用byte来表示
6. 建立或最近修改的时间
7. 名字 

例子：

```
ls -al
```



### cd 切换目录

1）基本语法：

```shell
cd 绝对路径

cd 相对路径

cd ~ 或者 cd   # 回到自己的家目录

cd -          # 回到上一次所在目录

cd ..         # 回到当前目录的上一级目录

cd -P         # 跳转到实际物理路径，而非快捷方式路径 
```



### mkdir 创建一个新的目录

1）基本语法：

    ```
mkdir [-p] 要创建的目录
    ```

选项：

- -p：创建多层目录

```
mkdir -p user/atguigu
```



### rmdir 删除一个空的目录

1）基本语法：

```
 rmdir 要删除的空目录
```

只能删除空目录



### touch 创建空文件

创建一个空白文件，假如当前目录有同样的文件，则会更新文件的时间戳。

1）基本语法：

```
touch 文件名称
```



### rm 移除文件或目录

1）基本语法

    rm [选项] [目录或是文件]

-f 强制删除
-r 删除目录 

常用：rm -rf 文件或目录



### >> 重定向命令

1）基本语法：

（1）ls –l >文件      （功能描述：列表的内容写入文件a.txt中（覆盖写））

（2）ls –al >>文件    （功能描述：列表的内容追加到文件aa.txt的末尾）



### echo 打印文件内容或编辑文件内容

常用选项有：
-n 不换行输出
-e 可以使用转义字符（\n回车，\t tab键）

示例：
echo “I am studying linux”>>xujun.txt 追加文件尾部内容
echo $? 假如返回值为 0 的时候，表示上一次命令成功。假如是1到255的话，则是失败
echo -e “wo\tshi\tshei”> xujun.txt

### ln 软链接

1）基本语法：

```
ln –s [原文件] [目标文件]
```

功能描述：给原文件创建一个软链接，软链接存放在目标文件目录



### vi/vim 编辑文件

如果编辑的文件不存在，会创建一个。

基本上 vi/vim 共分为三种模式，分别是**命令模式（Command mode）**，**输入模式（Insert mode）**和**底线命令模式（Last line mode）**。

#### 命令模式：

用户刚刚启动 vi/vim，便进入了命令模式。

此状态下敲击键盘动作会被Vim识别为命令，而非输入字符。比如我们此时按下i，并不会输入一个字符，i被当作了一个命令。

以下是常用的几个命令：

- **i** 切换到输入模式，以输入字符。
- **x** 删除当前光标所在处的字符。
- **:** 切换到底线命令模式，以在最底一行输入命令。

若想要编辑文本：启动Vim，进入了命令模式，按下i，切换到输入模式。

命令模式只有一些最基本的命令，因此仍要依靠底线命令模式输入更多命令。

### 输入模式

在命令模式下按下i就进入了输入模式。

在输入模式中，可以使用以下按键：

- **字符按键以及Shift组合**，输入字符
- **ENTER**，回车键，换行
- **BACK SPACE**，退格键，删除光标前一个字符
- **DEL**，删除键，删除光标后一个字符
- **方向键**，在文本中移动光标
- **HOME**/**END**，移动光标到行首/行尾
- **Page Up**/**Page Down**，上/下翻页
- **Insert**，切换光标为输入/替换模式，光标将变成竖线/下划线
- **ESC**，退出输入模式，切换到命令模式

#### 底线命令模式

在命令模式下按下:（英文冒号）就进入了底线命令模式。

底线命令模式可以输入单个或多个字符的命令，可用的命令非常多。

在底线命令模式中，基本的命令有（已经省略了冒号）：

- q 退出程序
- w 保存文件

按ESC键可随时退出底线命令模式。

https://www.runoob.com/linux/linux-vim.html

### 查看文件内容

#### cat

 查看文件内容，从第一行开始显示

1）基本语法

       cat  [选项] 要查看的文件

选项：

-A ：相当于 -vET 的整合选项，可列出一些特殊字符而不是空白而已；

-b ：列出行号，仅针对非空白行做行号显示，空白行不标行号！

-E ：将结尾的断行字节 $ 显示出来；

-n ：列出行号，连同空白行也会有行号，与 -b 的选项不同；

-T ：将 [tab] 按键以 ^I 显示出来；

-v ：列出一些看不出来的特殊字符



#### tac 

查看文件内容，从最后一行开始显示

1）基本语法：

 ```
 tac [选项参数] 要查看的文件
 ```



#### more

查看文件内容，一页一页的显示文件内容。

1）基本语法：

       more 要查看的文件

2）功能使用说明

```
空白键 (space)：代表向下翻一页；

Enter：代表向下翻『一行』；

q：代表立刻离开 more ，不再显示该文件内容。

Ctrl+F 向下滚动一屏

Ctrl+B 返回上一屏

= 输出当前行的行号

:f 输出文件名和当前行的行号
```



#### less

less 的作用与 more 十分相似，都可以用来浏览文字档案的内容，不同的是 less 允许使用 [pageup] [pagedown]往回滚动。

1）基本语法：

    less 要查看的文件

2）功能使用说明

```
空白键：向下翻动一页；

[pagedown]：向下翻动一页；

[pageup]：向上翻动一页；

/字串：向下搜寻『字串』的功能；n：向下查找；N：向上查找；

?字串：向上搜寻『字串』的功能；n：向上查找；N：向下查找；

q：离开 less 这个程序；
```



#### head

查看文件内容，只看头几行。

1）基本语法

```
head -n 10 文件   # 功能描述：查看文件头 10 行内容，10 可以是任意行数
```



#### tail

查看文件内容， 从指定点开始将文件写到标准输出。

1）基本语法

（1）tail -n 10 文件（功能描述：查看文件头10行内容，10可以是任意行数）

（2）tail  –f  文件（功能描述：实时追踪该文档的所有更新）

```
tail -n 5  文件名  # 查看后几行
tail -f error.log  # 不断刷新，看到最新内容
```



### open 打开文件





### mv 移动/重命名



用法：mv 文件名或目录 目标目录
mv a.txt ../  将a文件移动到上级目录（将一个文件移动到另一个目录没有重命名）
mv a.txt ../b.txt  将a文件移动到上一级并改名为b文件（将一个文件移动到另一个目录并重命名）



### cp 复制

用法：cp ［选项］文件名或目录 目标地址
-R 拷贝目录及目录下所有目录和文件
cp a.txt b.txt  将a文件复制，且另命名为b文件（目录名）



### find 查找文件

用法：find [路径] [选项]
常用选项有：
find . -name *.log  在当前目录查找以.log结尾的文件
find / -name log  在根目录查找log命名的目录



### grep 过滤

在指定文件中查找字符（串）并打印该行
用法：grep 字符串 文件名     
grep band file 在file文件中找寻band字符串



## 时间日期类

1）基本语法

date [OPTION]... [+FORMAT]



### date 显示当前时间

1）基本语法：

    date        #  显示当前时间 
    
    date +%Y    # 显示当前年份                                      
    date +%m    # 显示当前月份                                      
    date +%d    # 显示当前是哪一天                                 
    
    # 显示当前年月日各种格式
    date +%Y%m%d
    date +%Y/%m/%d
    date "+%Y-%m-%d %H:%M:%S"  # 显示年月日时分秒



### date 显示非当前时间

1）基本语法：

```
date -d '1 days ago'   # 显示前一天日期



date -d next-day +%Y%m%d		# 显示明天日期
date -d 'next monday'				# 显示下周一时间
```

date -d "1 days ago"

### date 设置系统时间

1）基本语法：

​    date -s 字符串时间



### cal 查看日历

1）基本语法：

```
cal [选项]
```

不加选项，显示本月日历

选项：

- -3：显示系统前一个月，当前月，下一个月的日历

- 具体某一年：显示这一年的日历。

```
cal 6 2020
cal 2020
cal
```



## 用户管理命令



### useradd 添加新用户

1）基本语法：

```
useradd 用户名
```



### passwd 设置用户密码

1）基本语法：

```
passwd 用户名
```



### id 判断用户是否存在

1）基本语法：

```
id 用户名
```



### su 切换用户

1）基本语法：

```
su 用户名称
```



### userdel 删除用户

1）基本语法：

```
userdel 用户名
```

删除用户但保存用户主目录

```
userdel -r 用户名
```

用户和用户主目录，都删除



### who 查看登录用户信息

1）基本语法

```
whoami
```

显示自身用户名称

```
who am i
```

显示登录用户的用户名

```
who
```

看当前有哪些用户登录到了本台机器上



### cat /etc/passwd 查看创建了哪些组



### usermod 修改用户

1）基本语法：

```
usermod -g 用户组 用户名
```

2）案例：

将用户 user1 加入 dev 用户组

```
usermod –g dev user1
```





## 其他操作



### df 文件系统的磁盘空间占用情况

df命令的功能是用来检查linux服务器的文件系统的磁盘空间占用情况。



### ps 查看进程（动态）

-ef 显示所有运行进程，并显示启动进程的命令





### netstat 查看网络状况 （net status的简写）

netstat -apn 查看所有端口
an，按一定顺序排列输出
p，表示显示哪个进程在调用



### | 管道符 （竖线）

在命令之间建立管道，将前面命令的输出作为后面命令的输入。
通过命令查找 tomcat 进程：ps -ef | grep tomcat
通过命令查找到占用此端口的进程编号：netstat -apn|grep 8080



### uname 查看系统

-m 查看系统是几位操作系统
-r 查看系统的内核版本
-a 查看详细的系统内核版本和系统的操作系统



### su 切换用户

su root



### history 查看命令历史记录





### chmod 权限赋予命令

-R 递归改变目录下所有子目录和文件的权限
数字方式：r=4 w=2 x=1





### tar 解压，压缩 tar.gz

tar -czvf test.tar.gz test

将 test 文件夹压缩成 test.tar.gz

tar -xzvf test.tar.gz

将 test.tar.gz 解压得到 test 文件夹



### zip 解压，压缩zip

zip –r test.zip test

将 test 文件夹压缩成 test.zip，必须带 r 才会把文件压缩进去，不然会生成一个空的文件夹

unzip test.zip

将 test.zip 文件夹解压



### 关闭防火墙

 开启：service iptables start
关闭：service iptables stop

**永久关闭防火墙**
开启：chkconfig iptables on 
关闭：chkconfig iptables off

### shutdown 关机



## 参考

https://blog.csdn.net/weixin_38407447/article/details/90581454?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight

https://www.cnblogs.com/binghuaZhang/p/11139326.html