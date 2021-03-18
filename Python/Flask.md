

### 介绍

Python Web 实现的开发框架

小而美，丰富的周边扩展

### 安装

```pyt
pip install flask
```

验证安装成功

```python
验证
>>> import flask
>>> flask.__version__
' 1.1.2'
```

### 使用

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def test_matt():
    return 'hello'
```



*参数name*
表示应用的主模块或包的名称。使用该参数FlaskFlask确定应用的位置，然后找到应用中其他文件的位置，如网页中的图片目录，模板目录
*装饰器app.route()*
表示一个路由配置，即：用户在浏览器输入URL，使用对应的函数处理其中的业务逻辑（可写多个）



### 启动



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210312233855.png)





启动服务器
 1.步骤1：设置环境变量

 Windows set FLASK_APP=app.py
 Linux export FLASK_APP=app.py、

 2.步骤2flask run web：启动内置服务器

指定IP及端口：
flask run host=0.0.0.0 port=8001
或：
flask run -h 0.0.0.0 -p 8001



开启调试模式

 Windows set FLASK_ENV=development

 Linux export FLASK_ENV=development



​	

### MVT模型

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210312234128.png)



视图：py中的函数

模型：mysql查询出来的



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210312234205.png)





### 路由

使用装饰器

@app.route(url_name, methods)

urlURL: 匹配的地址
methods: ['GET', 'POST']所支持的请求方式（）

实例：

@app.route('/login', methods=['GET', 'POST'])



使用API

app.add_url_rule(url_name view_name)

url : 匹配的URL地址
url_nameURL: 给的命名
view_name: 视图函数



#### 匹配规则

 匹配整个文字
@app.route('/hello')
  传递参数
@app.route('/user/<username>')
  指定参数类型
@app.route('/post/<int:post_id>')



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210312235118.png)





URL配置及路由
  查看URL规则列表
app.url_map
  URL逆向解析（根据名称解析成字符串）URL
<1>url_for(url_name, **kwargs)
<2>静态文件图片(/css/js)引用
url_for('static', filename='style.css')



URL中的值
@app.route('/page/<page>')
 def list_user(page):
URL中的值为可选
@app.route('/page/<page>')
 def list_user(page=None):















模板是html



视图是py中的一个函数





匹配整个文字
@app.route('/hello')
  传递参数
@app.route('/user/<username>')
  指定参数类型
@app.route('/post/<int:post_id>')

URL中的值
@app.route('/page/<page>')
 def list_user(page):
  URL中的值为可选
@app.route('/page/<page>')
 def list_user(page=None):





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210312214009.png)



食堂是应用上下文



### 应用上下文对象

1 current_app
当前应用的实例
2 g
处理请求时的临时存储对象，每次请求都会重设这个变量

### 请求上下文

1 request
请求对象，封装了客户端发出的请求中的内容HTTP
2 session
用户会话(dict)，各请求之间的数据共享



```python
@app.route('/test/req')
def test_request():
    # print('hello test_request')
    test_args = request.args
    print(request.args.get('name', 'dmx')) #不存在就dmx
    # 主机地址
    print(request.headers)
    headers = request.headers
    print(headers.get('Host'))
    print(request.remote_addr)
    return {'name': 'matt'}
```



### 请求钩子

1.before_first_request
	服务器初始化后第一个请求到达前执行
2.before_request
	每一个请求到达前执行

3.fter_request
	每次请求处理完成后执行，如果请求过程中产生了异常，则不执行
4.teardown_request
	每次请求处理完成之后执行，如果请求过程中产生了异常也执行



```python
@app.before_first_request
def first_request():
    print('服务器启动')

@app.before_request
def pre_request():
    # 钩子函数
    print('request。。。。')
```





### 响应

1.可以是字符串
2.可以是元组（）tuple
(response, status, headers) 或(response, headers)



<1>response——响应内容
<2>status——响应状态码
<3>headers——响应头信息



```python
@app.route('/test/resp')
def test_response():
    # return 'test resp', 201, {'name': 'ddd'}
    print()
    resp = make_response({'name': 'matt', 'age': 19}, 300)
    resp.headers['name'] = 'matt3343'
    resp.status_code = 200

    return resp
```



HTML

```python
@app.route('/test/html')
def test_html():
    html = render_template('index.html')
    return html
```







### 重定向

```python
@app.route('/')
def test_matt():
    return 'hello'


@app.route('/index')
def helloword():
    print(current_app)
    print('222')
    return redirect('/')
    return 'hello'
```

### 错误

```python
@app.route('/test/abort')
def test_abort():
    # 给定错误
    abort(403)
@app.errorhandler(403)
def forbidden(err):
    print(err)
    return 'xx'
```





```python
from app import db
db.create_all()
```















```python
pip install flask
pip install flask_sqlalchemy # 数据库
pip install Flask-WTF # 表单


pip install --upgrade 'SQLAlchemy<1.4'
```



