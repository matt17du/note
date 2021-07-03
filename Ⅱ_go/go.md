## 第一章  使用

### 1.1安装

[下载地址](https://golang.org/dl/)

win10/64-》选择x86-64    



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210420150359.png)



选择go1.13.15.windows-amd64.msi一直下一步安装即可，更改安装路径即可，安装完成后它已经配置了环境变量；

或者选择go1.13.15.windows-amd64.zip解压缩，配置环境变量；





### 1.2配置



GOROOT:指定go的安装目录

path:指定go的安装目录下的bin目录

GOPATH:工作目录，go项目的工作目录



GOROOT

```
D:\develop\env\go
```

path

```
%GOROOT%\bin
```

GOPATH

```
D:\matt\workspace\go
```





设置国内镜像

```go
go env -w GOPROXY=https://goproxy.cn,direct
```

go的依赖管理

```go
go env -w GO111MODULE=on
```

验证配置,可能验证的默认网站无法访问 [sum.golang.org](sum.golang.org)

```bash
go env -w GOSUMDB="sum.golang.google.cn"
```

或者关闭验证

```bash
go env -w GOSUMDB=off
```



### 1.3验证

验证go环境是否安装成功

```bash
go version
```

格式化代码

```
gofmt -w main.go
```



### 1.4资料

[中文API](https://studygolang.com/pkgdoc)

[官网](https://golang.org/)

## 第二章  Hello Word

### 2.1程序

新建项目

项目下创建src文件夹，创建bin文件夹，创建pkg文件夹

```go
package main

import "fmt"

func main() {
	fmt.Println("hello word")
}
```

### 2.2编译运行

#### 1.编译运行分开

编译

```bash
go build hello.go
```

运行

```bash
hello.exe
```

#### 2.编译运行不分开

```bash
go run hello.go
```

#### 分开和不分开区别

1) 如果我们先编译生成了可执行文件，那么我们可以将该可执行文件拷贝到没有 go 开发环境的机器上，仍然可以运行 

2) 如果我们是直接 go run go 源代码，那么如果要在另外一个机器上这么运行，也需要 go 开发环境，否则无法执行。 

3) 在编译时，编译器会将程序运行依赖的库文件包含在可执行文件中，所以，可执行文件变大了很多。



### 2.3注意事项

go源文件以 go 为扩展名

go 的入口函数是 main() 函数

go 严格区分大小写

go 语句不需要加分号，go语言自动会加分号

go语句是一行一行编译，所以一行不可以写多条语句

引用的包或者定义的变量必须使用，不使用会报错



### 2.4注释



```go
package main

import "fmt"
import "time"

func main() {
	// 行注释，推荐使用行注释
	/*
	  块注释
	  你好块注释
	*/
	fmt.Println(time.Now())
}

```

## 第三章  变量

### 3.1转义字符



```bash
1) \t : 表示一个制表符，通常使用它可以排版。

2) \n ：换行符 

3) \\ ：一个\ 

4) \\" ：一个"

5) \r ：一个回车
	fmt.Println("aaa\r bb");
```

### 3.2变量声明

指定变量类型，

整数：0

浮点数：0

bool:false

```go
// 如果不赋值，则使用它的默认值
var j int
```

不指定类型，自己判断

```go
var i = 100
var j
```

第三种,省略var

```go
// i没有声明过
i := 100
```

多变量声明

```go
var a, b, c int
fmt.Println(a, b, c)

var d, e, f = 1, 2, 3
fmt.Println(d, e, f)

g, h := "1", "2"
fmt.Println(g, h)
```

全局变量

```go

// 全局变量
var a1 = 100
var a2 = 200
// 推荐使用
var (
	a3 = 300
	a4 = 400
)
```

**变量的值只可以在同一种类型变化**



## 第四章  数据类型

### 4.1基本数据类型



#### 整数

有符号

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210521005142.png)



无符号

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210521005217.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210521005400.png)

```go
package main

// import "fmt"
// import "unsafe"
import (
	"fmt"
	"unsafe"
)

func main() {
	var i int = 100
	fmt.Println(i, unsafe.Sizeof(i))
}
```



#### 浮点数

系统默认使用float64,推荐使用float64

| 类型    | 占用存储大小 | 范围              |
| ------- | ------------ | ----------------- |
| float32 | 4            | -3.4E38～3.4E38   |
| float64 | 8            | -1.7E308～1.7E308 |



```go
package main

import (
	"fmt"
)

func main() {
	var i float64 = 1.1
	fmt.Println("浮点数", i)
}
```



#### 字符

使用'',字符有一个码值

```go
package main

import "fmt"

func main() {
	var i byte = '1'
	fmt.Println(i)
	fmt.Printf("%c\n", i)
	// %d %s %c
	// 如果一个字符超过byte表示的类型，使用int类型即可
	var j int = '中'
	fmt.Printf("%c", j)
}
```

字符

存储到 计算机中，需要将字符对应的码值（整数）找出来 

存储：字符--->对应码值---->二进制-->存储 

读取：二进制----> 码值 ----> 字符 --> 读取

​	





#### bool



```go
package main

import (
	"fmt"
	"unsafe"
)

func main() {
	var i bool = false
	fmt.Println(i, unsafe.Sizeof(i))
}
```



#### string



```go
package main

import "fmt"

func main() {
	var name string = "matt"
	var address = `
		hahahninrerer
	`
	fmt.Println(name)
	fmt.Println(address)
    // 多行输出
	fmt.Println("hello word",
		"你好")
}
```

一般使用"",也可以输出反引号``

反引号可以赋值多行





字符串拼接

+要写在每一行后面

```go
var address = "hello" +
	"word"
```

### 4.2基本数据类型转换



**注意**

```go
var i int8 = 10
// i + 8 是int8类型
```

只有强制转换，

```go
var i int8 = 1
var j = int16(i)
```

#### 基本类型转字符串



##### 使用fmt下的Sprintf



```go
package main

import (
    "fmt"
)

func main() {
    var i int8 = 100
    var address string = fmt.Sprintf("%d hello3434", i)
    fmt.Println(address)
}
```

##### 使用strconv包





#### 字符串转其他基本数据类型

##### 使用strconv包

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210521011754.png)



```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
   
	var i string = "100"
	var j int64
    // 因为这个函数会有俩个返回值
	j, _ = strconv.ParseInt(i, 10, 8)
	fmt.Println(j)

}
```



**注意**

如果是"hello"转int，那么直接转为0，并不会报错

高精度到低精度只会精度丢失，并不会报错



### 4.3指针类型



#### 4.3.1基础



```go
package main

import "fmt"

func main() {
	var num int = 10
	var p *int = &num
	fmt.Println(p)
	*p = 20
	fmt.Println(num)
}
```

&num:获取num地址

*int:int类型的指针

*p:获取p指针指向变量的地址

#### 4.3.2值类型和引用类型

(1) 值类型，都有对应的指针类型， 形式为 *数据类型，比如 int 的对应的指针就是 *int, float32对应的指针类型就是 *float32, 依次类推。 

(2) 值类型包括：基本数据类型 int 系列, float 系列, bool, string 、数组和结构体 struct



(1) 值类型：基本数据类型 int 系列, float 系列, bool, string 、数组和结构体 struct
(2) 引用类型：指针、slice 切片、map、管道 chan、interface 等都是引用类型





**值类型：变量直接存储值，内存通常在栈中分配**

**引用类型：变量存储的是一个地址，这个地址对应的空间才真正存储数据(值)，内存通常在堆**
**上分配，当没有任何变量引用这个地址时，该地址对应的数据空间就成为一个垃圾，由GC 来回收**



### 4.4标识符

#### 4.4.1基础

Golang 对各种变量、方法、函数等命名时使用的字符序列称为标识符

凡是自己可以起名字的地方都叫标识符



#### 4.4.2命名规则



(1) 由 26 个英文字母大小写，0-9 ，_ 组成

(2) 数字不可以开头。var num int //ok var 3num int //error

(3) Golang 中严格区分大小写

(4) 识符不能包含空格。

(5) 下划线"_"本身在Go 中是一个特殊的标识符，称为空标识符。可以代表任何其它的标识符，但 是它对应的值会被忽略(比如：忽略某个返回值)。所以仅能被作为占位符使用，不能作为标识符使用

(6) 能以系统保留关键字作为标识符（一共有 25 个），比如 break，if 等等...



#### 4.4.3注意事项



(1) 包名：保持 package 的名字和目录保持一致，尽量采取有意义的包名，简短，有意义，不要和
标准库不要冲突 fmt

(2)变量名、函数名、常量名：采用驼峰法

(3)如果变量名、函数名、常量名首字母大写，则可以被其他的包访问；如果首字母小写，则只能在本包中使用 ( 注：可以简单的理解成，首字母大写是公开的，首字母小写是私有的 ) ,在 golang没有 public , private 等关键字。

### 4.4系统保留关键字

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522201843.png)



### 4.5系统的预定义标识符



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522201953.png)



## 第五章  运算符

### 5.1算术运算符



#### 基础

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522170845.png)



#### 注意事项

##### 1.取模%

**a % b = a - a / b * b**

##### 2.除法

```go
10/3   = 3
```

##### 3.++ --

go 语言只支持 i++, i-- 这样的，没有 --i , ++i 同时 j = i++这样也是错误的

### 5.2关系运算符

#### 1.基础



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522171257.png)







### 5.3逻辑运算符



#### 5.3.1基础

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522171414.png)



#### 5.3.2注意事项

##### 1.短路

(1) &&也叫短路与：如果第一个条件为 false，则第二个条件不会判断，最终结果为 false 

(2) ||也叫短路或：如果第一个条件为 true，则第二个条件不会判断，最终结果为 true



### 5.4赋值运算符





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522172532.png)





### **5.5进制基础**

#### 5.5.1认知

几进制就是满几进1

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522193107.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522193143.png)



#### 5.5.2进制转换



##### 任意进制转十进制

二进制

```
01->0*2^1+0*2^0
```

八进制

```
71->7*8^1+1*8^0
```

十六进制

```
A1->10*16^1+1*16^0
```

##### 十进制转其他进制



十进制转二进制，除2取余的逆，直到商为0 (其他进制类似)



|      | 商   | 余数 |
| ---- | ---- | ---- |
| 14   | 7    | 0    |
| 7    | 3    | 1    |
| 3    | 1    | 1    |
| 1    | 0    | 1    |

1110

##### 二进制转八进制、十六进制

**二进制转八进制**

从末尾开始将二进制三位数转为对应八进制数

```
1110011 -> 1 110 011 ->163
```

转十六进制则为四位



十六进制转二进制、八进制转二进制

一位转四位、一位转三位





### **5.6原码反码补码**

正数和0：原码反码补码相同

负数的反码：符号位不变，其他位取反

负数的补码：反码+1



**计算机都是以补码进行运算**





### 5.7位运算符



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522172931.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522172551.png)



### 5、7指针运算符



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522173004.png)

### 5.8运算符优先级



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210522172800.png)







1：括号，++, --

2: 单目运算 

3：算术运算符 

4：移位运算 

5：关系运算符 

6：位运算符 

7：逻辑运算符 

8：赋值运算符 

9：逗号



### 5.9go没有三木运算符



## 第六章 流程控制



### 6.1IF ELSE



```GO
package main

import (
	"fmt"
)

func main() {
	var age int
	fmt.Scanln(&age)
	if age < 0 {
		fmt.Println("错误的数据")
	} else if age < -1 {
		fmt.Println("未成年")
	} else {
		fmt.Println("成年人")
	}
}
```

**注意：即使if语句中只有以及仍然要加{}**



### 6.2switch



```go

package main

import (
	"fmt"
)

func main() {
	var ch byte
	// 不要使用 Scanln

	fmt.Scanf("%c", &ch)
	// switch 'a'
	// switch test('a')
	switch ch {
		case 'a', 'b':
			fmt.Println("星期一或者星期二")
		case 'c':
			fmt.Println("星期三")
		default:
			fmt.Println("其他")
	}

	

	
}
```

switch：不需要写break，go已经帮我们添加了

golang 的 case 后的表达式可以有多个，使用 逗号 间隔,表示或的意思

case 后的各个表达式的值的数据类型，必须和 switch 的表达式数据类型一致

case/switch 后是一个表达式( 即：常量值、变量、一个有返回值的函数等都可以)

```go
// switch 'a'
// switch test('a')
```

default:不是必须的

case 后面的表达式如果是常量值(字面量)，则要求不能重复



switch:可以声明一个变量，不推荐

```go
switch age := 12; {
	
	case age == 18:
		fmt.Println("18")
		// 穿透
		fallthrough
	case age < 18:
		fmt.Println("未成年")
		fallthrough
	default:
		fmt.Println("成年")
}
```

switch：模拟ifel

```go
switch {
case 1 == 1 && 2 == 3:
	fmt.Println("error")
default:
	fmt.Println("true")
}
```



switch 穿透-fallthrough ，如果在 case 语句块后增加 fallthrough ,则会继续执行下一个 case，也 叫 switch 穿透,但是只可以穿透一次



### 6.3for//**go没有while**



```go
package main

import "fmt"

func main() {

	
	for i := 0; i < 10; i++{
		fmt.Println("matt", i)
	}
	
}

```



```go
i := 0
for i < 10{
	fmt.Println("matt", i)
    i++
}
```

遍历字符串

根据字符遍历的

```go
var str = "hello wordz中文"
// 如果使用传统的字符串遍历就会出错，因为3个字节
for index, val := range str {
	//fmt.Println(index, val)
	fmt.Printf("%d %c\n", index, val)
}
```

### 6.4break

break:跳出for循环



### 6.5continue

continue:跳出当前循环



### 6.6label

label:使用break跳出指定的for循环

同样continue也可以使用

```go
package main

import "fmt"

func main() {

	label1:
		for i := 0; i < 10; i++ {
			for j := 0; j < 10; j++ {
				if j == 3 {
					break label1
				}
				fmt.Println(j)
			}
			fmt.Println(i)
		}
}

```

### 6.7goto

goto:跳转到指定的行，不推荐使用



```go
package main

import (
	"fmt"
)

func main() {

	goto label1
	fmt.Print("不执行")
	label1:
		fmt.Print("执行")
}
```

```
输出：执行
```



## 第七章  函数使用



### 7.1认识

```go
func add(i int, j int) int {
	return i + j
}
```

func 函数名 (参数列表) (返回值类型列表)

​	函数体

​	可以有返回值也可以没有

### 7.2包

#### 7.2.1什么是包

一个文件夹，对应一个包



#### 7.2.2使用

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210524115127.png)



```go
package db

var Ip int = 11
```

```go
package main

import (
    // 包名的路径是在 %GOPATH/src路径下的
	"db"
	"fmt"
	"utils"
)

func main()  {
	fmt.Println("hello word")
	fmt.Println(utils.Add(1, 2))
	fmt.Println(db.Ip)
}

```

运行的时候根据 Directory 运行





```bash
GO111MODULE=off
```





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210524115517.png)



#### 7.2.3注意事项

##### 1.文件的包名通常和它的文件夹名一样

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210524115744.png)



##### 2.包的引入



```go
import "utils"
```

推荐这种

```go
import (
	"fmt"
    "utils"
)
```

**关于包的路径：包的路径是在 $GOPATH/src 开始找**



##### 3.权限 (变量函数大小写)

变量函数首字母小写只可以被该包访问，大写则可以被任意程序访问



##### 4.访问

包名+(方法名/函数名)

##### 5.包名可以起别名



```go
import tDb "db"
```

##### 6.同一个包下不能有相同的函数名或者变量名

##### 7.如果想把一个.go文件编译成可执行文件，则把该文件包名设置为 main



### 7.3函数调用

其实就是调用入栈，函数结束出栈



### 7.4return

只有一个返回值，可以不写 ()

可以用_接收方法的返回值

```go
func add(i int, j int) int {
    return i + j
}
```

```go
func add(i int, j int) (int, int) {
    return i + j, 1
}
```

```go
func main() {
    
    res, _ = add(1, 2)
}
```



### 7.5函数注意细节



1.参数列表可以有多个值，返回值也可以有多个值，类型可以是值类型，也可以是引用类型

2.注意变量的访问范围，函数内声明的，函数外就不可以访问，如果函数内和函数声明相同的变量，则函数内使用函数内声明的变量

3.大小写控制访问范围

4.基础数据类型、数组使用值得传递，引用类型使用引用传递

1)值类型：基本数据类型 int 系列, float 系列, bool, string 、数组和结构体 struct 

2)引用类型：指针、slice 切片、map、管道 chan、interface 等都是引用类型

5.不支持重载

**6.函数可以赋值给一个变量，也可以作为参数**

```go
a := test1
fmt.Println(a(1))
```



```go
func test2(test1 func(int) (int, int), n int) (){
	fmt.Println(test1(1))
	return
}
```

**7.支持自定义数据类型**



```go
//type 数据类型名 数据类型
type aa int
var i aa = 1
fmt.Println(i)
```





```go
package main

import (
	"fmt"
)
type t func(int) int
func main() {

	/*str := "11.1"
	t, err := strconv.ParseFloat(str, 64)
	fmt.Println(err == nil)
	fmt.Println(t)*/
	a := test1
	test2(1, 2, a)




}

func test1(i int) int {
	fmt.Println("test1")
	return i
}
//f func(int) int
func test2(i int, j int, f t) int {
	fmt.Println("test2")
	f(i)
	return i + j
}

```



8.支持对方法返回值命名

可以不写 return sum

```go
// 直接对返回值命名
func test3(i int, j int) (sum int) {
	sum = i + j
	return
}
```

9.使用 _接收方法的返回值



10.支持可变参数



```go
func test4(args... int) () {
	fmt.Println(args)
	fmt.Println(len(args))
}
```

```go
func main() {
    test4(1, 2, 3)
}
```

### 7.6init函数

main函数执行之前被执行

```go
func init() {
	// main函数执行之前被执行
	fmt.Println("init function")
}
```

变量定义 -> init 函数 -> main 函数

**如果引用了其他文件，先执行其他文件的**

### 7.7匿名函数

#### 7.7.1认知

匿名函数：没有名字的函数



#### 7.7.2使用

1.在定义的时候就使用

```go
// 定义的时候就使用
	res := func(i int, j int) int {
		return i + j
	}(1, 2)
	fmt.Println(res)
```

2.将函数赋值一个变量



```go
// 将该函数给一个变量，通过变量来调用
    add := func(i int, j int) int {
    	return i + j
	}
	fmt.Println(add(1, 2))
```

### 7.8闭包



#### 7.8.1认识

闭包：一个函数和与其相关的引用环境组合的一个整体(实体)



#### 7.8.2使用



```go
func makeSuffix(suffix string) func(string) string {

	return func(fileName string) string {
		if strings.HasSuffix(fileName, suffix) {
			return fileName
		}
		return fileName + suffix
	}
}
```

返回的函数和suffix组成一个整体，返回的函数对suffix进行操作



```go
func main() {
	
	b := makeSuffix(".jpg")
	fmt.Println(b("aaa.js"))
	fmt.Println(b("aa.jpg"))
}
```

### 7.9defer使用



```go
func testDefer(n int) int {
	// 值的拷贝
	defer fmt.Println("defer" + fmt.Sprintln(n))
	n++
	fmt.Println("111")
	return 1
}
```

```go
defer fmt.Println("defer" + fmt.Sprintln(n))
```

这样会依次压入栈，并在该函数执行完后在从栈取出，同时n也是值的拷贝



### 字符串常用的函数



#### 1.len():统计字符串字节的长度

一个中文三个字节

```go
var str string = "hello 中文"
fmt.Println(len(str))
```

#### 2.字符串遍历，根据字符进行遍历

```go
str1 := []rune(str)
for i := 0; i < len(str1); i++ {
	fmt.Printf("%c", str1[i])
}
```

#### 3.字符串转整数



```go
str2 := "1111111"
var i int64
// bitsize指定8， 如果是3333 则返回128
i, _ = strconv.ParseInt(str2, 10, 64)
fmt.Println(i)

str3 := "123"
//var k int
k, err := strconv.Atoi(str3)
if err != nil {
	fmt.Println("转换错误")
} else {
	fmt.Println(k)
}
```

#### 4.整数转字符串

```go
var str4 string = strconv.Itoa(11)
fmt.Println(str4)
```

#### 5.字符串 转 []byte: var bytes = []byte("hello go")

```go
var str string = "hello word"
bytes := []byte(str)
fmt.Println(bytes)
```

#### 6.字节转字符串

```go
fmt.Println(string(bytes))
```

#### 7.十进制转任意进制

```go
// 十进制转二进制
fmt.Println(strconv.FormatInt(67,2))
```

#### 8.查找子串是否在指定的字符串中: strings.Contains("seafood", "foo") //true

```go
// strings Contains
fmt.Println(strings.Contains("hello", "ele"))
```

#### 9.统计一个字符串有几个指定的字符串

```go
// strings Count
fmt.Println("strings Count:" ,strings.Count("hello", "e"))
```

#### 10.字符串比较

EqualFold:忽略大小写

```go
// strings.EqualFold
fmt.Println(strings.EqualFold("ab", "Ab"))
fmt.Println("ab" == "Ab")
```

#### 11返回子串第一次在字符串出现的位置



```go
fmt.Println("Index")
fmt.Println(strings.Index("abcdef mcatt", "c"))
fmt.Println(strings.LastIndex("abcdef mcactt", "c"))
```

#### 12返回子串最后一次在字符串出现的位置



```go
fmt.Println(strings.LastIndex("abcdef mcactt", "c"))
```

#### 13将指定的子串替换成 另外一个子串: strings.Replace("go go hello", "go", "go 语言", n) n 可以指 定你希望替换几个，如果 n=-1 表示全部替换



```go
fmt.Println(strings.Replace("aa bb ccbc bb bb ", "bb", "BB", -1))

```

#### 14字符串分割

```go
str := "aabcbebeeee"
strArr := strings.Split(str, "b")
for i := 0; i < len(strArr); i++ {
	fmt.Print(strArr[i])
}
```

#### 15字符串大小写转换



```go
fmt.Println(strings.ToLower("Abc"))
fmt.Println(strings.ToUpper("Abc"))
```

#### 16去除字符串俩边的空格

```go
fmt.Println(strings.TrimSpace("   aa  dfer dfdf    "))
```

#### 17字符串指定的字符去除

```go
fmt.Println(strings.Trim("aabbccaa", "aa"))
```

```go
fmt.Println(strings.TrimLeft("aabbccaa", "aa"))

fmt.Println(strings.TrimRight("aabbcccaa", "aa"))
```

#### 18字符串是否包含某个前缀、后缀

```go
fmt.Println(strings.HasPrefix("aabbcc", "aa"))
fmt.Println(strings.HasSuffix("aabbcc", "aa"))
```



### 日期函数



time.Time:类型

time.now()

```go
now := time.Now()
// fmt.Println(now)
fmt.Printf("%v\n%T", now, now)
```

获取年、月、日、时、分、秒



```go
fmt.Printf("Year-----%v\n", now.Year())
fmt.Printf("Month-----%v\n", int(now.Month()))
fmt.Printf("Day-----%v\n", now.Day())
fmt.Printf("Hour-----%v\n", now.Hour())
fmt.Printf("Minute-----%v\n", now.Minute())
fmt.Printf("Second-----%v\n", now.Second())
```



格式化

```go
fmt.Println("-------格式化------")
// 时间是固定的 2006/01/02 15:04:05
fmt.Println(now.Format("2006年01月02日 15时:04分:05秒"))
```

也可以使用Sprintf





获取单位时间 (NanoSecond,MicroSecond,MilliSecond,Second,Minute,Hour)



```go
fmt.Println(time.Millisecond)
fmt.Printf("%T", time.Second)
fmt.Println(time.Second)
```

Sleep()



```go
time.Sleep(time.Second * 5)
```

 获取时间戳

```go
fmt.Println(now.Unix())
fmt.Println(now.UnixNano())
```







## 常用包



### 从键盘输入



```go
package main

import (
	"fmt"
)
func main()  {
	var name string
	var address string
	//fmt.Scanln(&name)
	fmt.Scanf("%s %s", &name, &address)
	fmt.Println(name, address)
}
```



## 数组

### 介绍

存放多个同一类型的数据



### 使用

#### 声明

```go
var arr1 [3]int
```

四种初始化方法

```go
var arr1 [3]int = [3]int{1, 2, 3}
fmt.Println(arr1)

var arr2 = [5]int{1, 2, 3, 4, 5}
fmt.Println(arr2)

arr3 := [...]float64{1, 2, 3}
fmt.Println(arr3)

var arr4 = [...]string{1: "aa", 0: "bb"}
fmt.Println(arr4)
```



遍历

```go
for index, val := range arr4 {
	fmt.Println(index, val)
}
```



```go
for i := 0; i < len(arr4); i++ {
	fmt.Println(arr4[i])
}
```

### 注意

1.数组一旦声明，其长度不能发生改变

2.数组创建后，没有赋值，会有默认值

3.go 语言中数组是值类型，而不是引用类型



4.传递参数需要指定数组长度

```go
// [3]int [4]int 认为是不同数据类型
func valueTest(arr [3]int) {
	arr[0] = 1
}
```



### 切片



```go
var arr = [5]int{1, 2, 3, 45, 5}
slice := arr[2:4]
arr[2] = -1
fmt.Println(slice)
// 元素数量
fmt.Println(len(slice))
// 容量
fmt.Println(cap(slice))
```



```go
var slice1 []int = make([]int, 2, 10)
slice1[0] = 0
slice1[1] = 1
fmt.Println(slice1)
```



```go
fmt.Println("方式三")
var slice2 []float64 = []float64{1, 2, 3}
fmt.Println(cap(slice2))
```



直接引用数组，对数组是可见的，使用 make 方式，引用的数组是不可见的

使用make可以指定切片的大小和容量

没有赋值会有默认值





```go
type slice struct { 
    ptr *[2]int 
    len int 
    cap int
}
```

引用一个数组

数量

容量





#### 遍历



```go
for index, value := range slice2 {
	fmt.Printf("---%v:%v ", index, value)
}
```

#### 注意



```go
var slieceDemo = arr[startIndex: endIndex]
```

包含左边，不包含右边

var slice = arr[0:end] 可以简写 var slice = arr[:end] 

var slice = arr[start:len(arr)] 可以简写： var slice = arr[start:] 

var slice = arr[0:len(arr)] 可以简写: var slice = arr[:]



cap 是一个内置函数，用于统计切片的容量，即最大可以存放多少个元素。

```go
// 元素数量
fmt.Println(len(slice))
// 容量
fmt.Println(cap(slice))
```

切片定义完后，还不能使用，因为本身是一个空的，需要让其引用到一个数组，或者make 一
个空间供切片来使用



切片仍然可以切片



用 append 内置函数，可以对切片进行动态追加



```go
var arr = [5]int{1, 2, 3, 4, 5}
var slice []int = arr[:]
fmt.Println(slice)

// 返回
slice = append(slice, 10)
fmt.Println(slice)
```

切片的拷贝

```go
package main

import "fmt"

func main() {
	var slice1 []int = make([]int, 5)
	var slice2 []int = make([]int, 10)

	slice1[0] = 1
	copy(slice2, slice1)
	fmt.Println(slice2)
}
```

切片是引用传递



string底层也是数组，可以使用切片



### 二维数组



```go
func main() {
	var arr = [2][2]int{{1, 2}, {3, 4}}
	fmt.Println(arr)

	// 只有第一个可以为...
	var arr1 = [...][3]int{{1, 2}, {3, 4}}
	fmt.Println(arr1)
}
```





## Map使用

### 介绍

key-value 的数据结构，类似于 java 中的 map



key 的类型：bool, 数字，string, 指针, channel , 还可以是只包含前面几个类型的 接口, 结构体, 数组，通常 key 为 int 、string 注意: slice， map 还有 function 不可以，因为这几个没法用 == 来判断
valuetype 的类型和 key 基本一样，通常为: 数字(整数,浮点数),string,map,struct



### 使用

#### 声明



```go
var map1 map[int]int
```

1) map 在使用前一定要make(需要分配内存)

2) map 的 key 是不能重复，如果重复了，则以最后这个 key-value 为准 

3) map 的 value 是可以相同的. 

4) map 的 key-value 是无序



#### 三种使用方式



```go
var map1 map[int]int
map1 = make(map[int]int, 10)
fmt.Println(map1)
```



```go
map2 := make(map[int]int, 10)
fmt.Println(map2)
```



```go
map3 := map[int]int {
	1: 1,
	2: 2,
}
fmt.Println(map3)
```



### map中的方法

添加和更新



```go
var a = make(map[int]string)
a[0] = "matt"
a[1] = "pony"
a[0] = "jack"
a[100] = "aa"
```

删除



```go
// 删除不存在的 key 也不会出错
delete(a, 1)
```



查找

```go
// val:值 ok:是否找到
val, ok := a[3]
fmt.Println(ok, val)
```

遍历



```go
a1 := make(map[string]string)
a1["1"] = "a"
a1["2"] = "b"
a1["3"] = "c"
a1["4"] = "d"
for k, v := range a1 {
	fmt.Println(k, v)
}
```



长度

```go
fmt.Println(len(a1), "map的长度")
```

### *map切片*

```go
package main

import "fmt"

func main() {
	var students = make([]map[string]string, 2, 2)
	students[0] = map[string]string{
		"name": "matt",
		"age": "11",
	}
	fmt.Println(students)
}

```



### 注意

map是引用类型

map会自动扩容

map的 value 经常是struct







## 问题

**在函数外使用如下就会出错**

```go
i := 1

// 等价于
var i int
// i = 1 赋值语句不可以在函数外使用，是执行语句
i = 1
```











```bash
go build -o 输出目录 ./src/main
```

pkg:库文件





```go
string()
len()
```



## 面向对象

### 概述

go 语言并没有类，而采用结构体，仍然有面向对象中封装继承多态等特性。



### 结构体



#### 声明结构体



```go
type 结构体名 struct {
    字段名 类型
}
```





```go
type Person struct {
	Name string
	Age  int
	p *int
	slice []int
	map1 map[string]string
}
```



结构体是值类型

创建一个结构体变量后，如果没有给字段赋值，都会有零值，如果是引用类型，在没有进行分配内存则它的值为 nil 。



#### 创建结构体变量



```go
func main() {
	// 1
	var person Person
	person.Age = 11
	person.Name = "matt"
	fmt.Println(person)
	//2
	var p1 = Person{}
	fmt.Println(p1)

	// 3
	var p3 *Person = new(Person)
	(*p3).Name = "33"
	p3.Name = "44优化等价于上面的"
	fmt.Println(*p3)

	// 4
	var p4 *Person = &Person{}
	p4.Age = 111
	fmt.Println(*p4)
}
```



创建结构体变量也可以指定字段值

```go
func main() {
	var c Computer = Computer{
		Age: 1,
		Name: "matt",
	}
	fmt.Println(c)
}
```

这样指定字段可以不按结构体中的顺序，否则就要按结构体中的顺序。



#### 结构体使用注意



结构体所有字段在内存中连续的



俩个结构体进行转换的时候，要求这俩个结构体需要有相同的字段



```go
a = B(b)
```



对结构体进行重新定义， golang 认为是不同的数据类型



```go
type P Person
```

struct 的每个字段上，可以写上一个 tag, 该 tag 可以通过反射机制获取，常见的使用场景就是序列化和反序列化。



```go
import "fmt"
import "encoding/json"

type A struct {
	age int
	num int
}

type B struct {
	age int
	num int
}

type C struct {
	Name string `json:"name"`
}
func main() {
	var a A
	var b B
	a.age = 1
	// 要求字段一致
	b = B(a)
	var c C
	c.Name = "hello ma"
	str1, _ := json.Marshal(c)
	fmt.Println(string(str1))
	fmt.Println(b)
}

```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210701154924.png)



### 方法



#### 使用



```go
import "fmt"

type Person struct {
	Age int
}

func (p Person) getAge() int {
	return p.Age
}

func main() {
	var p Person
	p.Age = 18
	fmt.Println(p.getAge())

}
```

该方法和 Person 结构体进行绑定

方法进行调用会把调用该方法的变量赋值给该方法



#### 方法使用注意



结构体类型是值类型，在方法调用中，遵守值类型的传递机制，是值拷贝传递方式



方法也可以接收结构体指针



```go
func (circle *Circle) test()  {
	// (*circle).R
    // 进行了优化
	fmt.Println(circle.R)
}
```



方法不仅可以作用于结构体，还可以作用于 int,string等



```go
import "fmt"

func (i integer) testInt() {
	fmt.Println(i)
}

type integer int

func main() {
	var j integer = 10
	j.testInt()
}
```

方法的访问范围控制的规则，和函数一样。方法名首字母小写，只能在本包访问，方法首字母
大写，可以在本包和其它包访问。



如果一个类型实现了 String()这个方法，那么 fmt.Println 默认会调用这个变量的 String()进行输出，类似于 java 中的 toString() 方法



```go
func (c Computer) String() string {
	str := fmt.Sprintf("Name=%s Age=%d", c.Name, c.Age)
	return str
}
```



### 面向对象特性

#### 封装

##### 概念

将对象属性隐藏起来，属性的操作只可以通过被授权的方法。



##### 使用

结构体属性、方法首字母小写，其他包就不可以访问，当前包仍然可以访问。



为结构体提供一个创建的函数，相当于java中的构造函数。



编写set,get 方法。



```go
package main

type Person struct {
	name string
	age  int
}

func NewPerson() Person {
	var person = Person{}
	return person
}

func (p *Person) SetName(name string) {
	p.name = name
}

func (p *Person) GetName() string {
	return p.name
}

```

#### 继承



##### 概述

子类具有父类的属性和方法



##### 使用



```go
type S struct {
	Name string
	Age int
}

type X struct {
	S
}

func (s S) showInfo() {
	fmt.Println(s.Name)
}

func (x *X) showInfo() {
	fmt.Printf("x---name=%v age=%v\n",x.Name, x.Age)
}

func main() {
	var x  = &X{}
	x.S.Name = "matt"
	x.S.Name = "aa"
	x.Name = "ma"

	x.S.showInfo()

	x1 := X{
		S{
			Name: "aa",
			Age: 11,
		},
	}
	fmt.Println(x1)


}
```



##### 继承使用注意

结构体可以使用嵌套匿名结构体所有的字段和方法(首字母大小写都可以获得)



结构体访问可以简化



```go
func main() {
	var x  = &X{}
	x.S.Name = "matt"
	// 对上面进行简化
	x.Name = "ma"
	x.S.showInfo()

}
```

上述Name字段，编译器首先会从 X 中查找该属性，找不到在从不S中找，最后找不到则报错。





当结构体和匿名结构体有相同的字段或者方法时，编译器采用就近访问原则访问，如希望访问
匿名结构体的字段和方法，可以通过匿名结构体名（x.S.Name）来区分



结构体嵌入两个(或多个)匿名结构体，如两个匿名结构体有相同的字段和方法(同时结构体本身 没有同名的字段和方法)，在访问时，就必须明确指定匿名结构体名字，否则编译报错。



如果一个 struct 嵌套了一个有名结构体，这种模式就是组合，如果是组合关系，那么在访问组合 的结构体的字段或方法时，必须带上结构体的名字



```go
type A struct {
	Name string
}

type B struct {
	a A
}

func main() {
	var b B = B{}
	b.a.Name = "matt"
	fmt.Println(b)
}
```

可以在创建结构体变量时指定匿名结构体值



```go
var a A = B{
    B{
        Name: "matt sir"
    }
}
```



##### 多重继承

嵌套多个匿名结构体



如果嵌套的多个匿名结构体具有相同的属性和方法，那么需要指定具体哪一个结构体。

避免使用多重继承。





#### 接口



##### 使用

```go
type I interface {
	start()
}

type A struct {
}

func (a *A) start() {
	fmt.Println("A 开始...")
}
```

结构体 A 实现接口 I

##### 使用接口注意

1.接口本身不能创建实例,但是可以指向一个实现了该接口的自定义类型的变量(实例)



```go
// I是接口 s 是S的实例，S实现I
var s I
```

接口中不可以有变量

接口中所有的方法都没有实现



一个自定义类型实现了一个接口的所有方法，那么就说实现了该接口。

自定义类型可以实现多个接口



一个接口可以继承多个接口，比如A接口继承B，C, 如果实现A接口，那么就要把A,B,C中所有方法实现。

只要是自定义数据类型，就可以实现接口，不仅仅是结构体类型



interface 类型默认是一个指针(引用类型)，如果没有对 interface 初始化就使用，那么会输出 nil

空接口是没有方法，即任何变量实现了空接口，任何一个变量可以使用空接口类型。



##### 实现和继承



继承的价值主要在于：解决代码的复用性和可维护性。 

接口的价值主要在于：设计，设计好各种规范(方法)，让其它自定义类型去实现这些方法





#### 多态



多态参数：

一个方法中的一个参数是I类型，那么就可以接收实现I类型的所有类



多态数组

一个数组中的I类型，那么就可以接收实现I类型的所有类





### 类型断言



#### 概述

一个变量知道他是某一个接口类型，但是不知道它是哪一个具体类型，所以使用断言。





#### 使用



```go
func main() {
	var a interface{}
	var b B = B{}
	a = b
	c, ok := a.(B)
	fmt.Println(ok)
	fmt.Println(c)
}
```

