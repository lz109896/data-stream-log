# SQL语句强化练习题

#### 1、列出全部学生的信息。(表名：学生表。字段名：学号，性别，姓名，专业。)

SELECT * FROM 学生表

#### 2、列出软件专业全部学生的学号及姓名。(表名：学生表。字段名：学号，性别，姓名，专业。)

SELECT 学号,姓名 FROM 学生表 WHERE 专业='软件'

#### 3、求1号课成绩大于80分的学生的学号及成绩，并按成绩由高到低列出。（表名：成绩表。字段名：课号，学号，成绩。）

SELECT 学号,成绩 FROM 成绩表 WHERE 课号=1 AND 成绩>80 ORDER BY 成绩 DESC

#### 4、列出非软件专业学生的名单。(表名：学生表。字段名：学号，性别，姓名，专业。)

SELECT 姓名 FROM 学生表 WHERE  专业 not in ('软件')

#### 5、查询成绩在70~80分之间的学生选课得分情况。（表名：选课表。字段名：课号，学号，成绩。）

SELECT * FROM 选课表 WHERE 成绩 BETWEEN 70 AND 80

#### 6、列出选修1号课或3号课的全体学生的学号和成绩。（表名：选课表。字段名：课号，学号，成绩。）

方法一：SELECT 学号,成绩 FROM 选课表 WHERE 课号=1 OR 课号=3

方法二：SELECT 学号,成绩 FROM 选课表 WHERE 课号 IN (1,3)

#### 7、列出所有98级学生的学生成绩情况。（表名：选课表。字段名：课号，学号，成绩，班级。）

SELECT * FROM 选课表 WHERE 学号 LIKE "98%"

#### 8、列出成绩为空值(或不为空值)的学生的学号和课号。（表名：选课表。字段名：课号，学号，成绩。）

答案一：SELECT 学号,课号 FROM 选课表 WHERE 成绩 IS NULL

答案二：SELECT 学号,课号 FROM 选课表 WHERE 成绩 IS NOT NULL

#### 9、求出所有学生的总成绩。（表名：选课表。字段名：课号，学号，成绩。）

SELECT SUM(成绩) AS 总成绩 FROM 选课表

#### 10、列出每个学生的平均成绩。（表名：选课表。字段名：课号，学号，成绩。）

SELECT 学号,AVG(成绩) AS 平均成绩 FROM 选课表 GROUP BY 学号

#### 11、列出各科的平均成绩、最高成绩、最低成绩和选课人数。（表名：选课表。字段名：课号，学号，成绩。）

SELECT 课号,AVG(成绩) AS 平均成绩,MAX(成绩) AS 最高分,MIN(成绩) AS 最低分,COUNT(学号) AS 

选课人数 

FROM 选课表 GROUP BY 课号

#### 12、列出选修1号课的学生姓名及成绩。【表名：学生表（字段名：学号，性别，姓名，专业。）】；【表名：成绩表（字段名：课号，学号，成绩。）】

SELECT 姓名,成绩 FROM 学生表,成绩表 WHERE 学生表.学号=成绩表.学号 AND 课号=1

#### 13、列出选修1号课的学生的学号、姓名及成绩。【表名：学生表（字段名：学号，性别，姓名，专业。）】；【表名：成绩表（字段名：课号，学号，成绩。）】

SELECT 学生表.学号,姓名,成绩 FROM 学生表,成绩表 WHERE 学生表.学号=成绩表.学号 AND 课号=1

#### 14、求出总成绩大于150的学生的学号、姓名及总成绩。【表名：学生表（字段名：学号，性别，姓名，专业。）】；【表名：成绩表（字段名：课号，学号，成绩。）】
```
select a.学号,a.姓名, sum (b.成绩) 
from 学生表 a,成绩表 b
group by a.学号,a.姓名
having sum (b.成绩) > 150 ;
```
#### 15, 数据库表Book，字段BookID，Bookname，Price，PublicID，表出版社Public，字段PublicID，

PublicName，PublicTEL

#### 1，查询出Book表Price超过20元的书，按BookID降序。

```
SELECT 	Bookname
FROM book WHERE price>20 
ORDER BY BookID DESC
```

#### 2，统计出每个出版社里所有书Book的平均价格Price。（表Book，字段BookID，Bookname，Price，PublicID，）
```
select publicname,avg(price) 
from book,public where book.publicID =public.publicID 
group by publicname.

```

#### 3，所有书价格下调5%。

update book set price=0.95*price  


#### 16、下面是一个“学生与课程”的数据库，三个关系模式为：
```
学生关系模式S(S#,SNAME,AGE,SEX)
成绩关系模式SC(S#,C#,GRADE)
课程关系模式C(C#,CNAME,TEACHER)
其中S#为学号，SNAME为学生名字，AGE为年龄，SEX为性别，C#为课程号，CNAME为课程名，GRADE为

成绩，TEACHER为教师名。
```
## 请用SQL完成下面的查询：
#### A)查询学习课程号为C2的学生学号与成绩
```
select S.S#, GRADE 
from S,SC 
where S.S#= SC.S# 
AND C#='C2'
```
#### B)查询姓名以字符D打头的学生姓名。
```
SELET SNAME
FROM S
WHERE SNAME LIKE 'D%'
```

#### C)查询选修课程名为Maths的学生学号与姓名。
```
SELET S.S#,SNAME
FROMS,SC,C
WHERES.S#=SC.S#
AND SC.C#=C.C#
and CNAME='Maths';
```
#### D)查询选修课程号为C2和C4的学生学号。

```
S4ELET S# 
FROM SC , C 
WHERE SC,C#=C.C# 
AND C.C# IN ('C2','C4')
```


#### 17 ,数据库测试题：
```
Student（S#,Sname，Sage，Ssex） 学生表
Course（C#, Cname ,T#） 课程表
SC（S#, C#, score）成绩表
Teacher （T#, Tname） 教师表
其中S#为学号,C#为课程号,SNAME为学生名字，
```
#### 1，查询 '001' 课程比 '002' 课程成绩高的所有学生的学号；
```
SELECT a.S#, a.C#,b.C#, a.score,b.score FROM  SC  a , SC b  where a.S# = b.S#
and a.C# = '01' and b.C# = '02' and  a.score> b.score;

select  a.S#, a.C#,b.C#, a.score,b.score
FROM (select S#,C#, score from SC where C# = '01') as a ,
(select S#, C#,score from SC where C# = '02') as b
WHERE a.S#=b.S# and a.score> b.score ;
```
#### 2，查询平均成绩大于60分的同学的学号和平均成绩；
```
select S#,  AVG(score) 
from  SC 
GROUP BY  S# 
HAVING  AVG(score)> 60;
```
#### having 用法与WHER法类似，但有三点不同:
```
1、HAVING只用于GROUP BY（分组统计语句），
2、WHERE 是用于在初始表中筛选查询，HAVING用于在WHERE和GROUP BY 结果中查询。
3、HAVING可以使用聚合函数，而WHERE 不能。
```
#### 下面的语句统计用户表中姓名为“李”（WHERE子句定义），出现多于一次(having 用聚合函数
```
COUNT(1)定义）的人的用户
SELECT USERCODE,username=max(username),次数=count(1) 
from usertable
 where username like '李%'   
group by usercode 
having count(1)>1
```
#### 3，查询所有同学的学号，姓名，选课数，总成绩；
```
SELECT a.S#,a.Sname , COUNT(b.C#), SUM (b.score) 
from  Student a, SC b
WHERE a.S#= b.S#
GROUP BY a.S#,a.Sname ;
```

#### 4，查询学过'叶平'老师所教的所有课的同学的学号，姓名；
```
select  aa.S#,aa.Sname  from  Student aa, Course bb,   SC cc , Teacher dd
WHERE aa.S#=cc.S# and  bb.C#=cc.C#  and  bb.T#=dd.T# and dd.Tname='叶平'
GROUP BY aa.S#,aa.Sname
HAVING COUNT (cc.C#)=
(SELECT  COUNT(a.C#)  FROM Course a , Teacher b WHERE  a.T# =b.T# and b.Tname='叶平')

```
#### 分开三句话理解：
```
1,2行.........上过叶平的课的学生
3，4行......，叶平所教过的课的数量
5，行...........学生所上过叶平课的数量 = 叶平所教过的课的数量
```
#### 5，查询所有课程成绩小于60分的同学的学号，姓名
```
select a.S#,a.Sname ,MAX (b.score)  from  Student  a,  SC  b where a.S#=b.S#

GROUP BY  a.S#,a.Sname HAVING MAX (b.score)< 60
```
#### 6，删除学习'叶平'老师课的SC 表记录；

```
DELETE from  SC WHERE  S# 
in
(select a.S# from   Teacher a,  Course b, SC c 
WHERE a.T#=b.T# and  b.C#=c.C#  and  a.Tname='叶平')
```


#### 7，查询各科成绩最高和最低的分：以如下形式显示：课程ID, 最高分，最低分。


> SELECT C# as 课程ID , MAX (score) 最高分 , MIN (score) 最低分 FROM  SC GROUP BY C# 
































