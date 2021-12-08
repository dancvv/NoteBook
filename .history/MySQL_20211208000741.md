# 数据库

1. 数据库基本概念
2. MySql软件
3. SQL  
##数据库
DataBase  
* 用于存储和管理数据的仓库

数据库的特点：  
1. 持久化存储数据
2. 方便存储和管理数据
3. 统一的方式操作数据库-SQL

#### 卸载

* 去mysql的安装目录找到my.ini
* 卸载mysql
* 找到programdata下的mysql，直接删除掉

### 配置
服务中心设置mysql的启动方式  

1. 手动  
2. cmd-->services.msc
3. 以管理员权限打开cmd，启动mysql服务
    * net start mysql
    * net stop mysql

- mysql登录

1. mysql -uroot -proot 或 -p  
2. mysql -hip -uroot -p链接目标的密码  

* mysql退出  

1. exit
2. quit

- mysql目录结构

1. 安装目录
2. mysql数据目录
   * 几个概念
     * 数据库：文件夹
     * 表：文件
     * 数据：

* MySql用户名和密码：

  PipeName：MySQL56

  Password：root

  **MySQL设置**

  登录直接写`mysql -u root -p`

<img src="C:\Users\Wang\AppData\Roaming\Typora\typora-user-images\image-20210601202146126.png" alt="image-20210601202146126" style="zoom:80%;" />

# SQL

1. 结构化查询语言

   定义了操作所有关系型数据库的规则。每一种数据库操作的方式存在不一样的地方

2. SQL通用语法

   1. SQL 语句可以单行或多行书写，以分号结尾
   2. 可使用空格和缩进来增强语句的可读性
   3. MySQL数据库的SQL语句不区分大小写，**但建议使用大写**
   4. 3种注释：
      	* 单行注释：`-- ` 注释内容 或`#  `注释内容，*有空格*
      	* 多行注释：/* 注释 */

3. SQL分类：

   1. DDL：操作数据库、表
   2. DML：增删改表中的数据
   3. DQL：查询表中的数据
   4. DCL：授权

   ![image-20210602125119381](C:\Users\Wang\AppData\Roaming\Typora\typora-user-images\image-20210602125119381.png)

## DDL：操作数据库、表

1. 操作数据库：CRUD

   **查询：Retrieve**

   * 创建数据库，判断存在，在创建；
     * `create database if not exists db2;`
   * 创建数据库，并指定字符集
     * `create database 数据库名称 character set 字符集;`

   	 show databases;
   	 show create database mysql 数据库名称
   	 creat database 数据库名
   	 	create database if not exists db2;判断是否存在db2
   	 	create database set gbk 指定字符集
   	 	create database if not exists db4 character set gbk;综合型判断语句

   **修改UPDATE**

   修改字符集的数据集

   ​	`alter database 数据库名称 character set 字符集`

   **删除**

   删除数据库

   ​	`drop database 数据库名`

   判断数据库是否存在，再删除

   ​	`drop database if exists db4;`

   **使用数据库**

   查询正在使用的数据名称

   ​	`	select database()`

   使用数据库

   ​	`use 数据库名称;`

1. 操作表

   * 创建表

     1. 语法：

        ````mysql
        create tables 表名(
        	列名1 数据类型1，
        	列名2 数据类型2，
        ...
        	列名n 数据类型n
        );
        ````

        数据类型：

         1. int:整数类型

            * age int,

        	2. double:小数类型

            * score double(5,2) *一共有无为，保留2位小数，999.99*

        	3. date：日期，只包含年月日，yyyy-MM-dd

        	4. datetime:日期，包含年月日时分秒 yyyy-MM-dd HH:mm:ss

        	5. timestap:时间戳，包含年月日时分秒 yyyy-MM-dd HH:mm:ss

            *如果将来不给这个字段赋值，或赋值为null，则默认使用当前的系统时间，来自动赋值*

        	6. varchar: 字符串

            * name varchar(20): 姓名最大20个字符
            * zhangsan 8个字符 张三 2个字符

   * 创建表

     ````mysql
     create table student(
     	id int,
     	name varchar(32),
     	age int,
     	score double(2,1),
     	birthday date,
     	insert_time timestamp
     );
     create table account(
        id int,
        name varchar(255) character set utf8);
     ````
     
     **复制表 creat table 表名 like 被复制表**
     
     **`create table stu like student`**
   
   ![image-20210602192820893](C:\Users\Wang\AppData\Roaming\Typora\typora-user-images\image-20210602192820893.png)
   
   * 查询
   
     * 查询某个数据库中所有的表名称
       * `show tables;`
     * 查询表结构
       * `desc 表名;`
   
   * 删除
   
     常规写法
   
     `drop table 表名;`
   
     `drop table if exists 表名;`
   
   * 修改
   
     1. 修改表名
   
        `alter table 表名 rename to 新表名`
   
     2. 修改表的字符集
   
        `show create table 表名`展现表的字符集
   
        `alter table 表名 character set 字符集名称;`
   
     3. 增加一列
   
        `alter table 表名 add 列名 数据类型;`
   
     4. 修改列名称 类型
   
        ` alter table 表名 change 列名 新列名 新数据类型;`
   
        `alter table 表名 modify 列名 新数据类型 `
   
     5. 删除列
   
        `alter table 表名 drop 列名`

* 客户端图形化工具：SQLyog

## DML:

#### 增删改查表中的数据

1. 添加数据

   **语法：**

* `insert into 表名(列名1,列名2,...) values(value1,value2,...);`
* 注意：
  * 列名和值要一一对应。
  * 如果表名后，不定义列名，则默认给所有列添加值
  * 除了数字类型，其他类型需要使用引号""

2. 删除数据

   `delete from 表名 where 条件`

   *如果不加条件，则删除表中所有记录，不建议使用这种方式删除数据，效率低*

   *delete from 表名* --不推荐使用。有多少条记录就会执行多少次删除操作

   `truncate table stu;`--删除一个表，然后在创建一个一模一样的表。**推荐使用**

3. 修改数据：

   * 语法:

     * `update 表名 set 列名1 = value1， 列名2=value2 where [条件] `

       注意：如果不加条件，则会修改表中所有的数据。
   
   addressLine1,addressLine2,city,state,postalCode,country,salesRepEmployeeNumber,creditLimit

## DQL：

`select * from 表名`

1. 语法

   ````mysql
   select
   	字段列表
   form
   	表明列表
   where
   	条件列表
   group by
   	分组列表
   having
   	分组之后的条件
   order by
   	排序
   limit
   	分页限定
   ````

2. 基础查询

   1. 多个字段的查询

      `select 列名1,列名2,... from 表名;`

      如果查询所有字段，可以使用*来替代字段列表

   2. 去除重复

      `distince`去重

      `select distinct 列名 from 表名`

   3. 计算列

      `select 列名1,列名2, 列名1+列名2 from 表名;`

      如果有null参与的运算，计算结果都为null;

      `select 列名1,列名2, 列名1+ifnull(列名2,0) from 表名;`

      起别名`as`

      `select 列名1,列名2, 列名1+ifnull(列名2,0) as 别名 from 表名;`

      *别名的简化写法*

      `select 列名1,列名2, 列名1+ifnull(列名2,0) 别名 from 表名;`

      `ifnull(表达式1，表达式2)`

      ​	表达式1：那个字段需要判断是否为null

      ​	表达式2：如果该字段为null后的替换值

3. 条件查询

   1. where字句后跟条件

   2. 运算符

      判断等于一个等号`=`就可，不等号`!=,<>`

       `like`模糊查询

      占位符：_单个字符 %任意字符

      > 查询姓马的有哪些  
      >
      > ​	`like '马%'`

      > 查询姓名第二个字是化的人  
      >
      > `like '_化'`

      > 查询姓名是3个字的人  
      >
      > ​	`like '___'`

## DQL:查询语句

1. 排序查询

   > 语法：`order by 子句`  
   > ​	`order by 排序字段1 排序方式1,排序字段2，排序方式2...`  
   >
   > `select * from 表名 order by --排序方式`
   >
   > `select * from student order by math desc`--降序排列
   >
   > 排序方式:     
   >
   > desc --降序
   >
   > ASC --升序(DEFAULT Method)
   >
   > 注意：
   >
   > ​	如果有多个排序条件，则当前边的条件值一样时，才会判断第二条件
   
2. 聚合查询：将一列数据作为一个整体，进行纵向的计算

   1. `count`：计算个数

   > `select count(name) from 表名`
   >
   > 解决非空的问题
   >
   > `select count(ifnull(name,0)) from 表名`
   >
   > 一般选非空的列：主键
   >
   > count（*）

   1. `max`
   2. `min`
   3. `sum`
   4. `avg`

   **注意：聚合函数会排除null的值**

   解决方案：

    	1. 选择不包含非空的列进行计算
    	2. ifnull函数

3. 分组查询：

   > 语法 :`group by 分组字段`
   >
   > 按照性别分组，分别查询男、女同学的平均分
   >
   > `select sex,avg(math) from student group by sex`
   >
   > 按照性别分组，分别查询男、女同学的平均分 要求：分数低于70分的人，不参与分组
   >
   > `select sex,avg(math) from student where math>70 group by sex`
   >
   > 按照性别分组，分别查询男、女同学的平均分 要求：分数低于70分的人，不参与分组，分组之后，人数要大于2
   >
   > `select sex,avg(math) from student where math>70 group by sex having count(id)>2`
   >
   > 注意：
   >
   > where 和 having的区别？
   >
   >  	1. where在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如果不满足结果，则不会被查询出来
   >  	2. where后不可以跟聚合函数，having可以进行聚合函数的判断

4. 分页查询

   > 语法：`limit`开始的索引，每页查询的条数；
   >
   > `select * from 表名 limit 范围（0,3） `--从0开始，每页显示3个

   ````mysql
   select * from 表名 limit 0,3 --第一页
   select * from 表名 limit 3,3 --第二页
   --公式：开始的索引=（当前的页码-1）*每页显示的条数
   ````

   > limit分页操作是一个“方言”

## 约束

* 概念：对表中的数据进行限定，保证数据的正确性和有效性，完整性。

* 分类
  1. 主键约束
  2. 非空约束
  3. 唯一约束
  4. 外键约束

**非空约束**：not null  

> 1. 创建表时，添加约束
>
> ````mysql
> CREATE table stu(
> 		id int,
> 		name varchar(20) NOT NULL -- NAME为非空
> 		);
> ````
>
> 删除name的非空约束
>
> `alter table stu Modify name varchar(20);`
>
> 创建表完后，添加非空约束
>
> `alter table stu Modify name varchar(20) not null;`

**唯一约束**:unique，值不能重复

> ````mysql
> CREATE TABLE stu(
> 	id INT,
> 	phone varchar(20) UNIQUE -- 添加唯一约束
> 	);
> 	
> alter TABLE stu CHANGE phonr phone VARCHAR(20);
> 
> INSERT into stu(id,phone) VALUES(1,"1454");
> INSERT into stu VALUES(1,"1454");
> INSERT into stu VALUES(2,"145");
> INSERT into stu VALUES(3,null);
> 
> -- 删除唯一约束
> -- ALTER TABLE stu MODIFY phone VARCHAR(20);不起作用
> ALTER TABLE stu DROP INDEX phone;
> 
> -- 创建表后，添加唯一约束
> Alter TABLE stu MODIFY phone VARCHAR(20) UNIQUE;
> ````

**主键约束**：primary key

> 1. 注意：
>    1. 含义：非空且唯一
>    2. 一张表只能有一个字段为主键
>    3. 主键就是表中记录的唯一标识
> 2. 在创建表时，添加主键约束
>
> ```mysql
> CREATE TABLE stu(
> 	id INT primary key, -- 给id添加主键约束
> 	name varchar(20)
> 	);
> 	
> -- 删除主键
> -- ALTER TABLE stu MODIFY id INT; -- 不可行的方式
> ALTER TABLE stu DROP PRIMARY KEY;		
> 	
> -- 创建添加主键
> ALTER TABLE stu MODIFY id INT PRIMARY KEY;
> ```
>
> 3. 自动增长：(与主键配合一起使用)
>    * 概念：如果某一列是数值类型的，使用auto_increment 可以来完成值得自动增长
>    * 在创建表时，添加主键约束，并完成主键自动增长
>
> ```mysql
> CREATE TABLE stu(
> 	id INT primary key auto_increment, -- 给id添加主键约束
> 	name varchar(20)
> 	);
> 	
> -- 删除自动增长
> 	ALTER TABLE stu MODIFY id int;
> -- 添加自动增长
> 	ALTER TABLE stu MODIFY id int AUTO_INCREMENT;
> ```

**外键约束**：foreign key

1. 在创建表时，可以添加外键

   * 语法：

     ```mysql
     create table 表名(
     	...
     	外键列
     	constraint 外键名称 foreign key （外键列名称） references 主表名称（主表列名称）
     	);
     -- 删除外键
     alter table 表名 drop foreign key 外键名称；
     
     -- 创建表之后，添加外键
     alter table 表名 add contraint 外键名称 foreign key （外键列名称） references 主表名称（主表列名称）
     -- 如果表中数据有问题，会出现添加失败
     alter TABLE orderdata ADD FOREIGN KEY(down_stop_id) REFERENCES location(station_id);
     ```
   
     外键名称随意起
   
   * 级联操作

### 字段添加

表建立完成后，添加一个完整的字段如下：

```mysql
ALTER TABLE <表名> ADD <新字段名><数据类型>[约束条件];
```

对语法格式的说明如下：                    

- <表名> 为数据表的名字；
- <新字段名> 为所要添加的字段的名字；
- <数据类型> 为所要添加的字段能存储数据的数据类型；
- [约束条件] 是可选的，用来对添加的字段进行约束。

这种语法格式默认在表的最后位置（最后一列的后面）添加新字段。

>  注意：本节我们只添加新的字段，不关注它的约束条件。

#### 在开头添加字段

MySQL 默认在表的最后位置添加新字段，如果希望在开头位置（第一列的前面）添加新字段，那么可以使用 FIRST 关键字，语法格式如下：

```mysql
ALTER TABLE <表名> ADD <新字段名> <数据类型> [约束条件] FIRST;
```

> FIRST 关键字一般放在语句的末尾。

#### 在中间位置添加字段

MySQL 除了允许在表的开头位置和末尾位置添加字段外，还允许在中间位置（指定的字段之后）添加字段，此时需要使用 AFTER 关键字，语法格式如下：

```mysql
ALTER TABLE <表名> ADD <新字段名> <数据类型> [约束条件] AFTER <已经存在的字段名>;
```

AFTER 的作用是将新字段添加到某个已有字段后面。

> 注意，只能在某个已有字段的后面添加新字段，不能在它的前面添加新字段。



## 数据库的设计

1. 多表之间的关系

   **分类**

   1. 一对一：
      * 如：人和身份证，一对一的关系
      * 分析：一个人只有一个身份证，一个身份证也只能对应一个人
   2. 一对多(多对一)：
      * 如：部门和员工
      * 分析：一个部门有多个员工，一个员工只能对应一个部门
   3. 多对多:
      * 如：学生和课程
      * 分析：一个学生可以选择很多门课程，一个课程也可被很多学生选择

   **实现关系**

   1. 一对多(多对一):

      * 如：部门和员工

      * 在多的一方建立外键，指向一的一方的主键

   ![image-20210605153822453](C:\Users\Wang\AppData\Roaming\Typora\typora-user-images\image-20210605153822453.png)

    	2. 多对多的关系：
    	 * 如：学生和课程
    	 * 多对多关系实现需要借助第三章中间表。
    	 * 中间表至少包含两个字段，这两个字段作为第三张表的外键，分别指向两张表的主键

![image-20210605154503877](C:\Users\Wang\AppData\Roaming\Typora\typora-user-images\image-20210605154503877.png)

​		3. 一对一：

​			![image-20210605161556655](C:\Users\Wang\AppData\Roaming\Typora\typora-user-images\image-20210605161556655.png)

​	

2. 数据库设计的范式
   * 概念：设计数据库时，需要遵循的一些规范

## 数据库的备份和还原

1. 命令行

   * 语法

   ` mysqldump -u用户名 -p密码 数据库名称 >保存的路径`

   `mysqldump -uroot -p databases > path`

   this method suggests save the file in another route path exclude the c ,because this route need authority

   

   * 还原
     * 登录数据库
     * 创建数据库
     * 使用数据库
     * 执行文件`source 文件路径`

2. 图形化工具

## MySQL导入CSV文件

以下语句将数据从`F:/worksp/mysql/discounts.csv`文件导入到`discounts`表。

建表语句

```mysql
CREATE TABLE orderdata(
		id INT,
		passenger_id VARCHAR(255),
		date date,
		create_time TIME,
		check_ticket_time TIME,
		up_stop_id INT,
		down_stop_id INT,
		ride_count INT,
		small_vehicle_id VARCHAR(255),
		car_id varchar(255)
);
```

```sql
load data infile 'E:/new_order_data.csv' into table orderdata character set utf8 fields terminated by ',' optionally enclosed by '"' escaped by '"' lines terminated by '\r\n' IGNORE 1 ROWS;
```



```sql
LOAD DATA INFILE 'E:/new_order_data.csv' 
INTO TABLE orderdata
character set utf8
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```

文件的字段由`FIELD TERMINATED BY ','`指示的逗号终止，并由`ENCLOSED BY '"'`指定的双引号括起来。

因为文件第一行包含列标题，列标题不需要导入到表中，因此通过指定`IGNORE 1 ROWS`选项来忽略第一行。

现在，我们可以查看`discounts`表中的数据，查看是否成功导入了数据。

## JDBC

**快速入门**

* 步骤
  * 导入驱动jar包
    * 复制jar包到目录的libs目录下
    * 右键-->add as library
  * 注册驱动
  * 获取数据库连接对象connection
  * 定义sql
  * 获取执行sql语句的对象statement
  * 执行sql，接收返回结果
  * 处理结果
  * 释放资源

* 详解各个对象

  1. drivermanager：驱动管理对象

     功能

      	1. 注册驱动：告诉程序
      	 * 写代码使用：class.forname()
      	 * 通过源码发现，在jdbc类中存在静态代码块注册驱动
      	 * mysql5之后的驱动jar包可以省略注册驱动的步骤
      	2. 获取数据库连接：
      	 * 方法：DriverManager.getConnection
      	 * 参数：
      	   * url：指定连接的路径
      	     * 语法：`jdbc:mysql://ip地址(域名)：端口号/数据库名称`
      	     * 例子：`jdbc:mysql://localhost:3306/db1`
      	     * 细节：如果连接的是本机mysql服务器，并且mysql服务默认端口是3306，则mysql可以简写为：`jdbc:mysql://db1`
      	   * user用户名
      	   * password密码

  2. connection：数据库连接对象

     1. 功能，获取执行sql的对象
        * createStatement()
        * Preparestatemen preparestatemen 
     2. 管理事务：
        * 开启事务：setAutoCommit 调用该方法设置参数为false，即开启事务
        * 提交事务：commit
        * 回滚事务：rollback

  3. statement：执行sql的对象

     1. 执行sql
        1. boolean execute：可以执行任意的sql
        2. int executeUpadate：执行dml（inserte，update、delete）、ddl（create、alter、drop）语句
           * 返回值：影响的行数
        3. Resultset ExecuteQuery：执行dql（select）语句
     2. 联系：
        1. account表 添加一条记录
        2. 修改记录
        3. 删除一条记录

  4. resultset：结果集对象，封装查询结果

     * Boolean next()游标乡下移动一行，判断当前当前行是否是当前最后一行末尾（是否有数据）如果是，则返回false，否则返回true；
     * getXxx()：获取数据；
       * Xxx代表数据类型 如：int getInt() String getString()
       * 参数：
         1. int 代表列的编号，从1开始 如：getString（2）
         2. String：列名称，如：getDouble("balance")
     * 注意：
       * 使用步骤：
         1. 游标向下移动一行
         2. 判断是否有数据
         3. 获取数据
     * 练习：
       * 查询emp表的数据将其封装为对象，然后装载集合，返回。然后打印
         1. 定义Emp类
         2. 定义方法 `List<Emp> findAll(){}`
         3. 实现方法`select * from emp;`

  5. perparedstatement：执行sql的对象

## 抽取JDBC工具类：JDBCUtils

* 目的简化书写

* 分析：

  * 注册驱动也抽取

  * 抽取一个方法获取连接对象

    * 需求，不想传递参数(麻烦)，还得保证工具类的通用性。

    * 解决：配置文件  

      ```java
      jdbc.properites
      user
      password
      ```

登录方法

```
login(username password)
```

## 数据库连接池



## SpringJDBC

* Spring框架对JDBC的简单封装

> 调用JDBCtemplate的方法完成

<<<<<<< HEAD


### MySQL在Unbuntu下的问题

ubuntu下安装mysql会自动设置一个默认密码，首先查看默认密码，然后利用默认密码登录mysql，进入mysql后利用命令行修改

查看密码

 = localhost
user     = debian-sys-maint
password = rR8rIDoy5GO087Zt

```
sudo vim /etc/msyql/debian.cnf
```

目前采用mysql5.8以上的版本，与5.7的版本更改方式并不一致

```
use mysql;
-- 设置默认密码为空
update user set authentication_string='' where user='root';
-- 设置空密码为root
alter user 'root'@'localhost' identified with mysql_native_password by 'root'
```

以上的设置可以更改默认密码

更改完成后重启服务

`service mysql restart`
=======
## 数据备份

采用mysqldump命令备份

```mysql
mysqldump -u username -p dbname [tbname ...]> filename.sql
mysqldump -uroot -p mountain > /home/r/Documents/mountain.sql
```

对上述语法参数说明如下：

- username：表示用户名称；
- dbname：表示需要备份的数据库名称；
- tbname：表示数据库中需要备份的数据表，可以指定多个数据表。省略该参数时，会备份整个数据库；
- 右箭头“>”：用来告诉 mysqldump 将备份数据表的定义和数据写入备份文件；
- filename.sql：表示备份文件的名称，文件名前面可以加绝对路径。通常将数据库备份成一个后缀名为`.sql`的文件。


注意：mysqldump 命令备份的文件并非一定要求后缀名为`.sql`，备份成其他格式的文件也是可以的。例如，后缀名为`.txt`的文件。通常情况下，建议备份成后缀名为`.sql` 的文件。因为，后缀名为`.sql`的文件给人第一感觉就是与数据库有关的文件。

>>>>>>> 78271b0632b1df8907bac51e11ba6250809bd170
