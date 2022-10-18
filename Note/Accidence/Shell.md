# Script的引入

- 英文翻译script为在本子上写字，当本子上的字能够一行一行在机器上跑起来时，就成了能跑的本子。中文翻译为脚本，恰恰就是 Because it can run
- Shell的种类：sh、bash、ksh、rsh、csh等
- 最常见的shell是玻恩写的Bourne Again Shell，简称为bash

# Shell命令

## HelloWorld

```bash
#!/bin/bash 
echo "Hello World!" # 回声：Hello World！
```

Note：#! 指定解释该脚本的Shell程序、记得添加可执行权限、扩展名并不影响脚本执行

## Shell注释

```bash
# 
```

```bash
:<<EOF
注释内容...
注释内容...
注释内容...
EOF

# EOF 也可以用其他符号

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

## 基本变量

```bash
# 定义变量 name（等号两侧不能有空格）
name="fanfan"
# 输出 name 并自动换行
echo $name
# 加括号指定变量边界，无误解的情况下可以不加
echo ${name}

# 变量可以二次赋值
name="fanfan"
echo $name
name="huanhuan"
echo $name

# 只读变量
myUrl="https://www.google.com"
readonly myUrl
myUrl="https://www.runoob.com" # 该处会报错

# 删除变量
# 变量被删除后不能再次使用，需要再次定义，unset 命令不能删除只读变量
unset variable_name

# 单引号字符串(不会替换变量)
str1='fanfan'
str2='huanhuan $str1'
echo $str2
- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用
# 双引号字符串(会替换变量)
str1='fanfan'
str2="huanhuan $str1"
echo $str2

your_name="runoob"
str="Hello, I know you are \"$your_name\"! \n"
echo -e $str
- 双引号里可以有变量
- 双引号里可以出现转义字符

# 字符串拼接

your_name="runoob"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1

# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3

# 获取字符串长度
str='zhangfanfan'
echo ${#str}

# 查询字符下标
str="zhangfanfan"
echo `expr index "$str" fa`
- 以上脚本中 ` 是反引号，而不是单引号 '
- 哪个字母先出现就计算哪个
```

## Shell数组

bash支持一维数组（不支持多维数组），并且没有限定数组的大小

`数组名=(值1 值2 ... 值n)`

```bash
array_name=(1 2 3 4)
echo ${array_name[0]}
```

可以不使用连续的下标，而且下标的范围没有限制

```bash
array_name[0]=0
array_name[1]=1
array_name[5]=n
echo ${array_name[1]}
echo ${array_name[5]}
```

@获取全部元素

```bash
name=(
    fanfan
    Alice
    Tom
)
echo ${name[@]}
```

获取数组长度

```bash
name=(
    fanfan
    Alice
    Tom
)
# 元素个数
length=${#name[@]}
echo ${length}
length=${#name[*]}
echo ${length}
# 单个元素长度
length=${#name[0]}
echo ${length}
```

## Shell传递参数

脚本内获取参数的格式为：**$n 、n**代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……

```bash
#!/bin/bash
echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";
```

```bash
Shell 传递参数实例！
执行的文件名：Test.sh
第一个参数为：1
第二个参数为：2
第三个参数为：3
```

```bash
#!/bin/bash
echo "Shell 传递参数实例！";
echo "shell文件名：${0}"
echo "参数个数：${#}"
echo "所有参数(字符串格式)：${*}"
echo "所有参数(单个字符格式)：${@}"
```

```bash

Shell 传递参数实例！
shell文件名：Test.sh
参数个数：3
所有参数(字符串格式)：1 2 3
所有参数(单个字符格式)：1 2 3
```

$* 与 $@ 区别

- 相同点：都是引用所有参数。
- 不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则 " * " 等价于 "1 2 3"（传递了一个参数），而 "@" 等价于 "1" "2" "3"（传递了三个参数）

```bash
#!/bin/bash
echo "@和*的区别";
echo "@"
for i in "${@}"; do
    echo ${i}
done
echo "*"
for i in "${*}"; do
    echo ${i}
done
```

## 算术运算符

```bash
#!/bin/bash

a=10
b=20

val=`expr ${a} + ${b}`
echo "a + b = ${val}"
val=`expr ${a} - ${b}`
echo "a - b = ${val}"
val=`expr ${a} \* ${b}`
echo "a * b = ${val}"
val=`expr ${a} / ${b}`
echo "a / b = ${val}"
val=`expr ${a} % ${b}`
echo "a % b = ${val}"
if [ ${a} == ${b} ]
then
    echo "a == b"
fi
if [ ${a} != ${b} ]
then
    echo "a != b"
fi
```

```bash
a + b = 30
a - b = -10
a * b = 200
a / b = 0
a % b = 10
a != b
```

- 条件表达式要放在方括号之间，并且要有空格，例如: **[$a==$b]**是错误的，必须写成 **[ $a == $b ]**
- 乘号(*)前边必须加反斜杠(\)才能实现乘法运算
- if...then...fi 是条件语句，后续将会讲解
- 在 MAC 中 shell 的 expr 语法是：**$((表达式))**，此处表达式中的 "*" 不需要转义符号 "\"

## **关系运算符**

```bash
#!/bin/bash

a=10
b=20

if [ $a -eq $b ]
then
   echo "$a -eq $b : a 等于 b"
else
   echo "$a -eq $b: a 不等于 b"
fi
if [ $a -ne $b ]
then
   echo "$a -ne $b: a 不等于 b"
else
   echo "$a -ne $b : a 等于 b"
fi
if [ $a -gt $b ]
then
   echo "$a -gt $b: a 大于 b"
else
   echo "$a -gt $b: a 不大于 b"
fi
if [ $a -lt $b ]
then
   echo "$a -lt $b: a 小于 b"
else
   echo "$a -lt $b: a 不小于 b"
fi
if [ $a -ge $b ]
then
   echo "$a -ge $b: a 大于或等于 b"
else
   echo "$a -ge $b: a 小于 b"
fi
if [ $a -le $b ]
then
   echo "$a -le $b: a 小于或等于 b"
else
   echo "$a -le $b: a 大于 b"
fi
```

```bash
10 -eq 20: a 不等于 b
10 -ne 20: a 不等于 b
10 -gt 20: a 不大于 b
10 -lt 20: a 小于 b
10 -ge 20: a 小于 b
10 -le 20: a 小于或等于 b
```

## **布尔运算符**

| ! | 非运算，表达式为 true 则返回 false，否则返回 true |
| --- | --- |
| -o | 或运算，有一个表达式为 true 则返回 true |
| -a | 与运算，两个表达式都为 true 才返回 true |

## **逻辑运算符**

| && | 逻辑的 AND |
| --- | --- |
| || | 逻辑的 OR |

## **字符串运算符**

| = | 检测两个字符串是否相等，相等返回 true | [ $a = $b ] 返回 false |
| --- | --- | --- |
| != | 检测两个字符串是否不相等，不相等返回 true | [ $a != $b ] 返回 true |
| -z | 检测字符串长度是否为0，为0返回 true | [ -z $a ] 返回 false |
| -n | 检测字符串长度是否不为 0，不为 0 返回 true | [ -n "$a" ] 返回 true |
| $ | 检测字符串是否不为空，不为空返回 true | [ $a ] 返回 true |

## **文件测试运算符**

| -b file | 检测文件是否是块设备文件，如果是，则返回 true。 | [ -b $file ] 返回 false。 |
| --- | --- | --- |
| -c file | 检测文件是否是字符设备文件，如果是，则返回 true。 | [ -c $file ] 返回 false。 |
| -d file | 检测文件是否是目录，如果是，则返回 true。 | [ -d $file ] 返回 false。 |
| -f file | 检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。 | [ -f $file ] 返回 true。 |
| -g file | 检测文件是否设置了 SGID 位，如果是，则返回 true。 | [ -g $file ] 返回 false。 |
| -k file | 检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。 | [ -k $file ] 返回 false。 |
| -p file | 检测文件是否是有名管道，如果是，则返回 true。 | [ -p $file ] 返回 false。 |
| -u file | 检测文件是否设置了 SUID 位，如果是，则返回 true。 | [ -u $file ] 返回 false。 |
| -r file | 检测文件是否可读，如果是，则返回 true。 | [ -r $file ] 返回 true。 |
| -w file | 检测文件是否可写，如果是，则返回 true。 | [ -w $file ] 返回 true。 |
| -x file | 检测文件是否可执行，如果是，则返回 true。 | [ -x $file ] 返回 true。 |
| -s file | 检测文件是否为空（文件大小是否大于0），不为空返回 true。 | [ -s $file ] 返回 true。 |
| -e file | 检测文件（包括目录）是否存在，如果是，则返回 true。 | [ -e $file ] 返回 true。 |

```bash
file="/var/www/runoob/test.sh"
if [ -r $file ]
then
   echo "文件可读"
else
   echo "文件不可读"
fi
if [ -w $file ]
then
   echo "文件可写"
else
   echo "文件不可写"
fi
if [ -x $file ]
then
   echo "文件可执行"
else
   echo "文件不可执行"
fi
if [ -f $file ]
then
   echo "文件为普通文件"
else
   echo "文件为特殊文件"
fi
if [ -d $file ]
then
   echo "文件是个目录"
else
   echo "文件不是个目录"
fi
if [ -s $file ]
then
   echo "文件不为空"
else
   echo "文件为空"
fi
if [ -e $file ]
then
   echo "文件存在"
else
   echo "文件不存在"
fi
```