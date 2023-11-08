### 1. input 函数

```python
name = input('请输入你的名字')               #括号字符串内为提示信息
```

注意：input() 的返回类型一定是 str 字符串类型



### 2.命令行接受参数

#### （1）通过外部传入参数

程序代码（程序名称为 test.py ）

```python
from sys import argv                  #argv是“参数变量”

script, first, second, third = argv

print("the script is called:", script)
print("Your first variable is:", first)
print("Your second variable is:", second)
print("Your third variable is:", third)

```

命令行输入

```shell
python test.py 12 23 34
```

输出

```shell
The script is called: test.py
Your first variable is: 12
Your second variable is: 23
Your third variable is: 34

#第一个参数就是程序本身
```



#### （2）原理

 sys.argv[] 在运行python文件的时候从外部输入参数，往文件内传递参数。

从外部取得多个参数，获得一个列表，第一个参数是程序本身，随后依次是外部参数



### 3.文件操作

#### （1）读取文件

目录中一个 test.py 和一个 sample.txt

```python
file = open(sample)            #open()根据文件名sample创造了一个file对象
print file.read()              #使用方法read()即返回整个txt
```

#### （2）读写文件

```python
file = open(sample, 'w')
file.write('string')            #使用方法write()将string写入文件中
```



### 4.帮助文档

```python
def add(a, b):
    """add a and b ,then return sum"""        #定义函数时放在"""之间的，即是帮助文档
    
	print "ADDING %d + %d" % (a, b)
    return a + b

```

当执行

```shell
help(test.add)
```

会显示

```shell
add a and b ,then return sum
```



### 5. import 与 from ... import 

- import：导入一个模块（相当于导入的是一个文件夹，是个相对路径）
- from ... import ：导入了一个模块中的一个函数（相当于导入的是一个文件夹中的文件，是个绝对路径。）

当引用文件时

```python
import os

os.environ()       #模块.函数

-------------------------------------

from os import environ

environ()          #直接使用函数名
```

总结：

- import 导入模块，每次使用模块中的函数都要制定是哪个模块
- from ... import * 导入模块中的所有函数，每次使用模块中的函数，直接使用即可，因为已经注明



### 6.range函数

 range() 会创建一个整数列表，一般用在 for 循环中。

```python
range(start,stop,step)
```

- start ： 计数从start开始，默认为0。
- stop ： 计数到stop结束，**但不包括stop**。例如，range (5) ： [0,1,2,3,4]
- step ： 步长，默认为1。

#### 实例

```python
>>> range(0,30,5)            #起始为0，终点为30，步长为5
[0,5,10,15,20,25]
```

