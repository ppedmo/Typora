### 1、外键

使用了其他表的主键属性建立联系

方式一，在创建表的时候，增加约束

```mysql
CREATE TABLE `grade` (
	`gradeid` INT(10) NOT NULL auto_increment COMMENT '年级id',
	`gradename` VARCHAR(30) not NULL COMMENT '年级名次',
	PRIMARY KEY(`gradeid`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;


CREATE TABLE if not EXISTS `student2` (
	`id` INT(4) NOT NULL auto_increment COMMENT '学号',
	`name` VARCHAR(30) not NULL DEFAULT '匿名' COMMENT '姓名',
	`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
	`sex` VARCHAR(20) NOT NULL DEFAULT '女' COMMENT '性别',
	`birthday` DATE DEFAULT NULL COMMENT '出生日期',
	`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
	`email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
	`gradeid` INT(10) NOT NULL COMMENT '学生年级',
	PRIMARY KEY(`id`),

	KEY `fk_gradeid` (`gradeid`),
	CONSTRAINT `fk_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `grade`(`gradeid`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;

```

方式二，创建表没约束，之后添加

```mysql
ALTER TABLE `student2` 
ADD CONSTRAINT `fk_gradeid` FOREIGN KEY(`gradeid`) REFERENCES `grade`(`gradeid`);
```



以上操作都是物理外键，不建议

==最佳实践==

数据库就是单纯的 表，只有行（数据）和列（字段）

想使用外键的话，程序去实现

### 2、DML语言

- 增删改
- insert 
- update
- delete

### 3、 添加  Insert

语法结构 insert into 表名 (['字段名1','字段名2','字段名3','字段名4'.....]) values ('值1', '值2','值3','值4'.....),...

字段可以省略，但后面的值必须一一对应

```mysql
INSERT INTO `grade`(`gradename`) VALUES ('大四')
insert into `grade`(`gradename`) values('大三'),('大二'),('大一')
INSERT INTO `student`(`name`,`pwd`,`sex`,`birthday`,`address`,`email`,`gradeid`) VALUES ('张三','aaa123','男','2020-01-01','北京','email@email.com','1')

INSERT INTO `student2`(`name`,`pwd`,`sex`,`gradeid`) VALUES ('张四','aaa123','女','1')
##插入多个字段多个值，可以省略字段，但是需要表字段所有的字段都赋值
INSERT INTO `student2` VALUES ('5','张四','aaa123','女','2020-01-01','北京','hel@admin.com','1'),
('6','张四','aaa123','女','2020-01-01','北京','hel@admin.com','1'),
('7','张四','aaa123','女','2020-01-01','北京','hel@admin.com','1'),
('8','张四','aaa123','女','2020-01-01','北京','hel@admin.com','1'),
('9','张四','aaa123','女','2020-01-01','北京','hel@admin.com','1'),
('10','张四','aaa123','女','2020-01-01','北京','hel@admin.com','1'),
('11','张四','aaa123','女','2020-01-01','北京','hel@admin.com','1'),
('12','张四','aaa123','女','2020-01-01','北京','hel@admin.com','1')
```

### 4、 修改 Update

语法结构： update 表名  set [ 具体字段=新值, 具体字段=新值, 具体字段=新值 ] where 条件

update 表名 set 字段=新值 where 条件

```mysql
UPDATE `student2` SET `name`='狂神' WHERE id =1  
UPDATE `student2` SET `name`='狂神' -- 不指定条件全部都改了
UPDATE `student2` SET `name`='狂神',`sex`='女',`email`='wetos@aliyun.com' WHERE id =1
```

操作符会返回布尔值

| 操作符             | 意义            | 范围                  | 结果  |
| ------------------ | --------------- | --------------------- | ----- |
| =                  | 等于            | 5=6                   | false |
| <>  或者  !=       | 不等于          | 5<>6                  | true  |
| >                  |                 |                       |       |
| <                  |                 |                       |       |
| >=                 |                 |                       |       |
| <=                 |                 |                       |       |
| BETWEEN ... AND... | [] 在某个范围内 | BETWEEN 2 AND 5 [2,5] |       |
| AND                | 我和你          | 5>1 and 1>2           | false |
| OR                 | 我或你 \|\|     | 通过多个条件定位数据  |       |

```mysql
update `student` set `name`='长江7号' where `name`='kuangshen44' and sex='女'
```

注意：

```sql
-- column_name 是数据库的列，尽量带上``
-- 条件，筛选的条件，如果没有指定，则会修改所有的列
-- value 是一个具体的值，也可以是一个变量
-- 多个设置属性使用英文逗号隔开
```

### 5、 删除 Delete

语法 `delete from 表名 [ where 条件]`

```mysql
delete from `student` ##删除所有数据

delete from `student ` where id =1; 
```

truncate命令

作用：完全清空一个数据库表，表的结构和索引约束不会变

```sql
truncate `student`
```

两种删除方法的区别：

- 相同的 都能删除数据，都不会删除表结构
- 不同
  - TRUNCATE 重新设置，自增列，计数器会归零
  - TRUNCATE 不会影响事务

