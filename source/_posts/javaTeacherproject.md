---
title: Java与SQL server 2012搭建教师管理系统
date: 2019-9-10 17:16:36
categories: 编程语言
tags:
   - java
   - 实践
cover: https://i.loli.net/2019/09/14/uQEK2PFhZH9qgBL.png
---
这是我大二暑假的一次实训，利用Java和SQL server 2012搭建一个教师管理系统。我觉得比较有意思就把过程记录一下

## 设计介绍

### 设计环境与要求
本系统前端采用java swing来进行数据展示，后端采用sql sever来存储数据库。  
（1）swing技术
Swing技术是一个用于开发Java应用程序用户界面的开发工具包。
其以抽象窗口工具包(AWT)为基础使跨平台应用程序可以使用任何可插拔的外观风格。Swing开发人员只用很少的代码就可以利用Swing丰富、灵活的功能和模块化组件来创建优雅的用户界面。 工具包中所有的包都是以swing作为名称。  
（2）sql server
SQL Server是一个全面的数据库平台，使用集成的商业智能 (BI) 工具提供企业级的数据管理。
SQL Server数据库引擎为关系型数据和结构化数据提供了更安全可靠的存储功能，可以构建和管理用于业务的高可用和高性能的数据应用程序。

## 设计内容
### 功能概述

本系统是一款基于java swing技术的简单的教师信息管理系统系统，主要有两大模块，其中用户管理模块有：登录，注册，忘记密码，修改密码；教师管理界面有查询，添加，修改，删除，具体如图所示。

![](https://i.loli.net/2019/09/15/c7brsFzxleNT1uC.jpg)

### 数据库结构设计

本系统创建了一个名叫teacher的数据库，在该数据库中有2张表，分别是teacherinfo表和userinfo表。用户表包括了id，uid，pwd等字段信息，具体如表2-1所示。教师信息表包括了no，name，sex，birthdate，tel，prof，department等信息，具体如表2-2所示。

![](https://i.loli.net/2019/09/15/njf4qdD81Z35c6i.png)

数据库设计需要用到SQL server 2012[安装教程](https://blog.csdn.net/jiachang98/article/details/82874358)


## 界面设计与实现

## 连接数据库

> 首先导入sqljdbc4.jar

```java
import java.sql.Connection;//连接类
import java.sql.DriverManager;//驱动管理类
import java.sql.PreparedStatement;//执行sql
import java.sql.ResultSet;
import java.sql.SQLException;
public class DbAccess {
    //连接数据库
	Connection dbConn=null;
	ResultSet rs=null;//数据记录集，记录返回的结果
	PreparedStatement ps=null;

	public void connect()//测试是否跟数据库连通
	{
		try
		{
			//注册驱动
			Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
			//连接
			String url="jdbc:sqlserver://127.0.0.1:1433;DatabaseName=teacher";
			String dbName="sa";
			String dbPwd="123456";
			dbConn=DriverManager.getConnection(url,dbName,dbPwd);
			System.out.println("连接成功");
		}
		catch(Exception e)
		{
			System.out.println("连接失败");

		}
	}
	public void closeAll()//把所有对象关闭释放
	{
		try
		{
			if(rs!=null)
			{
				rs.close();
			}
			if(ps!=null)
			{
				ps.close();
			}
			if(dbConn!=null)
			{
				dbConn.close();
			}
		}
		catch(Exception e)
		{
			e.printStackTrace();
		}
	}
	//执行更新记录，删除、添加、修改
	//insert into table (field1,field2,...) values(value1,value2,...)
	//delete from table where 条件
	//update table set field1=value1,field2=value2...where 条件
	//预处理方法的sql
	//insert into table (field1,field2,...) values(?,?,...)
	//delete from table where field=?
	//update table set field1=?,field2=?...where 条件
   public int extUpdate(String sql,Object[] objs)
   //sql表示你要传入的预处理sql语句，objs表示你要传入的参数值
   {
	   int count=0;
	   try{
		   //(1)连接
		   connect();
		   //(2)根据传入的sql生成一个预处理sql对象
		   ps=dbConn.prepareStatement(sql);
		   //(3)参数值设置
		   for(int i=0;i<objs.length;i++)
			   ps.setObject(i+1,objs[i]);//组装完成了完整的sql语句
		   //(4)执行sql语句
		   count=ps.executeUpdate();
		   //(5)关闭
		   closeAll();
	   }
	   catch(Exception e)
	   {
		   e.printStackTrace();
	   }
	   return count;
   }
   //查询，返回记录集
   public ResultSet exeQuery(String sql,Object[] objs)
   {
	   try
	   {
		   //(1)连接
		   connect();
		   //(2)根据传入的sql生成一个预处理sql对象
		   ps=dbConn.prepareStatement(sql);
		   //(3)参数值设置
		   for(int i=0;i<objs.length;i++)
			   ps.setObject(i+1,objs[i]);//组装完成了完整的sql语句
		   //(4)执行sql语句
		  rs=ps.executeQuery();
	   }
	   catch(Exception e)
	   {
		   e.printStackTrace();
	   }
	   return rs;
   }
```

测试
