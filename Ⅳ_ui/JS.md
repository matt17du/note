



```js
let i = 100 // 声明一个局部变量
const i = 100 // 声明一个常量
```



```js
sort
filter
foreach
reduce
```







## ES6



### let

var 

​	声明的变量没有局部作用域

​	可以声明多次

​	会变量提升

let 

​	声明的变量有局部作用域

​	只可以声明一次

​	不会变量提升



```js
console.log(x)  //undefined
var x = "apple"


console.log(y)  //ReferenceError: y is not defined
let y = "banana"
```



### const

声明常量



### 解构赋值



```js
//1、数组解构

// 传统

let a = 1, b = 2, c = 3
console.log(a, b, c)

// ES6
let [x, y, z] = [1, 2, 3]
console.log(x, y, z)
```



```js

//2、对象解构
let user = {name: 'Helen', age: 18}

// 传统
let name1 = user.name
let age1 = user.age
console.log(name1, age1)

// ES6
let { name, age } =  user//注意：结构的变量必须是user中的属性
console.log(name, age)
```

### 模板字符串



```js
// 1、多行字符串
2
let string1 =  `Hey,
3
can you stop angry now?`
4
console.log(string1)
5
// Hey,
6
// can you stop angry now?
```





```js
// 2、字符串插入变量和表达式。变量名写在 ${} 中，${} 中可以放入 JavaScript 表达。

let name = "Mike"

let age = 27

let info = `My Name is ${name},I am ${age+1} years old next year.`

console.log(info)

// My Name is Mike,I am 28 years old next year.
```



```js
// 3、字符串中调用函数

function f(){

    return "have fun!"

}

let string2 = `Game start,${f()}`

console.log(string2);  // Game start,have fun!
```





### 声明对象缩写



```js
const age = 12

const name = "Amy"

// 传统

const person1 = {age: age, name: name}

console.log(person1)

// ES6

const person2 = {age, name}
console.log(person2) //{age: 12, name: "Amy"}
```



### 方法缩写



```js
// 传统

const person1 = {

    sayHi:function(){

        console.log("Hi")

    }

}

person1.sayHi();//"Hi"

// ES6

const person2 = {

    sayHi(){

        console.log("Hi")

    }

}

person2.sayHi()  //"Hi"
```



### 对象扩展运算符

拓展运算符（...）用于取出参数对象所有可遍历属性然后拷贝到当前对象。



```js
// 1、拷贝对象

let person1 = {name: "Amy", age: 15}

let someone = { ...person1 }

console.log(someone)  //{name: "Amy", age: 15}

// 2、合并对象

let age = {age: 15}

let name = {name: "Amy"}

let person2 = {...age, ...name}

console.log(person2)  //{age: 15, name: "Amy"}
```



### 对象的默认参数



```js
function showInfo(name, age = 17) {

    console.log(name + "," + age)

}

// 只有在未传递参数，或者参数为 undefined 时，才会使用默认参数

// null 值被认为是有效的值传递。

showInfo("Amy", 18)  // Amy,18

showInfo("Amy", "")  // Amy,

showInfo("Amy", null)  // Amy, null

showInfo("Amy")     // Amy,17

showInfo("Amy", undefined) // Amy,17
```



### 不定参数



```js

function f(...values) {

    console.log(values.length)

}

f(1, 2)      //2

f(1, 2, 3, 4)  //4
```



### 箭头函数

箭头函数提供了一种更加简洁的函数书写方式。基本语法是：
参数 => 函数体













```js
const {comment,index,deleteComment} = this 
上面的这句话是一个简写，最终的含义相当于
const  comment = this.comment
const  index = this.index
const   deleteComment = this.deleteComment
```





### 模块





```js
export { getList, save }
```

```js
import { getList, save } from "../api/user.js"
```









## end

### 