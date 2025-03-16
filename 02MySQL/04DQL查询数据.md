### 1、DQL

- (Data Query Language: 数据查寻语句)
  - 所有查询都是用的他 select
  - 简单复杂都可以
  
- ```sql
  SELECT [ALL | DISTINCT]
  {* | table.* | [table.field1[as alias1][,table.field2[as alias2]][,...]]}
  FROM table_name [as table_alias]
    [left | right | inner join table_name2]  -- 联合查询
    [WHERE ...]  -- 指定结果需满足的条件
    [GROUP BY ...]  -- 指定结果按照哪几个字段来分组
    [HAVING]  -- 过滤分组的记录必须满足的次要条件
    [ORDER BY ...]  -- 指定查询记录按一个或多个条件排序
    [LIMIT {[offset,]row_count | row_countOFFSET offset}];
     -- 指定查询的记录从哪条至哪条
  
  ```

  

### 2、查询所有字段

```sql
-- 查询全部
select * from `subject`;
-- 查询指定字段
select `StudentNo`,`StudentName` from `student`;
-- 起别名
select `StudentNo` as '学号',`StudentName` as '学生姓名' from `student` as s;
-- 拼接
select CONCAT('姓名:',StudentName) as 学生名 from `student` as 学生表;
```

去重复distinct  去除select查询出来的结果中重复的数据，重复的数据只显示一条

``` mysql
-- 查询一下哪些同学参加了考试 成绩
select * from result --查询全部的考试成绩
select `studentNo` from result -- 查询有哪些同学参加了考试
selct distinct `studentNo` from result --发现重复的数据，去重
```

select 表达式 from 表

### 3、where 条件子句

- 逻辑运算符

  | 运算符  | 语法            | 描述            |
  | ------- | --------------- | --------------- |
  | and &&  | a and b  a&&b   | 逻辑与          |
  | or \|\| | a or b a \|\| b | 逻辑或          |
  | Not !   | not a !a        | 逻辑非 非黑即白 |

  ```sql
  -- 成绩区间
  -- and
  select `studentno`,`studentresult` from `result`
  where studentresult >= 70 and studentresult <=100;
  -- &&
  select `studentno`,`studentresult` from `result`
  where studentresult >= 70 && studentresult <=100;
  -- between  and
  select `studentno`,`studentresult` from `result`
  where studentresult between 70 and 100;
  
  -- 查询学号不为1000的
  select `studentno`,`studentresult` from `result`
  where `studentno` != 1000;
  select `studentno`,`studentresult` from `result`
  where `studentno` = 1000;-- 只查询1000号的
  select `studentno`,`studentresult` from `result`
  where not `studentno` != 1000;-- 排除1000
  ```

  

- 模糊查询：比较运算符

  | 运算符           | 语法                      | 描述                                 |
  | ---------------- | ------------------------- | ------------------------------------ |
  | is null          | studentNo is null         | 如果操作符为Null,结果为真            |
  | is not null      | studentNo is not null     | 如果操作符不为Null,结果为真          |
  | between and      | studentNo between a and b | 若studentNo在 a和b之间，则结果为真   |
  | **Like**（重要） | **a like b**              | **Sql 匹配，如果a匹配b，则结果为真** |
  | IN（重要）       | A IN (a1,a2,a3,a4....)    | 如果A在列表中，结果为真              |

```sql
## Like 操作案例  模糊查询，查询姓刘的同学
like 结果 %(代表0到任意个字符 )  _(一个字符)

select `studentNo`,`studentName` from `student`
where studentName Like '刘%'

##查询姓刘的同学，名字后面只有一个字
select `studentNo`,`studentName` from `student`
where studentName Like '刘_'
##查询姓刘的同学，名字后面只有二个字
select `studentNo`,`studentName` from `student`
where studentName Like '刘__'
##查询名字中带有嘉的，
select `studentNo`,`studentName` from `student`
where studentName Like '%嘉%'


## IN 
##  模糊查询，查询1001 1002 1003号学员

select `studentNo`,`studentName` from `student`
where studentNo in(1001,1002,1003);

## null  not null
--查询地址为空的学生 null
select `studentNo`,`studentName` from `student`
where address ='' or address is null;


## not null  查询出生日期不为空的学生，查询有出生日期的同学
select `studentNo`,`studentName` from `student`
where `BornDate` is not null;


```

### 4、联表查询

![MySQL联表查询_mysql查询今年九月所有女生的成绩 join-CSDN博客](https://gitee.com/ppedmo/pic-go/raw/master/img/202411250830545.png)

- 联表查询的连接，不管是哪种连接，本质上都是在总的笛卡尔积下进行筛选过滤而已。知识筛选的方式不同

- inner 需要两个表都匹配的数据，left左边的表数据都显示，right右边的表都展示，full两边的表都展示
- left join 左连接：展示左表所有数据，右表符合on条件的数据，右表不符合的则为空显示。

- where是在整个笛卡尔积里面筛选，on是构造笛卡尔积时指定的条件----连接条件

- 字段加了着重号就必须要用on，使用where会出现语法错误

- ```sql
  -- join on    连接查询
  -- where     等值查询
  -- on 连接判断  where 全局判断
  
  -- 多表连接查询
  -- students表包含学生的ID和姓名。
  -- classes表包含课程的ID和课程名称。
  -- enrollments表是一个关联表，包含学生ID和课程ID，表示哪些学生选了哪些课程。
  SELECT students.name, classes.class_name
  FROM students
  JOIN enrollments ON students.id = enrollments.student_id
  JOIN classes ON enrollments.class_id = classes.id
  WHERE classes.class_name = 'Math';
  ```

- ```sql
  -- 结果集中包含左表（table_a）的所有记录：这意味着查询结果将包含table_a中的所有行，不管它们在table_b中是否有匹配的记录。
  -- 匹配的记录显示两个表的数据：对于table_a中的每一行，如果在table_b中找到满足连接条件a.id = b.a_id的对应行，那么结果集中相应的行将包含两个表的数据。
  -- 不满足条件的显示NULL：如果在table_b中没有找到满足连接条件的对应行，那么结果集中对应的table_b部分的字段将显示为NULL。
  
  SELECT a.*, b.*
  FROM table_a a
  LEFT JOIN table_b b ON a.id = b.a_id;
  ```

- ```sql
  -- ======================自连接============================
  -- 自连接
  CREATE TABLE `category` (
    `categoryid` INT(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主题id',
    `pid` INT(10) NOT NULL COMMENT '父id',
    `categoryName` VARCHAR(50) NOT NULL COMMENT '主题名字',
    PRIMARY KEY (`categoryid`)
  ) ENGINE=INNODB AUTO_INCREMENT=9 DEFAULT CHARSET=utf8
  INSERT INTO `category`(`categoryid`,`pid`,`categoryName`)
  VALUES('2','1','信息技术'),
  ('3','1','软件开发'),
  ('4','3','数据库'),
  ('5','1','美术设计'),
  ('6','3','web开发'),
  ('7','5','ps技术'),
  ('8','2','办公信息');
  -- 自己的表跟自己的表连接，核心：一张表拆为两张一样的表
  -- 查询父子信息
  select * from `category`
  SELECT a.`categoryName` AS '父栏目',b.`categoryName` AS '子栏目'
  FROM `category` AS a,`category` AS b
  WHERE a.`categoryid` = b.`pid`-- a的id=b的pid
  ```

### 5、分页与排序

- 分页limit 和 排序order by

> 排序
>
> order by studentresult desc 
>
> desc降序排列        asc 升序排列

> 分页 ：缓解数据库压力，给人的体验更好，现在很多瀑布流
>
> 语法：limit 起始，步长
>
> limit 0,5         0 1 2 3 4
>
> limit 1,5         1 2 3 4 5



### 6、子查询和嵌套查询

- where （值是固定的，如果这个值不固定，是计算出来的，那就是子查询，嵌套查询）

```sql
-- 方式一 ：使用关联查询
SELECT `StudentNo`,r.`SubjectNo`,`SutdentResult`
from result r
INNER JOIN `subject` s
ON r.`SubjectNo`= s.SubjectNo
where SubjectName='数据库结构-1'
ORDER BY SutdentResult DESC

-- 方式二：使用嵌套查询，查找顺序是由里及外，
SELECT `StudentNo`,r.`SubjectNo`,`SutdentResult`
from result
WHERE `SubjectNo`=(
	SELECT `SubjectNo` from `subject` where `SubjectName`='数据库结构-1'
)
ORDER BY SutdentResult DESC

-- 方式三  查询高等数学分数不低于80分的 学号和姓名
-- 查询高等数学-2分数不低于80分的学号和姓名
SELECT `StudentNo`,`StudentName` FROM student WHERE StudentNo in(
	SELECT StudentNo FROM result WHERE SutdentResult>80 AND SubjectNo=(
		SELECT `SubjectNo` from `subject` WHERE SubjectName='高等数学-2'
	)
)


```
