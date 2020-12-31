## 安装与使用

### 安装环境

https://www.python.org/



![python](https://raw.githubusercontent.com/matt17du/img/main/img/20201227192355.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201227192445.png)



1、**web-based installer、executable installer、embeddable zip file**
–**web-based installer**：在线安装。下载的是一个exe可执行程序，双击后，该程序自动下载安装文件（所以需要有网络）进行安装。
–**executable installer**：程序安装。下载的是一个exe可执行程序，双击进行安装。
–**embeddable zip file**：解压安装。下载的是一个压缩文件，解压后即表示安装完成。

2、**x86、x86-64**
–**Windows x86** ：适用32位windows操作系统。
–**Windows x86-64** ：适用64位windows操作系统。





选择对应版本点击即可2.7.17，最好选择32位的，因为它的兼容性更好

#### 配置Path

安装路径添加到path环境变量即可。

### **注意：python3.81安装的时候我们可以选择安装pip**

### 安装pip

**安装setuptools**

第一步：下载安装包（地址：https://pypi.io/packages/source/s/setuptools/setuptools-33.1.1.zip）

第二步：解压

第三步：CMD切换到该目录，切换的方法自己百度，运行命令”python setup.py install"

**安装pip**

第一步：下载pip压缩包（地址：https://pypi.org/project/pip/#files）

第二步：解压

第三步：CMD切换到该目录，运行命令”python setup.py install"



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231164305.png)

**pip环境变量配置**

这是你打开python的安装目录，发现Scripts的文件夹下就已经有了pip的文件，将此文件夹下的目录作为环境变量配置，再再在cmd下输入pip，完美完成！添加在path目录下



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231164233.png)



**检查**

在CMD输入pip,成功如下



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231164141.png)

### 安装requests

首先需要安装pip

2020.1205安装时由于挂vpn所以导致错误，之后关闭即解决问题。

```cmd
pip install requests
```

### VSCode开发python

Pyright

Python

安装以上俩个插件



### *Pycharm*

#### 如何创建一个项目

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201227233243.png)



1.设置新项目名称和存储路径（untitled可以修改）；

2.**Project Interpreter**设置新建项目所依赖的python环境；

​	2.1 **New environment using** 设置新的依赖环境。在项目中新建一个venv（virtualenv）目录，用于存放虚拟的python环境，这里所有的类库依赖都可以直接脱离系统安装的python独立运行；

​		2.1.1 勾选上**Inherit global site-packages**则可以使用base interpreter（基础解释器）中安装的第三方库（即本地Python的**site-packages目录中的类库**）；不选将和外界完全隔离（会在base interpreter的基础上创建一个新的虚拟解释器）；

​		2.1.2 勾选上**Make available to all projects**则可以将此项目的虚拟环境提供给其他项目使用；

​	2.2 **Existing Interpreter**关联已经存在的python解释器，可以使用该解释器所安装的Python库；

建议选择 **New environment using** 可以在Base Interpreter选择系统中安装的Python解释器，这样可以让项目独立部署运行，也可以避免一台服务器部署多个项目之间存在类库的版本依赖问。



### 使用python解释器

```python
python // 在终端输入即可使用


exit() // 退出
```





## 语法

### 概述

demo.py

demo:脚本名	py:脚本格式



#### 程序组成

```python
# coding:utf-8     # 脚本头

import os  # 引用部分

if __name__ == '__main__':  # 业务代码
    print('hello word ' + os.getcwd())
print('end')
```

脚本头注释：告诉解释器使用的编码格式



#### 注释



```python
# coding:utf-8

import os


'''
   这是块注释
'''

"""
    这也是块注释
"""
print(os.getcwd())
print('hello word by matt')  # 这是行注释
```

*行注释之前俩个空格*





### 变量

#### 定义

必须是数字，字母，下划线组成

任意长度，但不建议太长，20字符以内

开头必须是字母

区分大小写



一般不使用驼峰命名法使用下划线，max_age

#### 类型

##### 数字

整数

```python
age = 11  # 推荐使用这种
age = int(11)
```

浮点数

```
average = 1.1
average = float(1.1)
```

##### 字符串

```
str1 = 'hello word' 
str2 = "hello word"
str3 = str('hello word')
```

字符串使用+即可相加，使用*可以复制几次\

定义一个长的字符串

```python
（'hello'
'word'）
```

```
'''
this is good
hello hey
'''
```





find index





istitle // 用来判断字符串中的单词是否是大写开头





##### 布尔类型



```python
bool1 = True
bool1 = bool('hello')
```

##### 空类型

```python
None
```



### 关键字

*变量名用于给变量赋值使用，而关键字用于业务逻辑处理*

常见关键字

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201227205005.png)



### 运算符

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201228002007.png)





比较



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201227231419.png)



```
0-255会使用缓存
```



### 函数



#### 主函数，入口

```python
if __name__ == '__main__':
    print('hello word ' + os.getcwd())  # 主函数退出就是不在有缩进
print('end')
```

**主函数退出就是不在有缩进**（4个空格/tab）



#### 常用的内置函数

input

```
name = input("你的姓名")
print('name: %s' % (name))
```

**格式化输出**

```
print('name: %s' % (name))
```

type:判断数据的类型

```
type(age)
```

id:返回变量的内存地址

```
id(age)
```

len:返回字符串的长度

```
len(str1)
```

in 和  not in

```
'hello' in 'hello word'  # hello是否在hello word中

'hello' not in 'hello word' 
```

max:判断数据中最大的成员

```
max(list2)
```



min：判断数据中最小的成员

```
min(list1)
```





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201227201958.png)





### 常用的数据结构

#### list

列表：用来存储有序的数据的队列

```
int_list = [1, 2, 3]


int_list1 = list([1, 2, 3])
```



```
list = ['1', '2', '3']
list = list * 2
// 都会创建新的链表
```





#### tuple

元组：用来存储有序的数据的队列，相对于list,元组是不可变，list是可以改变的

```python
# coding:utf-8

tuple_1 = (1, 2, 3,)


tuple_2 = tuple((1, 2, 3, 4,))
print(tuple_1)
print(tuple_2)
```

如果元组中只有一个元素一定要添加,

```python
res = (1,)
```

#### dict

字典：用来存储key 和 value的映射

**key 支持 字符串，数字和元组类型，但列表是不支持的**
**value 支持所有python的数据类型**



```python
# coding:utf-8

dict_01 = {'name': 'matt', 'age': 12}
dict_02 = dict({'name': 'mike', 'age': 19})
print(dict_01)
print(dict_02)
```























find:找不到就会返回-1

而index则报错



### 列表和元组的操作

#### *len*():返回列表或者元组的元素个数

```python
list = [1, 2, 3]
print(len(list))  # 
```

#### *list_01* *= 2

```python
list_01 = [1, 2, 3]
print(len(list_01))

list_01 *= 2
print(list_01)  # [1, 2, 3, 1, 2, 3]
```

#### *in/ not in*  用来看元素是否在该列表中



```python
print(bool(5 in list_01))  # False
```

#### append:在原有列表的基础上添加在尾部

```python
list_02 = [1, 2, 3]
list_02.append(4)
print(list_02)  # [1, 2, 3, 4]
```

#### insert:在指定的位置插入元素，如果该位置不存在则添加在尾部,会发生数据的右移

```python
list_01 = [1, 2, 3]
list_01.insert(0, 'a')
print(list_01)  # ['a', 1, 2, 3]
```

#### count:用来查询列表或元组某个元素的个数



```python
list_01 = [1, 2, 3]
list_01.insert(0, 'a')
print(list_01)

print(list_01.count(1))  # 1
```

#### remove:用来删除某个元素，若有多个则删除第一个，若没有则报错（在原有的列表上进行删除）



```python
list_02 = [1, 2]
list_02.remove(1)
print(list_02)  # [2]
```

#### clear:对当前列表进行清空

```python
list_03 = [1, 2, 3]
list_03.clear()

print(list_03)  # []
```

#### sort:对当前列表进行排序，不支持对多种数据类型进行排序（比如一个列表中既有数字又有字母就会报错）

```python
# 不支持多种数据类型同时进行排序
list_01 = [1, 2, 3, -1]
print(list_01)
list_01.sort(reverse=True)
print(list_01)  # [3, 2, 1, -1]
```

#### copy:对当前列表进行拷贝，内存地址会发生改变

```python

list_01 = [1, 2, 3]
list_02 = list_01.copy()
list_01.append(11)
print(list_01)  # [1, 2, 3, 11]
print(list_02)  # [1, 2, 3]
```

#### deepcopy:深拷贝，对于copy复制的列表如果列表仍然有列表，则复制的列表和被复制的列表共享该列表的列表只要一个列表的一个发生改变另外一个也会发生改变

```
copy.deepcopy(list)
```

#### extend:用于在列表中添加列表

```python
list_05 = [1, 2, 3]
list_06 = ['a', 'b']
list_05.extend(list_06)
print(list_05)  # [1, 2, 3, 'a', 'b']
```

索引：数组的索引

切片：选择列表中某个位置到某个位置的元素

我们可以通过索引设置值

```python
list_07 = [1, 2, 3, 4, 5, 6]
print(list_07[0: 1])  # [1]

print(list_07[:: -1])  # 列表反转 [6, 5, 4, 3, 2, 1]

print(list_07[:: 2])  # 指定步长 [1, 3, 5]

list_07[0] = 100  
```



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201229203107.png)



pop(index) :删除指定索引的元素，如不存在则报错

del list[0] :删除指定索引的元素，如不存在则报错

```python
list_08 = [1, 2, 3, 4, 5, 6]
list_08.pop(0)
print(list_08)  # [2, 3, 4, 5, 6]
del list_08[0]
print(list_08)  # [3, 4, 5, 6]
```

字符串中的索引和切片和列表使用的相同，但是字符串无法改变

 find如果获取不到，返回-1
 index如果获取不到，直接报错

```python
list_09 = 'hello word'
print(list_09.find('1'))  # -1

print(list_09.index('hello word'))  # 0
```

