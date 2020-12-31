





java.sql.SQLException: Access denied for user 'root'@'localhost' (using password: YES)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:957) ~[mysql-connector-java-5.1.38.jar!/:5.1.38]



```mysql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'127.0.0.1' IDENTIFIED BY 'root';
```





```java
spring.config.additional-location=
```

