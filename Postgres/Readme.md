+ Postgres is the database
+ Structured Query Language: SQL is a programming language for *ralational database*
  + relational database is having relation between two or more tables ![relational tables](https://github.com/elonzhangyl/zixue/blob/main/Postgres/figs/relational_database.png) 除了初始列的id，你会在这一行有另外一个id，用来关联另一个表格。
 

# 数据库操作
## 链接数据库
+ cmd中运行psql进入postgresql（类似进入python） （注意默认的数据库用户名的电脑用户名，但默认的数据库用户名是postgres） psql -U postgres
+ 连接到某个数据库 \c <数据库名字>
+ 命令行必须以**分号结尾**才会运行
+ cmd进入postgresql，再进入username，\l看查看所有database，此时可创建database，然后连接到database，再创建table
## 创建database，table，插入数据
+ CREATE DATABASE <name>
+ ```CREATE TABLE <name> (
  id BIGSERIAL NOT NULL PRIMARY KEY,
  first_name VARCHAR(50) NOT NULL,
  email VARCHAR(100) );```
+ INSERT INTO <table name> (first_name, email)
  VALUES ('Jade', 'jade@gmail.com');
+ \d display all tables and sequences ; \dt only show tables
+ 显示table内容 SELECT * FROM <table name>
+ DROP TABLE <table name>
