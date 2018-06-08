## Linux 
```
1. 程序开机启动，他们在window中叫做服务（service），在Linux中叫做守护进程
2. chown 修改文件属性
3. chgrp 修改文件属组
4. 处理目录的常用命令
    * ls: 列出目录
    * cd：切换目录
    * pwd：显示目前的目录
    * mkdir：创建一个新的目录
    * rmdir：删除一个空的目录
    * cp: 复制文件或目录
    * rm: 移除文件或目录
5. 查看文件内容
    * cat  由第一行开始显示文件内容
    * tac  从最后一行开始显示，可以看出 tac 是 cat 的倒著写！
    * nl   显示的时候，顺道输出行号！
    * more 一页一页的显示文件内容
    * less 与 more 类似，但是比 more 更好的是，他可以往前翻页！
    * head 只看头几行
    * tail 只看尾巴几行
6. Linux磁盘管理
    * df：列出文件系统的整体磁盘使用量
    * du：检查磁盘空间使用量
    * fdisk：用于磁盘分区
7. 磁盘的挂载和卸除
#### Linux 的磁盘挂载使用 mount 命令，卸载使用 umount 命令。
8. linux yum命令
##### yum

> yum [options] [command] [package ...]

* options：可选，选项包括-h（帮助），-y（当安装过程提示选择全部为"yes"），-q（不显示安装的过程）等等。
* command：要进行的操作。
* package操作的对象。
9. yum常用命令
    1. 列出所有可更新的软件清单命令：yum check-update
    2. 更新所有软件命令：yum update
    3. 仅安装指定的软件命令：yum install <package_name>
    4. 仅更新指定的软件命令：yum update <package_name>
    5. 列出所有可安裝的软件清单命令：yum list
    6. 删除软件包命令：yum remove <package_name>
    7. 查找软件包 命令：yum search <keyword>
    8. 清除缓存命令:
        * yum clean packages: 清除缓存目录下的软件包
        * yum clean headers: 清除缓存目录下的 headers
        * yum clean oldheaders: 清除缓存目录下旧的 headers
        * yum clean, yum clean all (= yum clean packages;
        * yum clean oldheaders) :清除缓存目录下的软件包及旧的headers

## Shell
##### Shell 是一个用 C 语言编写的程序，它是用户使用 Linux 的桥梁。Shell 既是一种命令语言，又是一种程序设计语言。
##### Shell 脚本（shell script），是一种为 shell 编写的脚本程序。
##### #! 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。
1. 常用命令
    * echo 命令向用于向窗口输出文本，结尾自动添加换行符
    * printf命令
    > printf  format-string  [arguments...]
    ```
    %s %c %d %f都是格式替代符
    %-10s 指一个宽度为10个字符（-表示左对齐，没有则表示右对齐），任何字符都会被显示在10个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。
    %-4.2f 指格式化为小数，其中.2指保留2位小数。

    printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg  
    printf "%-10s %-8s %-4.2f\n" 郭靖 男 66.1234 
    printf "%-10s %-8s %-4.2f\n" 杨过 男 48.6543 
    printf "%-10s %-8s %-4.2f\n" 郭芙 女 47.9876 
    ```
    * test命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试

2. 执行shell脚本的两种方法
* 作为可执行程序
```
chmod -x ./test.sh #使脚本具有执行权限
./test.sh #执行脚本
```
* 作为解释器参数
```
/bin/sh test.sh
```
3. 定义变量
##### 定义变量变量不加美元符号（$）变量和等号之间不能有空格
```
yourname="test"
```
##### 命名规则
* 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
* 中间不能有空格，可以使用下划线（_）。
* 不能使用标点符号。
* 不能使用bash里的关键字（可用help命令查看保留关键字）。
4. 使用一个定义过的变量，只要在变量名前面添加美元符号即可
```
echo $yourname
echo ${yourname}
```
5. 只读变量readonly yourname
6. 删除变量unset yourname。变量被删除后不能再次使用。unset 命令不能删除只读变量。
7. 变量类型
* 局部变量 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
* 环境变量 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
* shell变量 shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行 
8. Shell字符串
* 单引号字符串原样输出，字符串中的变量无效，单引号中不能有单引号
* 双引号字符串可以有变量，可以出现转义字符。
* 获取字符串长度 echo ${#a}
* 提取字符串 echo ${string:1:4} 提取从第二个字符开始的四个字符
* 查找子字符串
```
string="runoob is a great company"
echo `expr index "$string" is`  # 输出 8
```
9. Shell 数组（一维数组，没有数组大小的限定）
##### 在Shell中，用括号来表示数组，数组元素用"空格"符号分割开。定义数组的一般形式为：
> 数组名=(值1 值2 ... 值n)
10. 读取数组 ${数组名[下标]}
11. 获取数组长度
* 取得数组元素的个数
> length=${#array_name[@]}
*  或者
> length=${#array_name[*]}
*  取得数组单个元素的长度
> lengthn=${#array_name[n]}
```
my_array=(A B "C" D)
for a in ${my_array[*]}
do
echo $a
done
```
12. Shell 注释
##### 以"#"开头的行就是注释，会被解释器忽略。
13. Shell 基本运算符
##### expr 是一款表达式计算工具，使用它能完成表达式的求值操作。
```
a=`expr 2 + 2`
echo ${a}
```
####   注意
> 表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。

> 完整的表达式要被 ` ` 包含，注意这个字符不是常用的单引号，在 Esc 键下边。

> 条件表达式要放在方括号之间，并且要有空格，例如: [$a==$b] 是错误的，必须写成 [ $a == $b ]。

>乘号(*)前边必须加反斜杠(\)才能实现乘法运算；

>在 MAC 中 shell 的 expr 语法是：$((表达式))，此处表达式中的 "*" 不需要转义符号 "\" 。
14. 关系运算符
* -eq 相等
* -ne 不相等
* -gt 大于
* -lt 小于
* -ge 大于等于
* -le 小于等于
15. 布尔运算符
* ！非
* -o 或
* -a 与
16. 逻辑运算符
* &&逻辑的AND ||逻辑的OR
17. 字符串运算符
18. 文件测试运算符
19. Shell流程控制
* if语句
```
if
then
else
fi

if
then
elif
then
else
fi
```
* for语句
```
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done    
```
* while语句
```
while condition
do
    command
done
```
* case语句
```
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```
* break命令允许跳出所有循环 continue，它不会跳出所有循环，仅仅跳出当前循环。

20. 函数
21. Shell 输入/输出重定向
* command > file	将输出重定向到 file。
* command < file	将输入重定向到 file。
* command >> file	将输出以追加的方式重定向到 file。
* n > file	将文件描述符为 n 的文件重定向到 file。
* n >> file	将文件描述符为 n 的文件以追加的方式重定向到 file。
* n >& m	将输出文件 m 和 n 合并。
* n <& m	将输入文件 m 和 n 合并。
* << tag	将开始标记 tag 和结束标记 tag 之间的内容作为输入。
22. Shell 文件包含

[Linux命令大全] (http://www.runoob.com/linux/linux-command-manual.html)

```