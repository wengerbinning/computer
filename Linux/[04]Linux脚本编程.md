# Linux脚本编程

[//]: # (__author__ = "Clark Aaron")

Shell是Linux的终端控制程序，是处理计算机与人之间交流的程序；而在众多的Shell中有sh、bash、csh、ksh等，bash是Linux默认的Shell。

## 文档注释

在shell编程中,通常以`#`标识注释,增强程序的可读性，在shell脚本中,通常使用`#!`来标识脚本执行的shell程序,在接下来的学习中,一般以bash为默认shell，例如`#!/bin/bash`。

* 指定默认执行的shell程序：

  ```shell
  #!/bin/bash
  ```

* 单行注释：

  ```shell
  # 这是单行注释的方法。
  ```

* 多行注释：

  ```bash
  :<<!
  多行注释,其中!可以是其他字符,例如EOF,?等.
  !
  ```

## 数据对象

在shell脚本中变量只能存储字符类型的数据，且赋值符号左右不留空格。变量值在单引号中的变量不会被变量值所替代，只会原样输出；只有在双引号中的变量与转义字符才会被替换；在赋值时，可以使用反引号\`<command\>\`或`$(<command>)`将指令的返回内容赋值给变量。

* 变量赋值

  ```bash
  <variblename>=<stringvalue>     # 变量赋值的一般格式
  <var>=`<command>`              # 命令返回值的赋值格式
  <variblename1>=$<variblename2>  # 变量间的相互赋值

  # 定义数组,仅支持一维数组
  <groupname>=(<value0>,<value1>, ... )

  <groupname1>=(
      value0
      value1
      ...
  )
  # 可以不使用连续下标,且下标无限制
  <groupname>[0]=<value0>
  <groupname>[n]=<valuen>
  ```

* 引用变量

  ```bash
  echo $<variblename>                                         # 输出变量值
  echo Varible=$<variablename>                                # 在字符串中嵌入变量值
  echo ${<variablename>[:<start_index>:<count>]}content       # 为避免混淆,使用${}标识变量,同时也可以对变量值进行切片,索引从0开始
  echo "Variable = $<variablename>"                           # 打印带空格的字符串,变量被替换
  echo 'Variable = $<variablename>'                           # 打印带空格的字符串,变量被当作普通文本
  echo ${#variablename}                                       # 获取字符串的长度
  echo ${<groupname>[<index>]}                                # 显示数组元素
  echo ${<groupname>[@]}                                      # 显示所有元素
  echo ${#<groupname>[@]}                                     # 获取数组长度
  echo ${#<groupname>[*]}                                     # 获取数组长度
  ```

* 变量的属性

  ```bash
  # 限定变量为只读变量
  readonly <variable_name>
  ```

* 删除变量

  ```bash
  unset <variable_name>
  ```

* 变量类型：在shell中存在三种变量:局部变量(当前shell实例中有效),环境变量(所有程序都能访问),shell变量(shell程序设定的特殊变量).

## 数据管理

### 数据输入

* 数据的输入: 在bash中只能输入字符

```bash
read <variablename>     # 读入文本并赋值给变量
```

### 数据输出

* 数据的输出: 输出文本到屏幕

```bash
# echo 输出字符
echo string         # 输出字符串
# 不换行显示,默认换行显示,-e开启转义
echo -e "string \c"

# printf 输出字符
printf "%10s %20s\n" "Name:" $name # 格式化输出,第一个参数为格式化字符串 之后依次为格式化参数
```

`printf`的转义字符与格式化字符: 转义字符只在格式化字符串中被解释,在格式化字符串,在%之后首先是属性{-(左对齐,默认右对齐),+(显示符号),#,0(以零填补)},然后是精度值,之后是格式化字符,例如`%-50s`表示固定50个字符长度,左对齐.

| 字符 | 说明 | 字符 | 说明 |
|:----:|:--- |:----:|:--- |
| \a | 警告字符 | %c | ASCII字符,显示参数的的第一个字符 |
| \b | 后退 | %d or %i | 十进制数 |
| \c | *禁止换行符 | %e or %E | 浮点数 |
| \f | 换页 | %f | 小数形式 |
| \n | 换行 | %g or %G | 自动选择小数形式 |
| \r | 回车 | %s | 字符串 |
| \t | 水平制表符 | %u | 无符号十进制数 |
| \v | 垂直制表符 | %x or %X | 无符号十六进制 |
| \\ | \符号 | %% | %符号 |

## 数学运算

在bash中,数字于运算符都会被当作普通文本,不能便捷的进行数学运算;但可以通过$(())语法来进行数值运算,运算符有{`+`,`-`,`*`,`/`,`%`,`**`,`=`};其优先级从高到低是乘方,乘除取余,加减;同一优先级按从左至右的顺序执行.

```bash
reasult=1+2                # 不会计算值,原样赋值
echo $reasult              # 原样打印
echo $((1+2*3/$reasult))   # 计算后打印结果
reasult=$((1+2**3))        # 运算后赋值

# 算数运算符 + - * / % ** = != == 用于数值运算
# 关系运算符 -eq -ne -gt -lt -ge -le 用于数值关系
# 逻辑运算符 !(非) -a or &&(与) -o or ||(或)
# 字符串运算符 = != -z -n $
# 文件检测运算符 -b -c -d -f -g -k -p -u -r -w -x -s -e -S -L
# 使用expr(表达式计算工具)
```

### 返回代码

在linux中,每个可执行程序会有一个整数的返回代码,在bash可以通过`$?`获取返回代码.在linux中可以使用`;`来在一行区别多条语句.

```bash
gcc foo.c      # 编译 fooc.c文件
./a.out        # 执行a.out程序
echo $?        # 打印a.out的返回代码
cd /; ls       # 多语句执行
rm demo.file && echo "rm succeed"  #在第一条语句返回代码为0(执行成功时),执行第二条语句
rm demo.file || echo "rm fail" #在第一条语句返回代码非0(执行失败时),执行第二条语句
```

### shell脚本

多行的bash命令写入一个文件即为bash脚本文件,执行时逐行执行,一般使用`.sh`或`.bash`来标识脚本文件,其目的达到代码复用.

* 脚本举例: 第一行说明该脚本使用的shell

```bash
#!/bin/bash         # 指定脚本执行shell
echo Hello
echo World
```

* 脚本参数: 脚本运行时,可以携带参数,使用`$<number>`获取参数值;

```bash
#!/bin/bash

echo $0         # 命令
echo $1         # 第一个参数

# $# 参数个数
# $* 所有参数
# $$ 脚本当前PID
# $! 后台运行的最后一个进程的PID
# $@ 所有参数
# $- 显示shell使用的当前选项
# $? 程序的返回代码
```

* 脚本的返回代码: 正常退出时自动返回0,也可以使用`exit <number>`指定返回代码;脚本在遇到`exit`指令会立即退出;

```bash
#!/bin/bash

lscpu >> $1

exit 0
```

### 函数

函数实现了脚本内部的代码重用.

* 函数定义: 使用function与{}来定义函数,其中function关键字可以去掉;

```bash
# 函数定义
function func()
{
    lscpu
}

func     # 函数调用
```

* 函数的参数: 函数也可使用参数,同样使用`$<number>`指定参数;

```bash
#!/bin/bash

function func()
{
    lscpu >> $1
}

func demo.log # 指定参数
```

* 脚本件的函数调用: 使用`source`命令实现函数在脚本间的调用;

```bash
# demo1.bash
#!/bin/bash

function func()
{
    lscpu >> $1
}

# demo2.bash
#!/bin/bash

source demo1.bash   # 加载脚本
func demo.log       # 脚本间的参数调用

```

### 程序结构

程序默认以顺序执行;

* 逻辑判断: 使用`test`命令来进行逻辑判断,{`-gt`,`-lt`,`-eq`,`-ne`,`-ge`,`-le`}分别表示大于,小于,等于,不等于,不小于,不大于,用于数值测试;

```bash
# 数值判断
    test 3 -gt 2; echo $?   # 3大于2成立时,返回代码为0;显示返回代码
    test 3 -lt 2; echo $?   # 3小于2不成立,返回代码为1;显示返回代码

# 字符串判断
    # 文本相同
    test abc=abx; echo $?
    # 文本不同
    test abc!=abx; echo $?
    test apple>tea; each $?     # 根据词典顺序,文本在另一文本之前
    test apple<tea; echo $?     # 根据词典顺序,文本在另一文本之后
    test -z <string>; echo $?   # 字符串长度为零时为真
    test -n <string>; echo $?   # 字符串长度不为零为真

# 文件状态判断
    # 文件是否存在
    test -e demo; echo $?
    # 普通文件是否存在
    test -f demo; echo $?
    # 目录文件是否存在
    test -d demo; echo $?
    # 软连接文件是否存在
    test -L demo; echo $?
    # 文件是否可读
    test -r demo; echo $?
    # 文件是否可写
    test -r demo; echo $?
    # 文件是否可执行
    test -x demo; echo $?
    # 文件存在且不为空
    test -s demo; echo $?
    # 字符特殊文件是否存在
    test -c demo; echo $?
    # 块特殊文件是否存在
    test -b demo; echo $?

# 逻辑组合
    !<expression>                  # 非
    <expression1> -a <expression2> # 与
    <expression1> -o <expression2> # 或

# if 条件语句,经常与test语句连用
    if [<expression>]
    then        # if的隶属代码,条件为真时执行
        echo content
    fi
# if-else 条件语句,可以使用if嵌套实现多分枝结构
    if [ -e $filename ]
    then
        echo "$filename is exists."
    else
        echo "$filename is not exists."
    fi
# if-elif-else 条件语句
    if [ <expression> ]
    then
        echo <content>
    elif [ <expression> ]
    then
        echo <content>
    else
        echo <content>
    fi
# case语句实现多程序执行,可以使用文本通配符,*表示任意文本,a?b表示a与b任意一个字符,[a-z]表示a-z之间的一个字符
    case $var in
    root)
        lscpu
        echo "you are $var"
    ;;
    vamei)
        echo "you are $var"
    ;;
    *)
        echo "you are the others"
    ;;
    esac
```

* 循环结构: 重复执行某段代码;

```bash
#!/bin/bash

now=`date+'%Y%m%d%H%M'`
deadline=`date --date='1 hour'+'%Y%m%d%H%M'`
# while 循环语句
while [$now -lt $deadline]
do  # while 隶属代码
    date
    echo "not yet"
    sleep 10
    now=`date+'%Y%m%d%H%M'
done
#for 循环语句: 执行'ls log*'语句,并以空格分割,之后依次赋值给var,并执行for隶属代码
for var in `ls log*`
do  #for 隶属代码
    rm $var
done
# 构建空格分割文本

for var in root user clark
do
    echo $var
done
for ((i=1;i<=5;i++))
do
    each $i
done
# seq生成等差数列
seq 1 2 10   # 第一个参数为起始,第二个参数为步长,第三个参数为终止
let 'index++'   # 标识index自增一个单位

for var1 in `seq 1 2 10`
do
 echo $var1
done
# break 可以跳出当前循环结构,continue跳出本次循环

# 无线循环
while :   # 等价于 while true
do
    <content>
done

for (( ; ; ))

# until 循环语句

until [ <condition> ]
do
    <content>
done
```

### 输出/输入重定向

一般情况,标准输出/输入都是以终端为对象,重定向是以其他作为对象;一般在Linux中 执行命令时会打开标准输入文件(stdin,文件描述符为0)、标准输出文件(stdout,文件描述符为1)、标准错误文件(stderr,文件描述符为2).

```bash
# 重定向输出至文件,将stdout重定向到file中
<command> > <filename>      # 直接覆盖文件
<command> >> <filename>     # 追加在文件末尾
<command> > <filename> 2>&1       # 将stderr与stdout合并输出到file
# 重定向输入至文件,将stdin重定向到file中
<command> < <filename>
<command> < <filename> 2<&1        # 将stderr与stdout合并输入
"dwdwd << <tag> <content> <tag>"                      # 将tag之间的内容作为输入
# 将文件描述符为n重定向到file,将stderr重定向到file
<command> <number> > <filename>     # 覆盖的方式
<command> <number> >> <filename>    # 追加的方式
```

如果执行命令后不想输出结果,则可以将输出重定向到`/dev/null`中,`/dev/null`中的内容都会被丢弃.

### 文件的包含

文件的包含用于在一个文件中使用另一个文件代码内容,通常以`. <shellfilename>`(顿号与文件之间的空格不可省略)或`source <shellfile>`来包含.

```bash

. ./bashfile

source bashfile
```
