# LINUX SHELL

## LINUX 基础

* 查看指令帮助
  > [command] --help  
  > man [command]  
  > info

* 关机、重启、定时关机
  > poweroff shutdown 关机
  > reboot 重启
  > sync 同步数据到磁盘，关机开机前可以执行下

# 文件、文件夹权限

* linux 新建的文件夹都在 /etc/group 内有记录

* Linux 文件权限的重要性：

  > 系统保护的功能
  > 团队开发软件或数据共享的功能
  > 未将权限设定妥当的危害

  ```
    r:4
    w:2
    x:1
  ```
  ![avatar](D:\install\notable\data\attachments\linux\rwx.png)

  > chgrp ：改变文件所属群组
  ```
  [root@study ~]# chown [-R] 账号名称 文件或目录
  [root@study ~]# chown [-R] 账号名称:组名 文件或目录 选项与参数： -R : 进行递归(recursive)的持续变更，亦即连同次目录下的所有文件都变更  
  范例：将 initial-setup-ks.cfg 的拥有者改为 bin 这个账号：
  [root@study ~]# chown bin initial-setup-ks.cfg
  [root@study ~]# ls -l -rw-r--r--. 1 bin users 1864 May 4 18:01 initial-setup-ks.cfg 范例：将 initial-setup-ks.cfg 的拥有者与群组改回为
  root：
  [root@study ~]# chown root:root initial-setup-ks.cfg
  [root@study ~]# ls -l -rw-r--r--. 1 root root 1864 May 4 18:01 initial-setup-ks.cfg
  ```
  > chown ：改变文件拥有者

  > chmod ：改变文件的权限, SUID, SGID, SBIT 等等的特性 u--所有者 g--群组 o--其他 a--所有
  > ![avatar](D:\install\notable\data\attachments\linux\chmod.png)
  ```
  [root@study ~]# chmod u=rwx,go=rx .bashrc
  # 注意喔！那个 u=rwx,go=rx 是连在一起的，中间并没有任何空格符！
  [root@study ~]# ls -al .bashrc
  -rwxr-xr-x. 1 root root 176 Dec 29 2013 .bashrc
  ```

* 文件内容查阅
  ```
  cat 由第一行开始显示文件内容
  tac 从最后一行开始显示，可以看出 tac 是 cat 的倒着写！  
  nl 显示的时候，顺道输出行号！
  more 一页一页的显示文件内容
  less 与 more 类似，但是比 more 更好的是，他可以往前翻页！
  head 只看头几行
  ```

* 查找  ```find [PATH] [option] [action]```
  ```
  [root@study ~]# find [PATH] [option] [action]
  选项与参数：
  1. 与时间有关的选项：共有 -atime, -ctime 与 -mtime ，以 -mtime 说明
    -mtime n ：n 为数字，意义为在 n 天之前的『一天之内』被更动过内容的文件；
    -mtime +n ：列出在 n 天之前(不含 n 天本身)被更动过内容的文件档名；
    -mtime -n ：列出在 n 天之内(含 n 天本身)被更动过内容的文件档名。
    -newer file ：file 为一个存在的文件，列出比 file 还要新的文件档名
  范例一：将过去系统上面 24 小时内有更动过内容 (mtime) 的文件列出
  [root@study ~]# find / -mtime 0
    # 那个 0 是重点！0 代表目前的时间，所以，从现在开始到 24 小时前，
    # 有变动过内容的文件都会被列出来！那如果是三天前的 24 小时内？
    # find / -mtime 3 有变动过的文件都被列出的意思！
  范例二：寻找 /etc 底下的文件，如果文件日期比 /etc/passwd 新就列出
  [root@study ~]# find /etc -newer /etc/passwd
    # -newer 用在分辨两个文件之间的新旧关系是很有用的！
  ```

* AWK 是一种处理文本文件的语言，是一个强大的文本分析工具

  > {print $1} 就是将某一行（一条记录）中以空格为分割符的第一个字段打印出来。
  ```
  -F fs or --field-separator fs
  指定输入文件折分隔符，fs是一个字符串或者是一个正则表达式，如-F:
  -v var=value or --asign var=value
  赋值一个用户定义变量。
  -f scripfile or --file scriptfile
  从脚本文件中读取awk命令。
  -mf nnn and -mr nnn
  对nnn值设置内在限制，-mf选项限制分配给nnn的最大块数目；-mr选项限制记录的最大数目。这两个功能是Bell实验室版awk的扩展功能，在标准awk中不适用。
  -W compact or --compat, -W traditional or --traditional
  在兼容模式下运行awk。所以gawk的行为和标准的awk完全一样，所有的awk扩展都被忽略。
  -W copyleft or --copyleft, -W copyright or --copyright
  打印简短的版权信息。
  -W help or --help, -W usage or --usage
  打印全部awk选项和每个选项的简短说明。
  -W lint or --lint
  打印不能向传统unix平台移植的结构的警告。
  -W lint-old or --lint-old
  打印关于不能向传统unix平台移植的结构的警告。
  -W posix
  打开兼容模式。但有以下限制，不识别：/x、函数关键字、func、换码序列以及当fs是一个空格时，将新行作为一个域分隔符；操作符**和**=不能代替^和^=；fflush无效。
  -W re-interval or --re-inerval
  允许间隔正则表达式的使用，参考(grep中的Posix字符类)，如括号表达式[[:alpha:]]。
  -W source program-text or --source program-text
  使用program-text作为源代码，可与-f命令混用。
  -W version or --version
  打印bug报告信息的版本。
  ```



