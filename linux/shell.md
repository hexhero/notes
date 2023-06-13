# Shell

## 数组

array_name=(value1 value2 ... valuen)

${array_name[0]}

array_name[0]=value0

## 循环

### while 

```sh
int=1
while(( $int<=5 ))
do
    echo $int
    let "int++"
done    
```

### case ... esac

```sh
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

## 运算

val=`expr 2 + 2`


### 跳出循环
continue/break

## let 

Bash let 命令，它用于执行一个或多个表达式，变量计算中不需要加上 $ 来表示变量

## read

读取键盘输入

## 函数

```sh
#!/bin/bash

funWithParam(){
    echo "第一个参数为 $1 !"
    echo "第二个参数为 $2 !"
    echo "第十个参数为 $10 !"
    echo "第十个参数为 ${10} !"
    echo "第十一个参数为 ${11} !"
    echo "参数总数有 $# 个!"
    echo "作为一个字符串输出所有参数 $* !"
}
funWithParam 1 2 3 4 5 6 7 8 9 34 73
```

