# Takeaways
+ mysql本质上是一个软件
+
| MySQL      | 认知 |
| ----------- | ----------- |
| 数据库database      | 文件夹       |
| 数据表table   | 文件(Excel)        |
# 如何初次使用
+ 下载免安装软件包
+ 初始化，包括定义port，生成data文件夹
+ **运行服务** ```net start/stop service```
+ 用工具连接并发送指令给mysql，有不同工具
## 使用mysql自带工具启动后
+ 添加mysql bin到path
+ 使用```mysql -u root -p```进入软件环境
+ 设置密码 ```set password = password("root123");```
+ 查看已有文件夹（数据库）```show databases;```
+ 关闭连接 ```exit```
## 忘记密码咋办？
1. 关闭service

# MySQL指令
## 查看已有的数据库（文件夹）
```show databases;```
## 创建数据库（文件夹）
```create database name;```
## 删除数据库（文件夹）
```drop```
## 进入数据库（文件夹）
```use```
## 查看数据库中的数据表（文件）
```show tables;```

