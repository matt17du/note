![](https://raw.githubusercontent.com/matt17du/img/main/img/20210325191454.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210325191742.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210325192118.png)





flask-wtf

flask-sqlalch

mysql-client





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210325192524.png)









### ImportError: No module named MySQLdb 解决方案



MySQLdb只支持Python2.*，还不支持3.*可以用PyMySQL代替

安装pymysql



```python
pip install PyMySQL
```



在app.py添加如下代码

```python
import pymysql

pymysql.install_as_MySQLdb()
```





```python
from app import db, app
db.create_all(app=app)
```



flask-cors







