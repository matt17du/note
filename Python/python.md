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





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210116165559.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210116165657.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210116165732.png)





**下图不要选择all user**

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210116175019.png)



**选择对应版本点击即可2.7.17，最好选择32位的，因为它的兼容性更好**

#### 配置Path

安装路径添加到path环境变量即可。在3.7可以在安装时选择配置path

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

字符串使用+即可相加，使用*可以复制几次

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



##### 布尔类型



```python
bool1 = True
bool1 = bool('hello')
```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210111233719.png)





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

input:从键盘输入

```
name = input("你的姓名")
print('name: %s' % (name))
```

格式化输出

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

is :判断俩个对象内存地址是否相等

```
print(str is str_1)
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



set:

{}:只可以传入不可变的类型，set{[1,2,3]} 错误的





dir(b):可以查看b的所有函数方法





### 字符串



```python
str1.capitalize() # 字符串首字母大写
str1.lower() # 字符串小写
str1.upper() # 字符串大写
str1.swapcase() # 字符串大小写转换
str2.zfill(10) # 左边用0填充

str2.count('h') # 返回字符串成员的个数
print(str2.startswith('he')) # str2是否是‘he’开头
print(str2.endswith('he')) # str2是否以‘he’结尾
```

find 和 index 查找成员开始的位置

区别：find找不到返回-1,而index会报错


```python
print(str2.find('hell'))
print(str2.index('hell'))
```

strip去除字符串首尾指定的成员默认是空格

```python
str3 = ' hello '
print(str3.strip())

print(str3.strip('h')) # hellhoh -> ellho
```

replace():字符串替换

```
str4 = 'hello'
print(str4.replace('e', 'a', 3)) # old,new,次数：默认是全部替换
```

```python
str_1 = ' '
print(str_1.isspace()) # 判断字符串是否有空格组成
str_1 = 'hello'
print(str_1.istitle())  # 判断字符串是标题，即单词首字母大写

print(str_1.isupper()) # 判断字符串是否全部大写
print(str_1.islower()) # 判断字符串是否全部小写
```







字符串格式化

```python
str1 = 'hello word'
# 1
print('%s python' % (str1))

# 2
print(f'hello {str1}')

# 3
print('abc{}'.format('ag'))

print('hello {0} -{1}-{0}'.format(1,2))
print('hello {name}'.format(name='age'))
print('hello num {:10.2f}'.format(3.134343))
print('{:d}'.format(34))

print('hello %30.e' % (10000000))
```



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210109003738.png)

```python
%d # 十进制
%b # 二进制
%o # 八进制
%x # 十六进制
```

转义字符

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210112002623.png)





### 列表 list

len:判断列表中元素的个数

```python
str = 'hello'
list1= [1, 3, 3]
print(len(list1)) # 3
```

in :判断某个元素是否在该列表中，或者判断任何数据类型的长度,而not in 功能刚好相反

```python
str = 'hello'
list_1= [1, 3, 3]
print(len(list_1))

print(1 in list_1)
```

append():列表添加元素

```python
list_1.append('5')
print(list_1) # [1, 3, 3, '5']
```

insert:列表中指定位置添加元素

```python
list_1 = [1, 2, 3]
list_1.insert(0, 'a')
print(list_1) # ['a', 1, 2, 3]
```

count:在列表中统计某个元素出现的次数

```python
print(list_1.count(1)) # 1
```

remove:删除列表中的元素，如果不存在则报错，如果有多个则删除第一个

```python
list_1.remove(1)
print(list_1)
```

del:将变量完全删除，在使用就会报错

```python
del list_1
print(list_1) # 直接报错
```

reverse():列表的元素进行反转

```python
list_1 = list([1, 2, 3])
list_1.reverse()
print(list_1) # [3, 2, 1]
```

sort():排序,reverse=False(默认)升序，如果True则降序，key=根据什么进行排序，

成员必须是同一数据类型，否则无法进行排序

```python
list_1.sort(reverse=False) # key= reverse=
print(list_1) # [1, 2, 3]
```

clear():列表清空



```python
list_1.clear()
print(list_1) # []
```



copy和deepcopy都是列表拷贝一份

如果列表还有列表使用copy则它们会共享一个列表，而deepcopy会重新开辟一个列表

```python
print('copy')
list_1 = [1, 2, 3]
list_2 = list_1.copy()
list_1.append('a')
print(list_1,list_2) # [1, 2, 3, 'a'] [1, 2, 3]
print(list_1 is list_2)

print('deepcopy----')
list_1 = [[1,2],[3,4]]
list_2 = copy.deepcopy(list_1)
list_2[1].append('a')
print(list_1, list_2)
```

extend:列表中添加列表

```python
print('extend')
list_1 = [1, 2, 3]
list_2 = ['a', 'b']
list_1.extend(list_2)
print(list_1) # [1, 2, 3, 'a', 'b']
```



索引：第一个元素是0

切片：比如字符串的截取，左含右不含



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201229203107.png)



pop():根据索引获删除值

```
list_1 = list([1, 2, 3])
list_1.pop(1)
print(list_1)
```

[]:根据索引获取值

也可以修改值，不过字符串无法修改

```python
del list_1[0]
print(list_1)
```

### set 集合的使用



集合的创建

```python
set_1 = {1, 2, 3} # 1
print(type(set_1)) 
set_1 = set() # 2 set([2, 3, 3])
# {}：不可以使用
```

add:添加一个元素

update:添加一个集合，如果元素已经在集合中则忽略该元素

remove:移除一个元素

clear:清空集合



```python
# coding:utf-8

set_1 = set((1, 2, 3, 4))
print(set_1)

set_1.add('helo') # {1, 2, 3, 4, 'helo'}
print(set_1) #

set_1.update([1, 3, 3, 'matt']) # 如果元素已经在集合中则忽略该元素
print(set_1) # {1, 2, 3, 4, 'matt', 'helo'}

set_1.remove('matt')
print('remove', set_1) # remove {1, 2, 3, 4, 'helo'}


set_1.clear()
print(set_1)

# del set_1
print(set_1)
```

difference:差集

intersection：交集

union：并集

isdisjoint：判断俩个集合中是否有交集

```python

# coding:utf-8

set_1 = {1, 2, 3, 4}
set_2 = {1, 2, 'a', 'b'}
diff = set_1.difference(set_2) # 也可以使用-
print(diff)

# print(set_1 - set_2)

intersection_res = set_1.intersection(set_2)
print('交集', intersection_res)

union_res = set_1.union(set_2)
print('union_res', union_res)

isdisjoint_res = set_1.isdisjoint(set_2) # 判断俩个集合是否包含相同的元素，没有则True
print(isdisjoint_res)
```





### 字典使用

定义

```python
dict_01 = {'name': 'matt', 'age': 12}
dict_02 = dict({'name': 'mike', 'age': 19})
```

[] 和 update()

[]:口号内填一个key,

update()中需要添加一个已经定义好的字典，并不会会已有的字典进行覆盖除其中俩个字典相同的key会进行覆盖

```python
dict['age'] = 11
dict_1 = {'name': 'matt'}
dict.update(dict_1) # {'age': 11, 'name': 'matt'}
```

setdefault:key不存在才会设置

```python
dict.setdefault('a', 1)
dict.setdefault('name', 1)
print(dict)
```



keys 和 values

keys:获取字典中所有的key

values:获取字典中所有的值

二者返回的都是伪列表，不具有列表的所有功能

```python
print(dict.keys())
print('values:', dict.values())
```



[] 和 get

二者用于字典根据key获取属性的值，

[]:当key不存在就会报错而get没有此缺陷

```python
print(dict['a'])
print(dict.get('v'))
```

clear:清空字典

```python
dict.clear()
```

pop():根据key删除值，若key不存在则报错

```python
dict.pop('a')
```

del使用

```python

del dict['b'] # 删除key魏'b'
del dict # 在内存中删除字典，在使用则报错
print(dict)
```

copy:字典的复制，内存地址会发生改变

```
dict_01 = dict.copy()
print(id(dict) == id(dict_01))
print(dict_01 is dict)
```

in 和 not in

```python
dict = {'a': 1, 'b': 2}
print('a' not in dict)
```

popitem():删除字典末尾的key-value,字典为空直接报错

```python
res = dict.popitem() # 字典为空直接报错
```

​                                                

类与类之间2个空行





### 流程控制

if

```python
# coding:utf-8

i  = 1
if i < 10:
    print('个位数')
elif i >= 10 and i < 100:
    print('十位数')
else:
    print('其他')
```

for

```python
# coding:utf-8

list_0 = [1, 2, 3, 4]
for i in list_0:
    print(i)

dict_0 = {'name': 'matt', 'age': 10}
for i in dict_0.values():
    print(i)
```

while

```python
# coding:utf-8

count = 100
while count > 0:
    count -= 1
    print(count)
print('end')
```

### 函数的使用

```python
# coding:utf-8

​```
a：必须要传，b有默认值可以不传
​```
def incr(a, b = 1): 
    return a + 1

sum = incr(a = 1)
print(sum)

# 可变参数，其中args封装为元组，而kwargs封装为字典
def test(*args, **kwargs):
    print('hello word')
    print(args)
    print(kwargs)
test(1, 2, 3,name = 'age', age = 17)
# (1, 2, 3)
# {'name': 'age', 'age': 17}
```

函数中使用类型

```python

# python不会对参数类型进行验证
def test(i:int, j:str = 'hello word'):
    print(i)
```

lambda使用

```python
f = lambda : print('test lambda')
f()

t = lambda x, y : x + y
print(t(1, 2))
print('hello' + '11')
```

### 类与对象

```python
# coding:utf-8

class Person(object):
    name = 'matt'
    __sex = '女'
	# 构造函数，self代表当前对象
    def __init__(self):
        print(self)
        self.age = 17

    def __init__(self, name):
        print('hello word')

person = Person('11')
print(person.name)
# print(person.sex)
```

装饰器的使用

```python
def a(f):
    def inter(*args, **kwargs):
        return f(*args, **kwargs)
    return inter

@a
def test(i):
    print(i)

test(1)
```

```python
class T(object):

    __name = 'matt'
	
    # 直接可以使用类调用
    @classmethod
    def a(cls, t):
        print(t)
 	# 直接可以使用类调用，不需要使用cls,self
    @staticmethod
    def b():
        print('staticmethod')

    # 可以使用对象.name
    @property
    def name(self):
        return self.__name

T.a('11')
T.b()

t = T()
print(t.name)

```

多继承

```python
# coding:utf-8

class A(object):

    def info(self):
        print('a')


class B(object):

    def info(self):
        print('b')

class C(B, A):

    def test(self):
        super(C, self).info()
        print('test')

c = C()
c.test()
```

super: super(当前类，self).父类的属性或者方法



```python
# coding:utf-8

class Parent(object):

    def __init__(self, name):
        self.name = name

    def info(self,name):
        print(name)

p = Parent('p')
p.info('aaa')

class Son(Parent):
    
    def __init__(self):
        super(Son, self).__init__('aaa')

    def test(self):
        super(Son, self).info('hello word')

s = Son()
s.test()
```

类的高级函数

```python
# coding:utf-8

class Person(object):

    # 类的描述信息,相当于toString()方法
    def __str__(self):
        print('this is person')
        return '1'
	
    # 在key不存在时会触发这个函数
    def __getattr__(self, item):
        print('%s 不存在' % (item))

    # 在属性不存在设置时触发这个函数
    def __setattr__(self, key, value):
        if key not in self.__dict__:
            return

    # 对象(参数)
    def __call__(self, *args, **kwargs):
        print(*args)


person = Person()
print(person.a)
print(person)

person.age = 18
print(person.age)

person(12222)

print(person.__dict__)
```







### 包与模块

```
包：一个文件夹，这个文件夹中有__init__.py和其他python文件，其中__init__.py是包的身份证，其他py文件是模块，包中也可以有包
```



导入包

```python
import animal.dog
```



导入模块

```python
from animal.dog import aciton

action.jump()
```

导入模块中的函数

```python
from animal.dog.action import run as dog_run # as是起别名

dog_run()
```



pop使用

```python
pip install 包名

pip uninstall 包名

pip -V
```





使用 python 不要使用代理 



```
ipython 7.2.0版本升级，导致自动补全（auto complete）功能出现异常，pip install ipython==7.1.1安装指定版本即可。
```

### end

```python
person.__dict__ # 返回它的所有属性
```





join,split



```python
print '------'


str_1 = ' '
list_1 = [1, 2, 3]
print str_1.join(['a', 'b', 'c']) # a b c
```

eval

chr

ord



### 加密

#### hashlib:不可逆

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210117214443.png)





```python
hashobj = hashlib.md5(b’hello’)
result = hashobj. hexdigest() # 生成16进制字符串
print(result)
```



base64：可解密，需要自己导入base64模块

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210117214629.png)





```python
 coding:utf-8
import hashlib
import base64

res = hashlib.md5(b'hehllo ')
print(res.hexdigest()) # 返回16进制字符串的值
str = '中国人'
res = str.encode(encoding='utf-8')
print(res.decode(encoding='utf-8'))

print(base64.encodebytes(str.encode(encoding='utf-8')))
```



### 日志 logging

日志的等级

debug
info
warnning
error
critical

日志的使用

```python

# coding:utf-8

import logging


logging.basicConfig(
        level=logging.INFO,
        format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
        filename='my.log',
        filemode='w'
    )

logging.info('hello word')
```






​	

| logging.basicConfig |                                 |
| ------------------- | ------------------------------- |
| level               | 日志输出等级level=logging.DEBUG |
| filename            | 存储位置filename=‘d://back.log’ |
| format              | 日志输出格式                    |
| filemode            | 输入模式filemode='w'            |


​	
​	




| format具体格式 | 格式符含义     |
| :------------- | :------------- |
| %(levelname)s  | 日志级别名称   |
| %(pathname)s   | 执行程序的路径 |
| %(filename)s   | 执行程序名     |
| %(lineno)d     | 日志的当前行号 |
| %(asctime)s    | 打印日志的时间 |
| %(message)s    | 日志信息       |



### 常用的内置函数



abs

all any type isinstance help var dir hasattr

input

enumerate



```python
# coding:utf-8

print(abs(-100)) # 返回正数

print(all([1, 1, 1])) # 判断列表内容是否全是true

class User(object):

    def __init__(self):
        print('创建User对象')

user = User()
print(help(user)) # help 打印对象的全部用法

name = input('请输入姓名：')
print(name)

list_1 = [1, 3, 3]
for index,i in enumerate(list_1): # 记录索引
    print(index, i)

print(isinstance(1, int)) # 判断某个变量是否是某个类型

print(type('hello word'))
user.name = 'hello'
print(vars(user)) # 返回对象实例化字典信息
print(dir(user)) # 返回对象的所有属性和方法

print(hasattr('hello', 'aaa')) # 判断对象是否有某个属性

user.__setattr__('age', 10)
print(user.__getattribute__('age'))

list_1 = [1, 2, 3]
print(any((None,))) # 判断对象中是否有true值
```



### random 模块

```python
# coding:utf-8

import random
# 右边不可以取到
def test():
    for i in range(10000):
        i = random.random() # 返回0-1的浮点数
        if i == 1:
            print(i)
            return i;
    print('没有1')

test()

print(random.uniform(1, 2)) # 返回范围的浮点数
def test_uniform():
    for i in range(10000):
        i = random.uniform(1, 2)
        if i == 1:
            print(i)
            return i;
test_uniform()

print('randint')
print(random.randint(1, 1000)) # 返回整数

print('choice', random.choice([1, 2, 3, 4, 5])) # 返回list中的一个值

print('sample', random.sample([1, 2, 3, 4, 5],2))# 返回list中的几个值

# 步长
for i in range(10):
    print(random.randrange(1, 100, 100)) # 返回指定的一个值，可以指定步长


```

### 迭代器

```python

# coding:utf-8

iter_obj = iter([1, 2, 3])
print(iter_obj.__next__())

iter_obj = (i for i in range(10))
print(iter_obj.__next__())

def get_iter_obj():
    for i in range(13):
        yield i
iter_obj = get_iter_obj()
print(iter_obj.__next__())
```

### 高级函数

```python
# coding:utf-8

from functools import reduce


def _filter(x):
    if x <= 0:
        return False;
    return True;

res = list(filter(lambda x: x > 0, [-1, 2, 3]))
print(res)

res = list(map(_filter, [-1, -2, 100])) # 返回True False list
print('map', res)

print('----reduce----')
res = reduce(lambda x, y: x + y, (1, 2, 3)) # 需要导入reduce
print(res)
```





### 正则表达式



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210116002023.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210116002110.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210116002139.png)



几个常用的函数

使用前首先需要导入re

```python
import re
```



findall:将得到的字符串存在list中

```python
str = 'my name is hash'
res = re.findall('\sis*', str) # 返回符合的list [' is']
print(res)
```

match:必须从字符串开始查找



```python
str = 'hedd '
print(re.match('\w*', str).group()) # 从开始字符开始查找
```

split:根据匹配得到的字符串进行分割

```python
str = 'my name is hello word'
res = re.split('\s+', str) # 找到的就是空格符号
print(res) # ['my', 'name', 'is', 'hello', 'word']
```

search:只可以匹配一次

```python

str = 'my email is 1718905040@qq.com 171890@qq.com'
res = re.search('(\d*.qq.com)', str) # 只会查找一次
print(res.groups())
print(res.group(1)) # 索引从1开始
```

compile:得到一个可以使用以上函数的对象

```python
str = 'my email is 1718905040@qq.com 1234343@qq.com'
re_obj = re.compile('\d+.\w{2}.com')
res = re_obj.findall(str)
print(res)
```





