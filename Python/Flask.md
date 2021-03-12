Python Web 实现的开发框架

小而美，丰富的周边扩展





```pyt
pip install flask
```





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