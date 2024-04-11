## MySQL

### 一、基本概念

数据库是结构化存储数据的容器，用于大量数据的存储、查询。

按照结构分，最大则是DataBase(数据库)，其次是Table(表)。

按照数据内容分(以表为单位)，表中的数据每一行为一条数据，每一列为该数据的属性，属性也称为字段。



---



### 二、数据库

#### 2.1 基本命令

##### 2.1.1 创建

```mysql
CREATE DATABASE 数据库名

CREATE DATABASE person; -- 创建一个名称为person的数据库
CREATE DATABASE IF NOT EXISTS 数据库名; -- 如果没有就创建，有就跳过。
```



##### 2.1.2 删除

```mysql
DROP DATABASE 数据库名

DROP DATABASE person;-- 删除名为person的数据库
DROP DATABASE IF EXISTS; -- 如果有就删除，没有就跳过。
```



##### 2.1.3 切换

```mysql
USE 数据库名

USE person;	-- 切换到person数据库。
```



---



### 三、表

> 字段为表的一列的列明

#### 3.1 基本命令

##### 3.1.1 创建

```mysql
CREATE TABLE 表名(字段名 数据类型[约束]);

CREATE TABLE person_info(	-- 创建一个person_info表
	id 		int 	PRIMARY KEY AUTO_INCREMENT,	-- 主键、自增
    name	varchar(20) NOT NULL,	-- 非空
	sex		char(1),
    birthday datatime,
    remark	text	-- 注意最后一个没有逗号
);
```

###### 根据查询结果生成新表

```mysql
CREATE table 新表表名 查询语句

CREATE table table_2 
SELECT SUM(ClassHour) as 总课时 ，
AVG(ClassHour) as 平均课时 
FROM subject;
```



##### 3.1.2 删除

```mysql
DROP TABLE 表名;

DROP TABLE IF clazz;	-- 删除表clazz
DROP TABLE IF EXISTS clazz; -- 如果存在就删除
```





#### 3.2 数据操作命令

##### 3.2.1 新增

###### 单条

```mysql
INSERT INTO 表名(字段名)
VALUES(值1,值2,值3,值4,值5,值6);

INSERT INTO person_info(id,name,age,sex,birthday,remark)
VALUES(1,'张三',29,'男','1999-10-01','我是谁？');

INSERT INTO person_info(id,name,sex,birthday,remark)
VALUES(2,'貂蝉',18,'女','2004-05-23','我是谁');
```

###### 多条

```mysql
INSERT INTO 表名(字段名)

INSERT INTO person_info(id,name,age,sex,birthday,remark)
VALUES (3,'叶孤城',27,'男','1995-08-15','我是谁'),
       (4,'陆小凤',20,'女','2002-03-23','我是谁');	-- 最后一句加分号，前面加逗号。
```



##### 3.2.2 删除

```mysql
DELETE FROM 表名 WHERE 值名 = 值;

DELETE FROM person_info WHERE id = 1; -- 删除表person_info中id为1的数据
```

###### TRUNCATE

> 无法恢复的删除

```mysql
TRUNCATE TABLE 表名;
TRUNCATE TABLE person_info;
```



##### 3.2.3 修改

```mysql
UPDATE 表名 SET 字段名(值名) = 新的值 WHERE 要修改的值名;

UPDATE person_info SET age = 28 WHERE id = 1;	-- 将person_info表中id为1的age修改为28
```



##### 3.2.4 查询

```mysql
SELECT 字段名(列名) FROM 表名;

SELECT GradeName FROM grade;
SELECT grade.GradeName FROM grade;	-- 可以用表名打点来看有哪些字段
```

###### 多字段查询

```mysql
SELECT 字段1，字段2 FROM 表名；

SELECT GradeId,GradeName FROM grade;
```

###### 查询MD5对应字符串

```mysql
SELECT MD5("数据") FROM 表名

-- 查询12345对应MD5
SELECT MD5("12345") FROM dual
```





#### 3.3 联表查询

##### 3.3.1 普通查询

```mysql
SELECT 要查询的列名 FROM 表1，表2	-- 联表查询至少要有两个表
WHERE 两个表去重的"="判断 AND 排除某些数据的语句;

-- 查询学号，学生姓名。年纪名称，年级Id，从学生表和年级表并且年级名为S2的所有数据
SELECT s.StudentNo,s.StudentName,g.GradeName,g.GradeId -- 直接使用别名
FROM student s,grade g	-- 表1 别名，表2 别名	别名为了避免两个表都有同一个列名数据库不知道查询哪个
WHERE s.GradeId = g.GradeId		-- 去重，避免笛卡尔积
AND g.GradeName = 'S2';
```



##### 3.3.2 INNER JOIN

> 内连接

```mysql
SELECT s.StudentNo,s.StudentName,g.GradeName,g.GradeId 
FROM student s 
INNER JOIN grade g	-- INNER可以去掉
on(s.GradeId = g.GradeId)	-- 跟where功能一致 必须使用在联表查询中
AND g.GradeName = 'S2';		-- on可以在联表查询中代替where，也可以使用where不用on
```



##### 3.3.3 OUTER JOIN

> 外连接，可以避免值为NULL的去重后不显示
>
> 一个表作为主表(驱动表)会将数据全部查询出来，即使从表(被驱动表)没有数据
>
> 主表：FROM 表名	从表：LEFT OUTER/RIGHT OUTER  JOIN 表名 
>
> OUTER可以省略，外连接不能用where
>
> 简要记忆：左连接FROM后面的表是主表，右连接JOIN后面的表是主表

###### 左外连接

```mysql
/*LEFT OUTER 左外连接*/
SELECT s.StudentNo,s.StudentName,g.GradeName,g.GradeId 
FROM student s 		-- 主表(驱动表)
LEFT OUTER JOIN grade g		-- 从表(被驱动表)	-- 将INNER改为LEFT OUTER
on(s.GradeId = g.GradeId)	
AND g.GradeName = 'S2';		
```

###### 右外连接

```mysql
/*RIGHT OUTER 右外连接*/
SELECT s.StudentNo,s.StudentName,g.GradeName,g.GradeId 
FROM student s 		-- 从表(被驱动表)
RIGHT OUTER JOIN grade g		-- 主表(驱动表)	-- 将INNER改为RIGHT OUTER
on(s.GradeId = g.GradeId)	
AND g.GradeName = 'S2';	
```



##### 3.3.4 多表查询不同数据

```mysql
SELECT 表一别名.*,表二别名.字段名
```





#### 3.4 set @name

> 定义内部变量

```mysql
-- 定义一个用户变量，范围只要不关闭会话(数据库)
set @name = 'java'; -- 关闭后默认值为NULL
SELECT @name;	-- java
```



---



### 四、关键字

#### 4.1 AS

> 表、字段、等重命名(备注)。keyi理解为别名，将长的名字简化，使SQLkanqi来更简洁
>
> 只修改查询出来的结果集，不会实际修改表中的字段。

##### 4.1.1 查询结果字段重命名

```mysql
SELECT 字段名 AS '新字段名',GradeName AS '新字段名' FROM 表名;

SELECT GradeId AS '年级编号',GradeName AS '年级名称' FROM grade;	-- 将GradeId 改成年级编号
```



##### 4.1.2 表重命名

```mysql
SELECT 表别名.字段名 FROM 表名 AS 表别名

SELECT g.GradeId,g.GradeName FROM grade AS g;	-- 将grade改为g
SELECT g.GradeId,g.GradeName FROM grade g;	-- 简写，AS
```





#### 4.2 IN

> 简化筛选，让WHERE更简洁

```mysql
-- 筛选多条
SELECT * FROM student WHERE StudentNo = ‘S1201302002’ or StudentNo = ‘S1201302003’;
-- IN筛选
SELECT * FROM student WHERE StudentNo IN('S1201302002','S1201302003');
/*也可以跟子查询*/
IN(SELECT...)
```





#### 4.3 LIKE

> 模糊查询

```mysql
LIKE '模糊查询值' ;

SELECT * FROM Student WHERE StudentName LIKE '刘星' -- 只查询固定值：刘星
```

###### 通配符

> `_`、`%`、`[]`、`[^]`

```mysql
LIKE 刘_;	-- 一个字符，匹配姓刘的二字名的人
LIKE _ _江;	-- 两个字符，匹配**江三字名的人，便于观察，正常没有空格，两个“_”
LIKE 刘%;	-- 多个字符：%表示不限制字符数，匹配姓刘的所有字名长度的人
-- 如 [] 内有一系列字符（01234、abcde）则可略写为“[0-4]”、“[a-e]” 
LIKE '刘[备,秀]'	-- [1,2,3] 匹配括号中指定范围的一个字符查询(刘备或刘秀)
LIKE '刘[^备,秀]'	-- [^]匹配括号中非指定范围的一个字符：查询姓刘的非刘备、刘秀的所有结果
```





#### 4.4 GROUP BY

> 分组查询，可以理解为会将一列重复的值合并为一个，GROUP BY哪个就合并哪个，用于统计。

```mysql
SELECT ... FROM ... 
WHERE ...
GROUP BY ...	-- 多一个GROUP BY，通常与聚合函数一起使用。

-- 返回GradeId： 1 2 3
SELECT GradeId FROM student	-- 查询student(学生)表里的年级ID，按照年级Id分组(查询年级有几个ID)
GROUP BY student.GradeId;	-- 查询哪个列，GROUP BY 哪个列，查询就不能写其他列了，除了聚合函数
```

**注意**

- SELECT后面只能包含被分组(GROUP BY)的列
- 每个分组只能返回一个值的表达式，如聚合函数

```mysql
-- SELECT后添加聚合函数
SELECT GradeId,COUNT(1) FROM student	-- 查询student(学生)表里的年级Id，按照年级Id分组
GROUP BY student.GradeId;	-- 查询哪个列，GROUP BY 哪个列，查询就不能写其他列了，除了聚合函数
-- 返回GradeId：1 2 3 及 COUNT(1)各个年级的人数
```





#### 4.5 HAVING

> 分组后筛选

```mysql
SELECT GradeId,AVG(ClassHour) FROM subject -- 从subject表查询年级Id，学时平均值
GROUP BY GradeId	-- 以年级Id分组(1,2,3)	得出1,2,3年级的所有课程的平均课时(56.2,49.4,66.5)
HAVING AVG(ClassHour) > 60; -- 筛选出平均学时大于60的年级--只显示GradeId3的分数66.5
```





#### 4.6 ORDER BY

>  排序，查询后升序/降序输出

```mysql
ORDER BY 字段名 asc/desc; -- 升序/降序。默认asc，所以升序可以不写，只写ORDER BY即可。

ORDER BY StudentResult;	-- 对学生成绩进行升序输出
```





#### 4.7 LIMIT

> 分页(索引页码)

```mysql
-- 第一种写法
SELECT * FROM Student LIMIT 开始索引，页码(每页查询多少条数据) -- 第一页

SELECT * FROM Student LIMIT 0,10;  -- 跟数组一样也是从零(第一条)开始，查询10条；
SELECT * FROM student LIMIT 10,10; -- 从第11条开始，查询10条；第二页
SELECT * FROM student LIMIT 60,10; -- 从第61条开始，查询10条；第七页
SELECT * FROM student LIMIT 70,10; -- 第八页没有数据，结果集为null;

-- 分页的第二种写法
SELECT * FROM Student LIMIT 10 OFFSET 0; -- 查询几条，从哪开始
```





#### 4.8 各关键字的使用顺序

> WHERE > GROUP BY > HAVING > ORDER BY > LIMIT

```mysql
select studentNo，AVG(studentResult) from result -- 查询学号及该学号学生平均成绩
where studentResult >= 60 -- 对学生成绩进行筛选，大于60的才取平均值
GROUP BY StudentNo -- 以StudentNo(学号)进行分组
HAVING AvG(studentResult) > 80 -- 筛选分组后的平均成绩，只显示大于80的
ORDER BY AVG(StudentResult) desc --对平均学生成绩进行降序输出(从大到小)
LIMIT 1; -- 查询几条
```



---

**非必要可以不学习外键，最好不用外键，影响性能；阿里巴巴开发规范禁止使用外键。**

### 五、外键

> 为了解决数据超出设定的问题：
>
> 部门表设定有4个部门，员工表的部门ID就不能有5了，解决这个问题就需要约束，这个约束就是外键。
>
> 外键可以多重继承：A表 -> B表 -> C表。

#### 5.1 创建

右键创建外键的表 -> 设计表 -> 外键 ：起名一般`fk`开头`fk_`。

字段是要当外键的字段，参考模式是数据库名；

参考表是要以哪个表为基准，参考字段是要以该表的哪个字段为基准。



---





---



### 六、运算符

#### 6.1 逻辑运算符

```mysql
AND：并且	OR：或者	NOT：取反
```





#### 6.2 条件运算符

```mysql
>	<	>=	<=	<>(不等于)	!=(不等于非SQL-92标准)
```





#### 6.3 判断空/非空

```mysql
IS NULL / IS NOT NULL
```



---



### 七、函数

#### 7.1 字符串函数

```mysql
/*
| --------------------------------------------------------------------------------|
| **函数名**   | 						**描　　述**                                      
| LENGTH      | 计算字符串长度函数，返回字符串的字节长度                                 
| CONCAT      | 合并字符串函数，返回结果为连接参数产生的字符串，参数可以使一个或多个         
| INSERT      | 替换字符串函数                                               		  |
| LOWER       | 将字符串中的字母转换为小写                                   		  |
| UPPER       | 将字符串中的字母转换为大写                                   			 
| LEFT        | 从左侧字截取符串，返回字符串左边的若干个字符                 			 	|
| RIGHT       | 从右侧字截取符串，返回字符串右边的若干个字符                 				|
| TRIM        | 删除字符串左右两侧的空格                                    			 
| REPLACE     | 字符串替换函数，返回替换后的新字符串                        			   |
| SUBSTRING   | 截取字符串，返回从指定位置开始的指定长度的字符换           				   |
| CHAR_LENGTH | 获取字符的个数                                               			 
| ---------------------------------------------------------------------------------|
*/
```

##### 7.1.1 replace()

> 替换字符串

```mysql
select replace(被替换的字符串,替换该字符串中的哪个值,替换为什么);
select replace('abc','a','A');	-- 将字符串'abc'中的'a'替换为'A'
-- 替换表中一列的值
select replace(SubjectName,'Java','JAVA') from subject;
```



##### 7.1.2 length()

> 计算字符串长度函数，返回字符串的字节长度

```mysql
SELECT LENGTH('abc'); -- 3
SELECT LENGTH('中国'); -- 6(一个中文占3~4之间个字节)
SELECT CHAR_LENGTH('中国'); -- 2(char_length获取字符个数)
```



##### 7.1.3 concat()

> 合并字符串函数，返回结果为连接参数产生的字符串

```mysql
-- 参数可以是一个或多个
SELECT CONCAT('a','b','c');-- 字符串的拼接
-- 函数之间可以组合：先执行里面，再执行外面的
SELECT CHAR_LENGTH(CONCAT('a','b','c')); -- 3
-- 可以做拼接姓和名
```



##### 7.1.4 insert()

> 查找对应字符串替换

```mysql
-- INSERT(被替换的字符,从一开始,到哪里,替换为什么)
SELECT INSERT('abc',1,1,'A');	-- 查找字符串abc，从第一个字符查找到第一个字符，将abc替换为A
```



##### 7.1.5 lower()/upper()

> 转大小写

```mysql
SELECT LOWER('ABC') as 小写 , UPPER('abc') as 大写;
```



##### 7.1.6 left/right

> 截取字符串，从头开始

```mysql
-- 从左开始截取num个
SELECT LEFT (字符串, num)
SELECT LEFT ('Student.java',7),	-- student

-- 从右开始截取num个
SELECT RIGHT (字符串, num)
SELECT RIGHT('home.html',4), 	-- html
```



##### 7.1.7 substring

> 截取字符串，从指定位置开始(正数)

```mysql
-- SUBSTRING(被截取的字符串，从哪开始，截取几个)
SELECT SUBSTRING('aBcDeFgH',2,3); -- BcD
```



##### 7.1.8 substring_index

> 目标字符串,以哪个字符为分隔符切割为字符串，获取从哪到分隔符的第几个字符串

```mysql
SELECT SUBSTRING_INDEX('aBcDeFgH','D',1); -- aBc 从左开始到D的第一个字符串
SELECT SUBSTRING_INDEX('aBcDeFDgH','D',-1); -- eFgH 从右开始到D的第一个字符串
```





#### 7.2 日期函数

```mysql
/*
| --------------------------------------------------------------------------|
| 函数名                         |           描　　述                         |
| CURRENT_DATE,CURRENT_TIME     | 取得当前的系统日期和日期                      |
| YEAR                          | 获取年份，返回值范围是 1970〜2069             |
| MONTH                         | 获取指定日期中的月份                          |
| MONTHNAME                     | 获取指定日期中的月份英文名称                   |
| DAYOFWEEK                     | 获取指定日期对应的一周的索引位置值              |
| DAYOFYEAR                     | 获取指定曰期是一年中的第几天，返回值范围是1~366   |
| DAYOFMONTH                    | 获取指定日期是一个月中是第几天，返回值范围是1~31  |
| **ADDDATE、SUBDATE**          | 向日期添加指定的时间间隔，向日期减去指定的时间间隔 |
| ADDTIME、SUBTIME              | 原始时间上添加指定的时间、原始时间上减去指定的时间 |
| DATEDIFF                      | 获取两个日期之间间隔，返回参数 1 减去参数 2 的值  |
| DATE_FORMAT                   | 格式化指定的日期，根据参数返回指定格式的值        |
| WEEKDAY                       | 获取指定日期在一周内的对应的工作日索引            |
| **TIMESTAMPDIFF**             | 根据指定单位，比较日期的间隔                    |
| ---------------------------------------------------------------------------|
*/
```

##### 7.2.1 CURRENT_xxx()

> 获取当前日期/时间/日期和时间

```mysql
-- 		当前日期，			当前时间，		当前日期和时间(2种)
SELECT CURRENT_DATE(),	CURRENT_TIME(),	CURRENT_TIMESTAMP(),NOW();
```



##### 7.2.2 YEAR

> 获取年份

```mysql
SELECT YEAR('2022-12-12'); -- 获取字符串的年份，返回2022
SELECT year(NOW()), MONTH(NOW()); -- 2022 9
```



##### 7.2.3 DAYOFWEEK()

> 获取指定日期是一周的第几天（1-7）

```mysql
select DAYOFWEEK(NOW()) - 1; -- 从周日开始 所以减一
```



##### 7.2.4 ADDDATE()

> 对时间进行加减等算数运算

```mysql
SELECT ADDDATE(NOW(),INTERVAL 1 YEAR); -- 加上一年
SELECT ADDDATE(NOW(),INTERVAL -1 YEAR); -- 减去一年

SELECT ADDDATE(NOW(),INTERVAL 1 MONTH), -- 加上一月
	   ADDDATE(NOW(),INTERVAL 1 DAY), -- 加上一天
	   ADDDATE(NOW(),INTERVAL 1 HOUR), -- 加上一小时
	   ADDDATE(NOW(),INTERVAL 1 MINUTE); -- 加上一分钟
```



##### 7.2.5 DATEDIFF()

> 日期比较大小，返回天数

```mysql
SELECT DATEDIFF(时间A，时间B)		-- A比B大/小了多少天
SELECT DATEDIFF(NOW(),'2008-5-12');	-- 5251
```

###### TIMESTAMPDIFF()

> 自定义返回值，不返回天数

```mysql
SELECT TIMESTAMPDIFF(YEAR,'2008-5-12',NOW()); -- 年
SELECT TIMESTAMPDIFF(MONTH,'2008-5-12',NOW()); -- 月
SELECT TIMESTAMPDIFF(DAY,'2008-5-12',NOW()); -- 日
SELECT TIMESTAMPDIFF(HOUR,'2008-5-12',NOW()); -- 小时
```





#### 7.3 聚合函数

> SQL语言本身的函数，所以可以跨数据库使用。计算的值只有一个。

##### 7.3.1 MAX() / MIN()

> 查询指定列的最大值/最小值

```mysql
SELECT MAX(字段名) FROM 表名;
SELECT MAX(GradeId) FROM student;	-- 最大是3
SELECT MIN(GradeId) FROM student;	-- 最小是1
```



##### 7.3.2 COUNT

> 统计行数(数据条数)

```mysql
-- 统计所有数据的行数
SELECT COUNT(*) FROM 表名;
SELECT COUNT(1) FROM 表名;

SELECT COUNT(字段名) FROM 表名;
SELECT COUNT(studentNo) FROM student; -- 统计学号的行数
-- 不能再添加其他列了
SELECT COUNT(1),studentNo FROM student;
```

###### 模拟用户登录

> 学号和密码

```mysql
SELECT IF(COUNT(1) > 0 , '登录成功' , '登陆失败') 
FROM student
WHERE studentNo = '001'
AND LoginPwd = 123456;
```



##### 7.3.3 SUM() / AVG()

> 获取该列所有值的和/平均数

```mysql
SELECT SUM(price) FROM fruit;
SELECT AVG(price) FROM fruit;
```

###### 排序后取第一条

```mysql
SELECT * FROM result ORDER BY studentResult desc limit 1;
SELECT COUNT(1),MAX(GradeId) FROM student;
SELECT SUM(ClassHour) as 总课时 ，AVG(ClassHour) as 平均课时 FROM SUBJECT;
```



---



### 八 、流程控制

#### 8.1 CASE END

> 选择结构

```mysql
SELECT CASE (DAYOFWEEK(NOW()) - 1)	-- 返回一个int 
	WHEN 1 THEN '周一'	-- case相当于switch，括号里的值去匹配when，匹配成功执行then
	WHEN 2 THEN '周二'
	WHEN 3 THEN '周三'
	WHEN 4 THEN '周四'
	WHEN 5 THEN '周五'
	WHEN 6 THEN '周六'
	WHEN 7 THEN '周日'
END;
```





#### 8.2 IF()

> SQL三元表达式

```mysql
IF(表达式1，表达式2，表达式3)跟三元表达式一样，判断表达式1，true执行表达式2，false执行表达式3
-- 判断年龄是否成年或未成年
SET @age = 20;	-- 定义一个用户变量
SELECT IF (@age > 18,'已成年','未成年');
```
