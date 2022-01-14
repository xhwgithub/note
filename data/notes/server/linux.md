# LINUX SHELL

## 变量

* 类型
  > 1) __局部变量__ 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
  > 2) __环境变量__ 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
  > 3) __shell变量__ shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

* 自定义变量
  > 变量名前面加美元符号:
  > * echo $your_name
  > * echo ${your_name} 加花括号是为了帮助解释器识别变量的边界
* 变量赋值

  > your_name="tom"  
  > echo $your_name  
  > your_name="alibaba"  
  > echo $your_name  
  > __赋值的时候不能写$your_name="alibaba"，使用变量的时候才加美元符（$）__
* readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变
  > myUrl = "https://www.google.com"  
  > readonly myUrl
* 删除变量
  > unset variable_name
* 环境变量
  > $HOME 当前用户的登录子目录  
  > $PATH 以冒号分隔的用来搜索的子目录清单   
  > $0    shell脚本程序的名字

* 读取环境变量的方法：
  > export命令显示当前系统定义的所有环境变量  
  > echo $+关键字 命令输出当前的PATH环境变量的值
* 执行脚本的时候，需要往一个文件里自动输入N行内容。
  > 如果是少数的几行内容，还可以用echo追加方式，但如果是很多行，那么单纯用echo追加的方式就显得愚蠢之极了！
  > * 向文件test.sh里输入内容 cat << EOF >test.sh
  > * 追加内容 cat << EOF >>test.sh
  > * 覆盖内容 cat << EOF >test.sh


* 双引号
  > 双引号里可以有变量  
  > 双引号里可以出现转义字符

* basename dirname 的区别 /usr/lib/shell.sh

  |path|basename|dirname|  
                                                                                                                                        |----|--------|-------|
  |/usr/lib/shell.sh/lib|shell.sh |/usr/lib|

## 字符串

* 关键字
  > $$ ：Shell本身的PID（ProcessID）   
  > $! ：Shell最后运行的后台Process的PID     
  > $? ：最后运行的命令的结束代码（返回值）   
  > $0 ：Shell本身的文件名 1~n：添加到Shell的各参数值。$1是第1参数、$2是第2参数

* 单引号字符串的限制：
  > 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；  
  > 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

* 获取字符串长度
  > string="abcd"  
  > echo ${#string} #输出 4

* 提取子字符串
  > string="runoob is a great site"  
  > echo ${string:1:4} # 输出 unoo

* 查找子字符串
  > string="runoob is a great site"  
  > echo `expr index "$string" io`  # 输出 4

## Shell 基本运算符

* 算术运算符

  |运算符|说明|举例|
                                                            |---|---|---|
  |+| 加法|    `expr $a + $b` 结果为 30   |
  |-| 减法|    `expr $a - $b` 结果为 -10   |
  |*| 乘法|    `expr $a \* $b` 结果为 200。| 
  |/| 除法|    `expr $b / $a` 结果为 2。   |
  |%| 取余|    `expr $b % $a` 结果为 0。   | 
  |=| 赋值|    `a=$b 把变量 b 的值赋给 a。   | 
  |==|  相等|用于比较两个数字，相同则返回 true。    [ $a == $b ] 返回 false。|
  |!=| 不相等|用于比较两个数字，不相同则返回 true。    [ $a != $b ] 返回 true。|

* 关系运算符

  |运算符|说明|举例|
                                            |---|---|---|
  |-eq| 检测两个数是否相等，相等返回 true                |    [ $a -eq $b ] 返回 false|
  |-ne| 检测两个数是否不相等，不相等返回 true             |    [ $a -ne $b ] 返回 true |
  |-gt| 检测左边的数是否大于右边的，如果是，则返回 true     |    [ $a -gt $b ] 返回 false|
  |-lt| 检测左边的数是否小于右边的，如果是，则返回 true     |    [ $a -lt $b ] 返回 true |
  |-ge| 检测左边的数是否大于等于右边的，如果是，则返回 true。|    [ $a -ge $b ] 返回 false|
  |-le| 检测左边的数是否小于等于右边的，如果是，则返回 true。|    [ $a -le $b ] 返回 true |

* 布尔运算符

  |运算符|说明|举例|
                                            |---|---|---|
  |!    |非运算，表达式为 true 则返回 false，否则返回 true。    |[ ! false ] 返回 true。|
  |-o|    或运算，有一个表达式为 true 则返回 true。        |[ $a -lt 20 -o $b -gt 100 ] 返回 true。|
  |-a|    与运算，两个表达式都为 true 才返回 true。        |[ $a -lt 20 -a $b -gt 100 ] 返回 false。|

* 字符串运算符

  |运算符|说明|举例|
                                            |---|---|---|
  |=    |检测两个字符串是否相等，相等返回 true          |[ $a = $b ] 返回 false。|
  |!=   |检测两个字符串是否不相等，不相等返回 true       |[ $a != $b ] 返回 true。|
  |-z   |检测字符串长度是否为0，为0返回 true           |[ -z $a ] 返回 false。|
  |-n   |检测字符串长度是否不为 0，不为 0 返回 true     |[ -n "$a" ] 返回 true。|
  |$    |检测字符串是否为空，不为空返回 true            |[ $a ] 返回 true。|

* 文件测试运算符

  |运算符|说明|举例|
                                              |---|---|---|
  |-b file    |检测文件是否是块设备文件，如果是，则返回 true。                           |[ -b $file ] 返回 false。|
  |-c file    |检测文件是否是字符设备文件，如果是，则返回 true。                          |[ -c $file ] 返回 false。|
  |-d file    |检测文件是否是目录，如果是，则返回 true。                                |[ -d $file ] 返回 false。|
  |-f file    |检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。    |[ -f $file ] 返回 true。|
  |-g file    |检测文件是否设置了 SGID 位，如果是，则返回 true。                         |[ -g $file ] 返回 false。|
  |-k file    |检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。               |[ -k $file ] 返回 false。|
  |-p file    |检测文件是否是有名管道，如果是，则返回 true。                              |[ -p $file ] 返回 false。|
  |-u file    |检测文件是否设置了 SUID 位，如果是，则返回 true。                         |[ -u $file ] 返回 false。|
  |-r file    |检测文件是否可读，如果是，则返回 true。                                   |[ -r $file ] 返回 true。|
  |-w file    |检测文件是否可写，如果是，则返回 true。                                   |[ -w $file ] 返回 true。|
  |-x file    |检测文件是否可执行，如果是，则返回 true。                                  |[ -x $file ] 返回 true。|
  |-s file    |检测文件是否为空（文件大小是否大于0），不为空返回 true。                      |[ -s $file ] 返回 true。|
  |-e file    |检测文件（包括目录）是否存在，如果是，则返回 true。                         |[ -e $file ] 返回 true。|

## echo

* 输出日期 echo `date`