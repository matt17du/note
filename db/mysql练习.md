已知有如下4张表：

学生表：student(学号,学生姓名,出生年月,性别)

成绩表：score(学号,课程号,成绩)

课程表：course(课程号,课程名称,教师号)

教师表：teacher(教师号,教师姓名)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210309113134.png)



成绩表

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210309113215.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210309113254.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210309113326.png)



数据的插入

```mysql
INSERT INTO student (id, name, birth, sex)
VALUES (0001, 'matt', '1998-09-05', 1)

INSERT INTO student(id, name, birth, sex) 
VALUES(2, 'pavi', '2003-05-01', 0)


INSERT INTO student (id, name, birth, sex)
VALUES (3, '小明', '1994-09-05', 1)

INSERT INTO student(id, name, birth, sex) 
VALUES(4, '李华', '2005-08-15', 0)

INSERT INTO score(student_id, course_id, score)
VALUES(1, 1, 100)
INSERT INTO score(student_id, course_id, score)
VALUES(1, 2, 89)
INSERT INTO score(student_id, course_id, score)
VALUES(1, 3, 65)

INSERT INTO score(student_id, course_id, score)
VALUES(2, 1, 99);
INSERT INTO score(student_id, course_id, score)
VALUES(2, 2, 77);
INSERT INTO score(student_id, course_id, score)
VALUES(2, 3, 65);

INSERT INTO score(student_id, course_id, score)
VALUES(3, 1, 99);
INSERT INTO score(student_id, course_id, score)
VALUES(3, 2, 97);
INSERT INTO score(student_id, course_id, score)
VALUES(3, 3, 98);

INSERT INTO course(id, name, teacher_id)
VALUES(1, '语文', 1);
INSERT INTO course(id, name, teacher_id)
VALUES(2, '数学', 2);
INSERT INTO course(id, name, teacher_id)
VALUES(3, '日语', 3);


INSERT INTO teacher(id, name)
VALUES(1, '苏轼');
INSERT INTO teacher(id, name)
VALUES(2, '华罗庚');
INSERT INTO teacher(id, name)
VALUES(3, 'trump');

```

### 1.简单查询

查询姓“猴”的学生名单

```mysql
SELECT id, name, birth, sex
FROM student
WHERE name = '侯%'

SELECT id, name, birth, sex
FROM student
WHERE name like '%明' #like

SELECT id, name, birth, sex
FROM student
WHERE name like '%明%' #like
```



查询姓“孟”老师的个数

```mysql
SELECT count(id)
FROM student
WHERE name like '%明%'
```

### 2.汇总分析

查询课程编号为“0002”的总成绩

```mysql
SELECT sum(score)
FROM score
WHERE course_id = 2
```

查询选了课程的学生人数

```java
SELECT count(DISTINCT student_id) AS 'student_count'
FROM score
```

#### 分组

查询各科成绩最高和最低的分， 以如下的形式显示：课程号，最高分，最低分

```mysql
SELECT course_id, max(score), min(score)
FROM score
GROUP BY course_id
```

查询每门课程被选修的学生数

```mysql
SELECT course_id, count(student_id)
FROM score
GROUP BY course_id
```

查询男生、女生人数

```mysql
SELECT sex, count(id) # 有性别字段
FROM student
GROUP BY sex
```

#### 分组结果的条件

查询平均成绩大于60分学生的学号和平均成绩

```mysql
SELECT student_id, avg(score)
FROM score
GROUP BY student_id
HAVING avg(score) > 60
```

查询至少选修两门课程的学生学号

```mysql
SELECT count(course_id)
FROM score
GROUP BY student_id
HAVING count(course_id) >= 2
```

**查询同名同姓学生名单并统计同名人数**

```mysql
SELECT name, count(*) as student_count
FROM student
GROUP BY name # name不加''
HAVING COUNT(*) >= 2
```

查询不及格的课程并按课程号从大到小排列

```mysql
SELECT DISTINCT course_id
FROM score
WHERE score < 60
ORDER BY course_id desc
```

查询每门课程的平均成绩，结果按平均成绩升序排序，平均成绩相同时，按课程号降序排列

```mysql
SELECT course_id, AVG(score) as avg_score
FROM score
GROUP BY course_id
ORDER BY avg_score asc, course_id desc
```

检索课程编号为“0004”且分数小于60的学生学号，结果按按分数降序排列

```mysql
SELECT student_id
FROM score
WHERE course_id = 3 AND score > 60
```

统计每门课程的学生选修人数(超过2人的课程才统计)

要求输出课程号和选修人数，查询结果按人数降序排序，若人数相同，按课程号升序排序

```mysql
SELECT course_id,count(student_id) as student_count
FROM score
GROUP BY course_id
HAVING count(student_id) > 2
ORDER BY student_count desc, course_id asc
```

查询两门以上不及格课程的同学的学号及其平均成绩

```mysql
SELECT student_id , avg(score) as 'avg_score'
FROM score
WHERE score < 60
GROUP BY student_id
HAVING count(score) > 2
```

#### 查询结果排序分组指定条件

查询学生的总成绩并进行排名

```mysql
SELECT student_id, sum(score) AS "sum_score"
FROM score
GROUP BY student_id
ORDER BY sum_score desc
```

查询平均成绩大于60分的学生的学号和平均成绩

```mysql
# 查询平均成绩大于60分的学生的学号和平均成绩
SELECT student_id, avg(score) AS "avg_score"
FROM score
GROUP BY student_id
HAVING avg_score > 60
```

### 3.复杂查询

查询所有课程成绩小于60分学生的学号、姓名

```mysql
# 查询所有课程成绩小于60分学生的学号、姓名
SELECT id, `name`
FROM student
WHERE id in (
	SELECT DISTINCT student_id
	FROM score
	WHERE score < 60
)

```

查询没有学全所有课的学生的学号、姓名

```mysql
SELECT id, name
FROM student
WHERE ID IN (
	SELECT student_id
	FROM score
	GROUP BY student_id
	HAVING COUNT(student_id) < (
		SELECT COUNT(ID)
		FROM course
	)
)
```

查询出只选修了两门课程的全部学生的学号和姓名

```mysql
SELECT id, name
FROM student
WHERE ID IN (
	SELECT student_id
	FROM score
	GROUP BY student_id
	HAVING COUNT(student_id) = 2  # 没有==
)

```

日期函数

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210310105753.png)



1990年出生的学生名单

```mysql
SELECT id, `name`
FROM student
WHERE YEAR(birth) > 100
```

查询各学生的年龄（精确到月份）

```mysql
# 查询各学生的年龄（精确到月份）
SELECT ID, TIMESTAMPDIFF(month, birth, now()) / 12
FROM student

```

查询本月过生日的学生

```mysql
SELECT id, `name`
FROM student
WHERE MONTH(birth) = MONTH(CURRENT_DATE)
```

#### TOPN

```mysql
#没有俩个第一名
SELECT course_id, max(score) as "MAX_SCORE"
FROM score
GROUP BY course_id
# 可以有俩个第一名
SELECT score1.*
FROM score AS score1
WHERE score = (
	SELECT MAX(score2.score)
	FROM score AS score2
	WHERE score1.course_id = score2.course_id
)

(SELECT *
FROM score
WHERE course_id = 1
ORDER BY score DESC
LIMIT 2)
UNION ALL 
(SELECT *
FROM score
WHERE course_id = 2
ORDER BY score DESC
LIMIT 2)

# 记得上括号

```

### 4.多表查询

查询所有学生的学号、姓名、选课数、总成绩

```mysql
# 查询所有学生的学号、姓名、选课数、总成绩 ON
SELECT st.id, st.name, COUNT(sc.student_id), sum(sc.score)
FROM student as st
LEFT JOIN score as sc
ON st.id = sc.student_id
GROUP BY sc.student_id
```

查询平均成绩大于85的所有学生的学号、姓名和平均成绩

```mysql
#查询平均成绩大于85的所有学生的学号、姓名和平均成绩
SELECT student.*, AVG(score.score)
FROM student
LEFT JOIN score
ON student.id = score.student_id
GROUP BY student_id
HAVING AVG(score) > 60
```

查询学生的选课情况：学号，姓名，课程号，课程名称

```mysql
# 选课情况
SELECT student.id, student.name, course.id, course.name
FROM student
INNER JOIN score
ON student.id = score.student_id
INNER JOIN course
ON score.course_id = course.id

SELECT SUM(0)
FROM STUDENT
```

查询出每门课程的及格人数和不及格人数

```mysql
# 几个人数和不及格人数 忘记写end

SELECT course_id,
	sum(CASE WHEN score >= 60 THEN 1 ELSE 0 END),
	SUM(CASE WHEN score < 60 THEN 1 ELSE 0 END)
FROM score
GROUP BY course_id;


SELECT course_id,
	sum(CASE WHEN score BETWEEN 60 AND 100 THEN 1 ELSE 0 END),
	SUM(CASE WHEN score < 60 THEN 1 ELSE 0 END)
FROM score
GROUP BY course_id;

```

查询课程编号为0003且课程成绩在80分以上的学生的学号和姓名

```mysql
# 查询课程编号为0003且课程成绩在80分以上的学生的学号和姓名
SELECT student.id, student.name
FROM student
INNER JOIN score
ON student.id = score.student_id
WHERE score.course_id = 2 AND score.score > 80
```

#### sql的行列转换

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210310110422.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210310110459.png)





```mysql
SELECT student_id, 
	MAX(CASE course_id WHEN 1 THEN score ELSE 0 END) AS 'couse_1',
	MAX(CASE course_id WHEN 2 THEN score ELSE 0 END) AS 'couse_2',
	MAX(CASE course_id WHEN 3 THEN score ELSE 0 END) AS 'couse_3'
FROM score
GROUP BY student_id
```





### 多表连接



### 参考

[https://zhuanlan.zhihu.com/p/38354000](https://zhuanlan.zhihu.com/p/38354000)



查询所有课程不即可

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210310123917.png)