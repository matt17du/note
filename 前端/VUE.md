### 基本使用

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





输入vue

```js
npm install -g vue-cli
```







![](https://raw.githubusercontent.com/matt17du/img/main/img/20210319233446.png)



不使用测试

不使用vue-router

