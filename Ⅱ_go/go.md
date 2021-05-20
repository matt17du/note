## 使用

### 安装

[下载地址](https://golang.org/dl/)

win10/64-》选择x86-64    



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210420150359.png)



选择go1.13.15.windows-amd64.msi一直下一步安装即可，更改安装路径即可，安装完成后它已经配置了环境变量；

或者选择go1.13.15.windows-amd64.zip解压缩，配置环境变量；





### 配置



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



### 验证

验证go环境是否安装成功

```bash
go version
```

格式化代码

```
gofmt -w main.go
```



### 资料

[中文API](https://studygolang.com/pkgdoc)

[官网](https://golang.org/)



## Hello Word

### 程序

新建项目

项目下创建src文件夹，创建bin文件夹，创建pkg文件夹

```go
package main

import "fmt"

func main() {
	fmt.Println("hello word")
}
```

### 编译运行

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



### 注意事项

go源文件以 go 为扩展名

go 的入口函数是 main() 函数

go 严格区分大小写

go 语句不需要加分号，go语言自动会加分号

go语句是一行一行编译，所以一行不可以写多条语句

引用的包或者定义的变量必须使用，不使用会报错



### 注释



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

## 变量

### 转义字符



```bash
1) \t : 表示一个制表符，通常使用它可以排版。

2) \n ：换行符 

3) \\ ：一个\ 

4) \\" ：一个"

5) \r ：一个回车
	fmt.Println("aaa\r bb");
```

### 变量声明

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



## 数据类型

### 基本数据类型



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

### 基本数据类型转换



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











