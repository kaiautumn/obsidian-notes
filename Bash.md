## 一、简介
Bash是 Linux系统默认的 Shell。
Shell 本身是一个程序，只有一个命令提示符，又称为命令行环境
Shell 是一个命令解释器
扩展名为 sh
## 快捷键

ctrl+C      终止正在执行的命令
Ctrl+U/K 从光标的位置删除到行首/行尾
Ctrl+D     关闭Shell会话
## 扩展
##### 波浪线扩展
~会自动扩展成用户的主目录
~dir表示扩展成主目录的某个子目录，dir是子目录名
~user表示扩展成user的主目录
~+会扩展当前所在的目录，和pwd一样
##### ？字符扩展
? 代表文件路径里任意单个字符，即不确定某个文件里的名字有哪些字母
#####  \*字符扩展*
\*表示文件路径里任意数量的字符，包括零个字符
##### \[]扩展
\[]可以找包含括号内任意一个字符的文件
\[ab]可以找到 a.txt b.txt（这俩确实存在的情况下）
\[!ab]则表示匹配不在括号内的字符
\[start-end]表示连续的范围，\[a-c]为abc，\[0-9]为0123456789
##### {}扩展
{ }表示分别扩展大括号内的所有值，大括号内逗号分隔
```bash
1. `$ echo d{a,e,i,u,o}g`
2. `dag deg dig dug dog`

3. `$ echo Front-{A,B,C}-Back`
4. `Front-A-Back Front-B-Back Front-C-Back`
```
{start..end..step}扩展表示连续的序列,step为步长
{a..z}可扩展为26个小写英文字母
常用于新建一些列目录
```bash
$ mkdir {2007..2009}-{01..12}
```
也可以用于循环
```bash
for i in {1..4}
```
##### 变量扩展
$开头的词元视为变量，将其扩展为变量值
##### 子命令扩展
$(...)可以扩展另一个命令的运行结果
##### 算术扩展
$((.....))可扩展成整数运算的结果
##### 字符扩展
- `[[:alnum:]]`：匹配任意英文字母与数字
- `[[:alpha:]]`：匹配任意英文字母
- `[[:blank:]]`：空格和 Tab 键。
- `[[:cntrl:]]`：ASCII 码 0-31 的不可打印字符。
- `[[:digit:]]`：匹配任意数字 0-9。
- `[[:graph:]]`：A-Z、a-z、0-9 和标点符号。
- `[[:lower:]]`：匹配任意小写字母 a-z。
- `[[:print:]]`：ASCII 码 32-127 的可打印字符。
- `[[:punct:]]`：标点符号（除了 A-Z、a-z、0-9 的可打印字符）。
- `[[:space:]]`：空格、Tab、LF（10）、VT（11）、FF（12）、CR（13）。
- `[[:upper:]]`：匹配任意大写字母 A-Z。
- `[[:xdigit:]]`：16进制字符（A-F、a-f、0-9）
## 变量
1. 命名规则：
>- 只能包含字母、数字、下划线
>- 不能以数字开头
>- 不能使用 Shell 关键字
>- 大写字母表示常量
>- 避免特殊符号和空格
2. 变量类型：
>- 字符串：使用 \' 和 \" 来定义字符串
>- 整数：declare 或 typeset 声明
>```bash
>declare -i my_integer=42
>```
>若尝试将其赋值为非整数，Sehll会强制将其转化为整数
>- 数组：
>```bash
>declare -A associative_array
>associative_array["name"]="John"
>associative_array["age"]=30
>```
>- 环境变量：操作系统或用户设置的特殊变量
>- 特殊变量：$0 表示脚本名称 ，$1、\$2表示脚本参数 ，\$\#表示传给脚本的参数数量 ，\$\?表示上一个命令的退出状态
3. 变量赋值：等号两侧不能有空格
```bash
your_name="balabala"
```
4. 隐式赋值
```bash
for file in 'ls/etc'
```
上面语句会将 /etc 下目录的文件名循环出来

5. 使用变量：使用定义过的变变量需在变量前面加 $
```bash
echo $your_name
```
变量名可加花括号\{\}以帮解释器区分变量的边界
6. 重写变量：
```bash
your_name="lihua"
echo $your_name
your_name="666"
```
7. 只读变量：使用 readonly 将变量定义为只读变量
```bash
your_name="nihao"
readonly your_name
your_name="lihua"
#会提示your_name为只读变量
```
8. 删除变量：unset
```bash
unset your_name
```
unset 不能删除只读变量

### 字符串
###### 单引号双引号。
- 单引号的任何字符会原样输出，字符串中的变量是无效的
- 双引号里可以有变量、可以出现转义字符
>```bash
your_name="runoob"
str="Hello, I know you are \"$your_name\"! \n"
echo -e $str
>```
>输出结果为 
>Hello, I know you are "runoob"! 

###### 字符串拼接
```bash
#双引号
str_1="hello,"$your_name"!"
str_2="hello,${your_name}!"
#单引号
str_3='hello,'$your_name'!'  #输出hello,lihua !
str_4='hello,${your_name}!'  #输出hello,${your_name} !
```
###### 获取字符串长度
```bash
str="abcd"
echo ${#str}
str_2=(1,2,3)
echo ${str_2} #等价于echo ${str_2[0]}
```
###### 提取子字符串
```bash
str="runoob is a great site"
echo ${str:1:4} #输出unoo
```
###### 查找子字符串
```bash
echo `expr index "$str" io` #在str里查找第一个i或o
```
### 数组
只支持一维数组，初始化不需要定义数组大小
```bash
数组名=(value1，value2,...,value n)
${数组名[下标]}
```
###### 所有的元素
```bash
echo ${array_name[@]}
```
###### 获取数组长度
```bash
# 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
length=${#array_name[n]}
```
###### 关联数组
使用任意的字符串或整数作为下标来访问数组元素
```bash
declare -A array_name #-A就是用于声明一个关联数组
例:
declare -A site
site["google"]="www.google.com"
site["runoob"]="www.runoob.com"
site["taobao"]="www.taobao.com"

echo ${site["runoob"]}    #输出www.runoob.com
```
在数组前加一个感叹号可以获取数组的所有键：
```bash
declare -A site
site["google"]="www.google.com"
site["runoob"]="www.runoob.com"
site["taobao"]="www.taobao.com"

echo "数组的键为: ${!site[*]}"
echo "数组的键为: ${!site[@]}"

输出结果为：
数组的键为: google runoob taobao
数组的键为: google runoob taobao
```

## 注释
经典#后跟注释
###### 多行注释
```bash
: <<'COMMENT'
这是注释的部分。
可以有多行内容。
COMMENT

:<<'
注释内容...
注释内容...
注释内容...
'

:<<!
注释内容...
注释内容...
注释内容...
!
```
也可以直接用：号
```bash
: '
这是注释的部分，可以有多行内容。
'
```

## 传递参数
```bash
echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";
```
为脚本设置可执行权限，并执行脚本，输出结果如下：
```
$ chmod +x test.sh 
$ ./test.sh 1 2 3
Shell 传递参数实例！
执行的文件名：./test.sh
第一个参数为：1
第二个参数为：2
第三个参数为：3
```
## 运算符
###### 算术运算符
原生bash不支持运算，但是可以用awk、expr（常用）命令实现
表达式和运算符之间要有空格，即2 + 2，不能2+2
注意，乘法需要 \* 才能实现
```bash
val=`expr 2 + 2`
val=`expr $a / $b`
val=`expr $a \* $b`
```
((.....))语法可以进行整数的算术运算
###### 关系运算符
| 运算符 | 说明       | 举例        |
| --- | -------- | --------- |
| -eq | 是否相等     | $a -eq $b |
| -ne | 是否不相等    |           |
| -gt | 是否左大于右   |           |
| -lt | 是否左小于右   |           |
| -ge | 是否左大于等于右 |           |
| -le | 是否左小于等于右 |           |
###### 布尔运算符

| 运算符 | 说明  | 举例                           |
| --- | --- | ---------------------------- |
| ！   | 非   | \[ ! false ]                 |
| -o  | 或   | \[ $a -lt 20 -o $b -gt 100 ] |
| -a  | 与   |                              |
###### 逻辑运算符

| 运算符  | 说明  | 举例                               |
| ---- | --- | -------------------------------- |
| &&   | 逻辑与 | \[\[ $a -lt 100 && $b -gt 100 ]] |
| \|\| | 逻辑非 |                                  |
&&是只有a成功才会进行b
| |是只有a失败才会进行b
###### 字符串运算符

| 运算符 | 说明         | 举例    |
| --- | ---------- | ----- |
| =   | 两个字符串是否相等  |       |
| !=  | 两个字符串是否不相等 |       |
| -z  | 长度是否为0     | -z $a |
| -n  | 长度是否不为0    | -n $a |
| $   | 是否空        | $a    |
## 行操作
Bash 内置了 Readline 库，具有这个库提供的很多“行操作”功能，比如命令的自动补全，可以大大加快操作速度。

这个库默认采用 Emacs 快捷键，也可以改成 Vi 快捷键。
```
$ set -o vi`
```

下面的命令可以改回 Emacs 快捷键。
```
$ set -o emacs
```

## 脚本入门
脚本的第一行通常是指定解释器，即这个脚本必须通过什么解释器执行。这一行以`#!`字符开头，这个字符称为 Shebang，所以这一行就叫做 Shebang 行。`#!`后面就是脚本解释器的位置，Bash 脚本的解释器一般是`/bin/sh`或`/bin/bash`
## read 命令
read\[选项]\[变量名]，可接受多个变量
- -t：设置超时的秒数
- -p：提示信息，即先显示内容，后接受用户的输入
## echo命令
echo\[选项\]\[字符串\]
- -n：取消末尾的回车符
```bash
echo -n"Loading..."
echo "Done!"
```
- -e：启用转义字符解释
```bash
echo -e "First line\nSecond line"
```

| 转义  | 说明    |
| --- | ----- |
| \v  | 垂直制表符 |
| \b  | 退格    |
| \r  | 回车    |

###### 多行输入
Bash单个命令一般是一行，若想写成多行，在每一行结尾加上\\，Bash就会将下一行和当行放在一起
```bash
1. `$ echo foo bar`

2. `# 等同于`
3. `$ echo foo \`
4. `bar`
```
###### 高级用法
- 输出到文件
```bash
#重定向将输出保存到文件
echo "This will be saved to file" >output.txt
#追加内容到文件
echo "Additional line" >> output.txt
```
- 彩色输出
```bash
#使用ANSI转移码实现彩色文本
echo -e "\033[31mRed Text\033[0m"
echo -e "\033[42;31mGreen Background with Red Text\033[0m"
```
颜色代码参考：
>- 前景色：30(黑)、31(红)、32(绿)、33(黄)、34(蓝)、35(紫)、36(青)、37(白)
>- 背景色：40-47 对应上述颜色
>- `\033[0m` 重置所有属性
- 输出命令执行结果
```bash
echo "Today is $(date)"
```

## printf命令
printf format-string \[arguments...]
format-string：包含普通字符和格式说明的字符串
arguments：与格式说明相对应的变量或值
###### 格式说明符
>%s 字符串
>%d 十进制整数
>%f 浮点数
>%c 字符
>%x 十六进制数
>%o 八进制数
>%b 二进制数
>%e 科学计数法表示的浮点数

说明：遇到格式说明符后读取下一个参数，并按说明符的格式处理该参数，将结果输出
```bash
# 整数
printf "Decimal: %d\nHex: %x\nOctal: %o\n" 255 255 255
# 浮点数
printf "Float: %f\nScientific: %e\n" 3.14159 3.14159
# 字符串
printf "Name: %s\n" "Bob"
# 字符
printf "First letter: %c\n" "A"

#结果
Decimal: 255
Hex: ff
Octal: 377
Float: 3.141590
Scientific: 3.141590e+00
Name: Bob
First letter: A
```
###### 格式化控制
```bash
# 字段宽度和对齐
printf "|%10s|\n|%-10s|\n" "right" "left"
# 数字前导零
printf "Year: %04d\n" 23
# 浮点数精度
printf "Pi: %.2f\n" 3.14159

#结果
|     right|
|left      |
Year: 0023
Pi: 3.14

```
###### 多参数处理
```bash
printf "%-10s %5d %8.2f\n" "Apple" 5 2.5 "Orange" 3 1.75

#结果
Apple          5     2.50
Orange         3     1.75
```
## test命令
用于评估表达式并返回布尔值，通常与if结合使用
```bash
test EXPRESSION
# 或
[ EXPRESSION ]  # 注意方括号内必须有空格
[ [ EXPRESSION ] ]
```
###### 文件测试操作
| 操作符 | 描述      | 示例                     |
| --- | ------- | ---------------------- |
| e   | 文件是否存在  | `[ -e file.txt ]`      |
| -f  | 是普通文件   | `[ -f /path/to/file ]` |
| -d  | 是目录     | `[ -d /path/to/dir ]`  |
| -r  | 可读      | `[ -r file.txt ]`      |
| -w  | 可写      | `[ -w file.txt ]`      |
| -x  | 可执行     | `[ -x script.sh ]`     |
| -s  | 文件大小 >0 | `[ -s logfile ]`       |
| -L  | 是符号链接   | `[ -L symlink ]`       |
###### 字符串比较
|操作符|描述|示例|
|---|---|---|
|-z STRING|字符串为空|`[ -z "$var" ]`|
|-n STRING|字符串非空|`[ -n "$var" ]`|
|STRING1 = STRING2|字符串相等|`[ "$var1" = "$var2" ]`|
|STRING1 != STRING2|字符串不等|`[ "$var1" != "$var2" ]`|
###### 数值比较
|操作符|描述|示例|
|---|---|---|
|-eq|等于|`[ "$a" -eq "$b" ]`|
|-ne|不等于|`[ "$a" -ne "$b" ]`|
|-gt|大于|`[ "$a" -gt "$b" ]`|
|-ge|大于或等于|`[ "$a" -ge "$b" ]`|
|-lt|小于|`[ "$a" -lt "$b" ]`|
|-le|小于或等于|`[ "$a" -le "$b" ]`|
###### 逻辑操作符
|操作符|描述|示例|
|---|---|---|
|!|逻辑非|`[ ! -f "$file" ]`|
|-a|逻辑与|`[ "$a" -eq 1 -a "$b" -eq 2 ]`|
|-o|逻辑或|`[ "$a" -eq 1 -o "$b" -eq 2 ]`|
## 流程控制
### if
```bash
if condition
then
	command1
	command2
fi
```
写成一行，用于终端命令提示符：
```bash
if [ $(ps -ef | grep -c "ssh") -gt 1 ]; then echo "true"; fi
```
if else
```bash
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```
if else 中\[...] ，大于用 -gt，小于用 -lt  ； ((....))，大于小于可直接> <
### for
```bash
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done
```
写成一行：
```bash
for var in item1 item2 ... itemN; do command1; command2… done;
```
### while
```bash
while condition
do
    command
done
```
### until循环
until循环执行到条件为true时停止
```bash
until condition
do
    command
done
```
### case...esac
一种多分枝选择结构
```bash
case 值 in
模式1)
    command1
    command2
    ...
    commandN
    ;;
模式2)
    command1
    command2
    ...
    commandN
    ;;
esac
```
示例
```bash
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

#结果
输入 1 到 4 之间的数字:
你输入的数字为:
3
你选择了 3
```
### 跳出循环
break ,  continue

## 函数
一般格式如下：
```bash
[ function ] funname ()
{
    action;
    [return int;]
}
```

```bash
funWithReturn(){
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum !"
    return $(($aNum+$anotherNum))
}
funWithReturn
echo "输入的两个数字之和为 $? !"

#结果：
这个函数会对输入的两个数字进行相加运算...
输入第一个数字: 
1
输入第二个数字: 
2
两个数字分别为 1 和 2 !
输入的两个数字之和为 3 !
```
函数的返回值在调用该函数后通过 $? 获得，且return 只能返回一个0~255间的数

## 输入输出重定向
一般情况下，大多数命令的标准输入和标准输出都是终端，但是可以更改

|命令|说明|
|---|---|
|command > file|将输出重定向到 file。|
|command < file|将输入重定向到 file。|
|command >> file|将输出以追加的方式重定向到 file。|
|n > file|将文件描述符为 n 的文件重定向到 file。|
|n >> file|将文件描述符为 n 的文件以追加的方式重定向到 file。|
|n >& m|将输出文件 m 和 n 合并。|
|n <& m|将输入文件 m 和 n 合并。|
|<< tag|将开始标记 tag 和结束标记 tag 之间的内容作为输入。|
```bash
command1 > file1
#表示执行command1然后将输出的内容存入file1
```
## 文本处理
- cat
将文件的内容显示在标准输出、
- nl
为文本文件添加行号
- sort
将文本文件的所有行排序后输出
- uniq
排序后删除重复的行
- cut
从文本行中抽取文本，并输出到标准输出
- paste
将多个文本文件按行合并
- wc
输出文本文件的统计信息
- head
返回头部
- tail
返回文本文件的尾部
- grep
搜索符合某个模式的行
- sed
强大的文本编辑工具
## 文件操作
##### cp
用于将文件或目录拷贝到目的地
##### mkdir
用于新建目录
##### mv
用于将源文件移动到目的地
##### rm
删除文件
##### ln
建立链接文件
## 文件系统
##### pwd
显示当前所在目录
##### cd
改变所在目录
##### ls
显示当前目录的内容
##### stat
加强版的ls，可以显示详细信息
##### touch
设置或更新文件的访问
##### file
显示文件的类型
##### chmod
更改文件的权限
##### umask
查看权限和权限掩码
##### du
查看指定目录的大小
##### find
## 硬件操作
##### df
查看硬盘信息
##### free
查看内存占用情况

## 进程管理
##### ps
列出进程信息
##### top
查看当前机器的状态
##### jobs
查看后台任务
##### fg
将后台任务切换到前台
##### bg
将暂停的任务转到后台
##### kill
杀死进程
