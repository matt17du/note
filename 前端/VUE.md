## 基本使用

v-model:双向绑定数据

{{取值}}

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <input type="text" v-model="username">
    <p>hello word{{username}}</p>
</div>


<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
    const vm = new Vue({
        // 选项
        el: '#app', //element
        data: {
            username : 'matt'
        }
    })

</script>
</body>
</html>
```



### 模板语法

v-html:innerHTML

v-text:innterText

:src="src" 

@click: 事件的绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<div id="app">
    {{username}}
    <p v-html="msg"></p>
    <p v-text="msg"></p>
    <img src="" v-bind:src="src">
    
    <img src="" :src="src">

    <button v-on:click="test">hello word</button>
    <button @click="test">hello word</button>
</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
    const vm = new Vue({
        // 选项
        el: '#app', //element
        data: {
            username : 'hello word',
            msg : 'jav',
            src : 'https://www.baidu.com/img/flexible/logo/pc/result@2.png'
        },
        methods: {
            test() {
                alert('hello word')
            }
        }
    })

</script>
</body>
</html>
```

### 计算属性和监视

1. 计算属性
    在computed属性对象中定义计算属性的方法
    在页面中使用{{方法名}}来显示计算的结果
2. 监视属性:
    通过通过vm对象的$watch()或watch配置来监视指定的属性
    当属性变化时, 回调函数自动调用, 在函数内部进行计算
3. 计算属性高级:
    通过getter/setter实现对属性数据的显示和监视
    计算属性存在缓存, 多次读取只执行一次getter计算

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="demo">
    姓: <input type="text" placeholder="First Name" v-model="firstName"><br>
    名: <input type="text" placeholder="Last Name" v-model="lastName"><br>
    <!--fullName1是根据fistName和lastName计算产生-->
    姓名1(单向): <input type="text" placeholder="Full Name1" v-model="fullName1"><br>
    姓名2(单向): <input type="text" placeholder="Full Name2" v-model="fullName2"><br>
    姓名3(双向): <input type="text" placeholder="Full Name3" v-model="fullName3"><br>

    <p>{{fullName1}}</p>
    <p>{{fullName1}}</p>
</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
    const vm = new Vue({
        el: '#demo',
        data: {
            firstName: 'A',
            lastName: 'B',
            fullName2: 'A-B'
        },
        computed : {
            fullName1() {
                return this.firstName + "1-1" + this.lastName;
            },
            fullName3 : {
                get() {
                    return this.firstName + ' ' + this.lastName;
                },
                set(value) {
                    const names = value.split(' ')
                    console.log(names[0])
                    console.log(names[1])
                    this.firstName = names[0]
                    this.lastName = names[1]
                }
            }
        },
        watch : {
             firstName: function (value) {
                 this.fullName2 = value + this.lastName;
             }
        }
    })
</script>
</body>
</html>
```

### class style 绑定



1. 理解
    在应用界面中, 某个(些)元素的样式是变化的
    class/style绑定就是专门用来实现动态样式效果的技术
2. class绑定: :class='xxx'
      xxx是字符串
    xxx是对象
    xxx是数组(使用较少)
3. style绑定
    :style="{ color: activeColor, fontSize: fontSize + 'px' }"
    其中activeColor/fontSize是data属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .classA {
            color: red;
        }
        .classB {
            background: blue;
        }
        .classC {
            font-size: 20px;
        }
    </style>
</head>
<body>

<div id="demo">
    <h2>1. class绑定: :class='xxx'</h2>
    <p :class="myClass">xxx是字符串</p>
    <p :class="{classA: hasClassA, classB: hasClassB}">xxx是对象</p>
    <p :class="['classA', 'classB']">xxx是数组</p>

    <h2>2. style绑定</h2>
    <p :style="{color:activeColor, fontSize}">:style="{ color: activeColor, fontSize: fontSize + 'px' }"</p>

    <button @click="update">更新</button>

</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
    const vm = new Vue({
        el: '#demo',
        data: {
            myClass : 'classA',
            hasClassA: true,
            hasClassB : false
        },
        methods : {
            update() {
                this.myClass = 'classB'
                this.hasClassA = !this.hasClassA
                this.hasClassB = !this.hasClassB
            }
        }
    })
</script>

</body>
</html>
```

### 条件渲染

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>08_条件渲染</title>
</head>
<body>
<!--
1. 条件渲染指令
  v-if
  v-else
  v-show
2. 比较v-if与v-show
  如果需要频繁切换 v-show 较好
if:显示与删除
show:隐藏
-->

<div id="demo">
  <p v-if="ok">表白成功</p>
  <p v-else>表白失败</p>

  <hr>
  <p v-show="ok">求婚成功</p>
  <p v-show="!ok">求婚失败</p>

  <button @click="ok=!ok">切换</button>
</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
  new Vue({
    el: '#demo',
    data: {
      ok: true,
    }
  })
</script>
</body>
</html>
```

### 列表渲染



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>06_列表渲染</title>
</head>
<body>

<!--
1. 列表显示
  数组: v-for / index
  对象: v-for / key
2. 列表的更新显示
  删除item
  替换item
-->

<div id="demo">
  <h2>测试: v-for 遍历数组</h2>
  <ul>
    <li v-for="(p, index) in persons" :key="index">
      {{index}}--{{p.name}}--{{p.age}}
      --<button @click="deleteP(index)">删除</button>
      --<button @click="updateP(index, {name:'Cat', age: 16})">更新</button>
    </li>
  </ul>
  <button @click="addP({name: 'xfzhang', age: 18})">添加</button>

  <h2>测试: v-for 遍历对象</h2>

  <ul>
    <li v-for="(item, key) in persons[1]" :key="key">{{key}}={{item}}</li>
  </ul>

</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
  new Vue({
    el: '#demo',
    data: {
      persons: [
        {name: 'Tom', age:18},
        {name: 'Jack', age:17},
        {name: 'Bob', age:19},
        {name: 'Mary', age:16}
      ]
    },

    methods: {
      deleteP (index) {
        this.persons.splice(index, 1) // 调用了不是原生数组的splice(), 而是一个变异(重写)方法
              // 1. 调用原生的数组的对应方法
              // 2. 更新界面
      },

      updateP (index, newP) {
        console.log('updateP', index, newP)
        // this.persons[index] = newP  // vue根本就不知道
        this.persons.splice(index, 1, newP)
        // this.persons = []
      },

      addP (newP) {
        this.persons.push(newP)
      }
    }
  })
</script>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>06_列表渲染_过滤与排序</title>
</head>
<body>
<!--
1. 列表过滤
2. 列表排序
-->

<div id="demo">
  <input type="text" v-model="searchName">
  <ul>
    <li v-for="(p, index) in filterPersons" :key="index">
      {{index}}--{{p.name}}--{{p.age}}
    </li>
  </ul>
  <div>
    <button @click="setOrderType(2)">年龄升序</button>
    <button @click="setOrderType(1)">年龄降序</button>
    <button @click="setOrderType(0)">原本顺序</button>
  </div>
</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
  new Vue({
    el: '#demo',
    data: {
      searchName: '',
      orderType: 0, // 0代表不排序, 1代表降序, 2代表升序
      persons: [
        {name: 'Tom', age:18},
        {name: 'Jack', age:17},
        {name: 'Bob', age:19},
        {name: 'Mary', age:16}
      ]
    },

    computed: {
      filterPersons () {
//        debugger
        // 取出相关数据
        const {searchName, persons, orderType} = this
        let arr = [...persons]
        // 过滤数组
        if(searchName.trim()) {
          arr = persons.filter(p => p.name.indexOf(searchName)!==-1)
        }
        // 排序
        if(orderType) {
          arr.sort(function (p1, p2) {
            if(orderType===1) { // 降序
              return p2.age-p1.age
            } else { // 升序
              return p1.age-p2.age
            }

          })
        }
        return arr
      }
    },

    methods: {
      setOrderType (orderType) {
        this.orderType = orderType
      }
    }
  })
</script>
</body>
</html>
```

### 事件的处理



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>07_事件处理</title>
</head>
<body>
<!--
1. 绑定监听:
  v-on:xxx="fun"
  @xxx="fun"
  @xxx="fun(参数)"
  默认事件形参: event
  隐含属性对象: $event
2. 事件修饰符:
  .prevent : 阻止事件的默认行为 event.preventDefault()
  .stop : 停止事件冒泡 event.stopPropagation()
3. 按键修饰符
  .keycode : 操作的是某个keycode值的健
  .enter : 操作的是enter键
-->

<div id="example">

  <h2>1. 绑定监听</h2>
  <button @click="test1">test1</button>
  <button @click="test2('abc')">test2</button>
  <button @click="test3('abcd', $event)">test3</button>

  <h2>2. 事件修饰符</h2>
  <a href="http://www.baidu.com" @click.prevent="test4">百度一下</a>
  <div style="width: 200px;height: 200px;background: red" @click="test5">
    <div style="width: 100px;height: 100px;background: blue" @click.stop="test6"></div>
  </div>

  <h2>3. 按键修饰符</h2>
  <input type="text" @keyup.13="test7">
  <input type="text" @keyup.enter="test7">

</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
  new Vue({
    el: '#example',
    data: {

    },
    methods: {
      test1(event) {
        alert(event.target.innerHTML)
      },
      test2 (msg) {
        alert(msg)
      },
      test3 (msg, event) {
        alert(msg+'---'+event.target.textContent)
      },

      test4 () {
        alert('点击了链接')
      },

      test5 () {
        alert('out')
      },
      test6 () {
        alert('inner')
      },

      test7 (event) {
        console.log(event.keyCode)
        alert(event.target.value)
      }
    }
  })
</script>
</body>
</html>
```

### 表单的输入输出

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>08_表单输入绑定</title>
</head>
<body>
<!--
1. 使用v-model(双向数据绑定)自动收集数据
  text/textarea
  checkbox
  radio
  select
-->
<div id="demo">
  <form action="/xxx" @submit.prevent="handleSubmit">
    <span>用户名: </span>
    <input type="text" v-model="username"><br>

    <span>密码: </span>
    <input type="password" v-model="pwd"><br>

    <span>性别: </span>
    <input type="radio" id="female" value="女" v-model="sex">
    <label for="female">女</label>
    <input type="radio" id="male" value="男" v-model="sex">
    <label for="male">男</label><br>

    <span>爱好: </span>
    <input type="checkbox" id="basket" value="basket" v-model="likes">
    <label for="basket">篮球</label>
    <input type="checkbox" id="foot" value="foot" v-model="likes">
    <label for="foot">足球</label>
    <input type="checkbox" id="pingpang" value="pingpang" v-model="likes">
    <label for="pingpang">乒乓</label><br>

    <span>城市: </span>
    <select v-model="cityId">
      <option value="">未选择</option>
      <option :value="city.id" v-for="(city, index) in allCitys" :key="city.id">{{city.name}}</option>
    </select><br>
    <span>介绍: </span>
    <textarea rows="10" v-model="info"></textarea><br><br>

    <input type="submit" value="注册">
  </form>
</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
  new Vue({
    el: '#demo',
    data: {
      username: '',
      pwd: '',
      sex: '男',
      likes: ['foot'],
      allCitys: [{id: 1, name: 'BJ'}, {id: 2, name: 'SS'}, {id: 3, name: 'SZ'}],
      cityId: '2',
      info: ''
    },
    methods: {
      handleSubmit () {
        console.log(this.username, this.pwd, this.sex, this.likes, this.cityId, this.info)
        alert('提交注册的ajax请求')
      }
    }
  })
</script>
</body>
</html>
```





```
v-if:移除
v-show:隐藏
```

### 生命周期

mounted(): 发送 ajax 请求, 启动定时器等异步任务
beforeDestory(): 做收尾工作, 如: 清除定时器

























































## 组件化

**组件：一个局部功能界面，包含该界面的全部资源**

### 安装



需要有npm , 

```js
npm install -g vue-cli  // 首先输入vue，检测是否有该工具
vue init webpack vue_demo
npm run dev
```



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210319233446.png)



### 文件结构



```js
|-- build : webpack 相关的配置文件夹(基本不需要修改)
|-- dev-server.js : 通过 express 启动后台服务器
|-- config: webpack 相关的配置文件夹(基本不需要修改)
|-- index.js: 指定的后台服务的端口号和静态资源文件夹
|-- node_modules
|-- src : 源码文件夹
|-- components: vue 组件及其相关资源文件夹
|-- App.vue: 应用根主组件
|-- main.js: 应用入口 js
|-- static: 静态资源文件夹
|-- .babelrc: babel 的配置文件
|-- .eslintignore: eslint 检查忽略的配置
|-- .eslintrc.js: eslint 检查的配置
|-- .gitignore: git 版本管制忽略的配置
|-- index.html: 主页面文件
|-- package.json: 应用包配置文件
|-- README.md: 应用描述说明的 readme 文件
```



### 打包发布

```js
//打包:
npm run build
//发布 1: 使用静态服务器工具包
npm install -g serve
serve dist
//http://localhost:5000
```



### 组件

#### vue文件的组成



```js
// 1 模板页面
<template>

</template>
// 2 js模块对象
<script>

</script>
// 3 样式
<style scoped>

</style>

```



#### 使用

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210324204353.png)



组件会放在 componenets 目录下

#### main.js



```js
// 入口js 左边大写
import Vue from 'vue'
import App from './App'

Vue.config.productionTip = false


new Vue({
  el: '#app',
  components: { App },
  template: '<App/>'
})

```

#### 如何引入组件

1.导入

2.映射

3.使用

```vue
<template>
  <div>
    <img src="./assets/logo.png">
    <!--3.使用组件标签-->
    <HelloWord></HelloWord>
  </div>
</template>

<script>
  // 1.引入
  import HelloWord from './components/HelloWord'
  export default {
    components: {HelloWord},
    comments: {
      // 2.映射组件标签
      HelloWord
    }
  }

</script>

<style>

</style>

```



### 组件通信

1)props
2)vue 的自定义事件
3)消息订阅与发布(如: pubsub 库)
4)slot
5)vuex()



#### props



1.

```vue
<my-component name='tom' :age='3' :set-name='setName'></my-component>
```



2.

方式一: 只指定名称
props: ['name', 'age', 'setName']



方式二: 指定名称和类型
props: {
name: String,
age: Number,
setNmae: Function
}

方式三: 指定名称/类型/必要性/默认值
props: {
name: {type: String, required: true, default:xxx},
}





##### 注意

只可以在父子组件间进行数据传递





#### 自定义事件



##### 绑定事件监听



```js
// 方式一: 通过 v-on 绑定
@delete_todo="deleteTodo"
// 方式二: 通过$on()
this.$refs.xxx.$on('delete_todo', function (todo) {
this.deleteTodo(todo)
})
```

##### 触发事件监听



```js
// 触发事件(只能在父组件中接收)
this.$emit(eventName, data)
```

##### 注意

*用于子组件向父组件发送消息(数据)*



#### pubsub 



##### **安装**

```js
npm info pubsub-js

npm install --save pubsub-js
    
    
npm fund
```





##### 发布 // 触发事件

```js

import pubSub from "pubsub-js"

pubSub.PubSub.publish('addToDo',todo)
```





##### 订阅 // 绑定事件

```js
pubSub.PubSub.subscribe('addToDo', (msg, todo) => {

      this.todos.unshift(todo)
    })
```







## ajax





### axios使用

#### 安装

```js
npm install axios --save
```



#### 使用



```js

<script>
import axios from 'axios'
export default {
  name: 'App',
  data() {
    return {
      reponame: 'google',
      repoUrl: ''
    }
  },
  mounted () {

    const url = 'https://api.github.com/search/repositories?
    axios.get(url).then(
      response => {
        //alert('hello word')
        console.log(response.data.items[0].url)
        this.repoUrl = response.data.items[0].url
      }
    ).catch(error=> {
      console.log(error)
    })

  }

}
</script>
```





## 组件库



[elementui](https://element.eleme.cn/#/zh-CN)

[mintui](http://mint-ui.github.io/#!/zh-cn)



## 路由

### 概念

页面导航的跳转



### 使用

#### **安装**

```js
npm install vue-router --save
```





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210323003939.png)



#### 创建路由器

```js
/*
路由器模块
 */
import Vue from 'vue'
import VueRouter from 'vue-router'

import About from '../views/About'
import Home from '../views/Home'
import News from '../views/News'
import Messages from '../views/Messages'
// 3.使用
Vue.use(VueRouter)
// 默认暴露可以使用任意名字, 
// 1.创建路由器
export default new VueRouter({
  //2.路由的配置
  routes: [
    {
      path: '/',
      redirect: '/about' // 重定向
    },
    {
      path: '/about',
      component: About
    },
    {
      path: '/home',
      component: Home,
      // childern 一个页面又有路由
      children: [
        {
          path: '/home',
          redirect: '/home/news'
        },
        {
          path: '/home/messages',
          component: Messages
        },
        {
          path: '/home/news',
          component: News
        }
      ]
    }
  ]
})


```

#### 注册路由



```js
import Vue from 'vue'
import App from './App'
import router from './router'

// 声明使用插件， 内部就会给vm 和组件对象添加要给$http对象

new Vue({
  el: '#app',
  components: {
    App
  },
  template: '<App/>',
  // 4。注册路由
  router
})

```



#### 使用



```js
1. <router-link>: 用来生成路由链接
<router-link to="/xxx">Go to XXX</router-link>
2. <router-view>: 用来显示当前路由组件界面
<router-view></router-view>
```





```js
<template>
  <div>
    <div class="row">
      <div class="col-xs-offset-2 col-xs-8">
        <div class="page-header"><h2>Router Test</h2></div>
      </div>
    </div>

    <div class="row">
      <div class="col-xs-2 col-xs-offset-2">
        <div class="list-group">
          <!--生成路由链接-->
          <router-link to="/about" class="list-group-item">About</router-link>
          <router-link to="/home" class="list-group-item">Home</router-link>
        </div>
      </div>
      <div class="col-xs-6">
        <div class="panel">
          <div class="panel-body">
            <!--显示当前组件-->
            <keep-alive>
              <router-view msg="abc"></router-view>
            </keep-alive>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style scoped>

</style>
```



#### 选中路由配置



```css
 .router-link-active {
        color: red !important;
}
```

默认是router-link-active，也可以linkActiveClass: 'active', // 指定选中的路由链接的 class



### 嵌套

```js
{
      path: '/home',
      component: Home,
      children: [
        {
          path: '/home',
          redirect: '/home/news'
        },
        {
          path: '/home/messages',
          component: Messages,
          children: [
            {
              // 占位符
              path: '/home/message/detail/:id',
              component: MessageDetail
            }
          ]
        }
```



### 传递数据





```js
{
    path: '/home/message/detail/:id',
    component: MessageDetail
 }
```



#### 路径

```js

<router-link :to="'/home/message/mdetail/'+m.id">{{m.title}}</router-link>

```

#### 路由组件中读取请求参数

this.$route.params.id



*query: ?*

*params: /3*



### 路由组件的缓冲

默认是每次切换都会销毁



```js
<keep-alive>
	<router-view></router-view>
</keep-alive>
```



### 编程式路由导航

```js
1)this.$router.push(path): 相当于点击路由链接(可以返回到当前路由界面)
2)this.$router.replace(path): 用新路由替换当前路由(不可以返回到当前路由界面)
3)this.$router.back(): 请求(返回)上一个记录路由
4)this.$router.go(-1): 请求(返回)上一个记录路由
5)this.$router.go(1): 请求下一个记录路由
```











## vuex



### 概念

对 vue 应用中多个组件的共享状态进行集中式的管理(读/写)



state:

vuex 管理的状态对象







actions:

1)包含多个事件回调函数的对象
2)通过执行: commit()来触发 mutation 的调用, 间接更新 state
3)谁来触发: 组件中: $store.dispatch('action 名称', data1)// 'zzz'
4)可以包含异步代码(定时器, ajax)





mutations:

1)包含多个直接更新 state 的方法(回调函数)的对象
2)谁来触发: action 中的 commit('mutation 名称')
3)只能包含同步的代码, 不能写异步代码



getters:

1)包含多个计算属性(get)的对象
2)谁来读取: 组件中: $store.getters.xxx



### 安装



```js
npm install --save vuex
```



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210323223307.png)





### 使用



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210324195830.png)



#### *index.js*

向外暴露store



```js
import Vue from 'vue'
import Vuex from 'vuex'
import state from './state'
import mutations from './mutations'
import actions from './actions'
import getters from './getters'

Vue.use(Vuex)


export default new Vuex.Store({
  state,
  mutations,
  actions,
  getters
})

```

#### *state.js*

```js

export default {
  todos: []
}

```

#### *actions.js*



```js
import {ADD_TODO, DELETE_TODO, SELECT_ALL, DELETE_COMPLETE_TODOS, RECEIVE_TODOS} from "./mutation-types"
import storageUtils from "../utils/storageUtils";
export default {

  addToDo({commit}, todo) {

    commit(ADD_TODO, {todo})
  },
  delete_todo({commit}, index) {
    commit(DELETE_TODO, {index})
  },
  selectAll({commit}, check) {
    commit(SELECT_ALL, {check})
  },
  deleteCompleteTodos({commit}) {
    commit(DELETE_COMPLETE_TODOS)
  },
  reqToDos({commit}) {
    setTimeout(() => {
      const todos = storageUtils.readTodos()
      commit(RECEIVE_TODOS, {todos})
        
    }, 1000)
  }
}

```



#### *mutations.js*

```js
import {ADD_TODO, DELETE_TODO, SELECT_ALL, DELETE_COMPLETE_TODOS, RECEIVE_TODOS} from './mutation-types'
import storageUtils from "../utils/storageUtils";

export default {
  [ADD_TODO] (state, {todo}) {

    state.todos.unshift(todo)
    console.log(state.todos)
  },
  [DELETE_TODO] (state, {index}) {
    state.todos.splice(index, 1)
  },
  [SELECT_ALL] (state, {check}) {
    state.todos.forEach(todo => todo.complete = check)
  },
  [DELETE_COMPLETE_TODOS] (state) {
    state.todos = state.todos.filter(todo => !todo.complete)
  },
  [RECEIVE_TODOS] (state, {todos}) {
    state.todos = todos
  }
}

```

#### *getters.js*



```js
export default {
  totalCount(state) {
    return state.todos.length
  },
  completeCount(state) {
    return state.todos.reduce((preTotal, todo) => preTotal + (todo.complete ? 1 : 0),
      0)
  },
  isAllSelect(state, getters) {
    return getters.totalCount === getters.completeCount && state.todos.length > 0
  }

}

```

#### *mutation-types.js*



```js
export const ADD_TODO = 'add_todo'
export const DELETE_TODO = 'delete_todo'
export const SELECT_ALL = 'select_all'
export const DELETE_COMPLETE_TODOS = 'deleteCompleteTodos'
export const RECEIVE_TODOS = 'receiveTodos'

```





#### *main.js*

映射store

```js
import Vue from 'vue'
import App from './App'
import store from './store'

new Vue({
  el: '#app',
  components: {
    App
  },
  template: '<App/>',
  store
})

```



this.$store.dispatch('reqToDos')

分发，去触发action

```js
export default {
  name: 'App',
  components: {
    ToDoHeader,
    ToDoList,
    ToDoFooter
  },
  mounted() {
    this.$store.dispatch('reqToDos')

  }

  
}
```



#### 简化版



```js
import {mapState, mapActions, mapGetters} from 'vuex'
export default {
  name: 'App',
  computed: {
    evenOrOdd() {
      return this.$store.getters.evenOrOdd
    },
    ...mapState(['count']), // {'count'}
    ...mapGetters(['evenOrOdd'])
  },
  methods: {
    ...mapActions(['incr', 'decr', 'incrIfOdd', 'incrAsync'])
  }
```









```js

<template>
  <div>
    <p>click {{ count }} is {{ evenOrOdd }}</p>
    <button @click="incr">+</button>
    <button @click="decr">-</button>
    <button @click="incrIfOdd">incr if odd</button>
    <button @click="incrAsync">incr async</button>
  </div>
</template>

<script>
import {mapState, mapActions, mapGetters} from 'vuex'
export default {
  name: 'App',
  computed: {
    evenOrOdd() {
      return this.$store.getters.evenOrOdd
    },
    ...mapState(['count']), // {'count'}
    ...mapGetters(['evenOrOdd'])
  },
  methods: {
    ...mapActions(['incr', 'decr', 'incrIfOdd', 'incrAsync'])
  }
  /*methods: {
    incr() {
      //
      // 触发 store 中对应的 action 调用
      this.$store.dispatch('incr')

    },
    decr() {
      this.$store.dispatch('decr')
    },
    incrIfOdd() {
      /!*const count = this.count;
      if (count % 2 != 0) {
        this.count = count + 1
      }*!/
      this.$store.dispatch('incrIfOdd')
    },
    incrAsync() {
      /!*setTimeout(() => {
        const count = this.count;
        this.count = count + 1
      }, 100)*!/
      this.$store.dispatch('incrAsync')
    }
  }*/
}
</script>

<style>

</style>

```

## **error**

**Errors: 1 http://eslint.org/docs/rules/no-multiple-empty-lines**

vue启动（npm run dev）报错

*解决方法，找到 config–>index.js文件里的useEslint：true 改为useEslint ：false*







## end





```js
const {comment,index,deleteComment} = this  
上面的这句话是一个简写，最终的含义相当于 
const  comment = this.comment 
const  index = this.index const   
deleteComment = this.deleteComment
```









### 开发思路

某个组件需要还是某些组件需要

某些需要咋放在App.vue(父组件)



函数大写

对象小写

js中引入常量作为方法名加[]



reduce find filter sort, map,









