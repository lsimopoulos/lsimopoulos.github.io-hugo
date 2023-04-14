+++
date = "2022-11-25T10:00:00+02:00"
archives = ["2022/11"]
categories = ["Entity Framework Core"]
tags = ["entity framework core"]
title = "Run a raw sql query/command via EF Core"
description = "How to run a  raw sql query/command via EF Core"
author = "Leonidas Simopoulos"
image = "banners/entity-framework.png"
+++

There are different ways to run a SQL command/query in Entity Framework Core. 



1.**DbSet.FromSqlRaw**

```
var parentsList =  context.Parents
						.FromSqlRaw("Select * from dbo.Parents  where IsRich = 0 ")
						.ToList();			
```

2.**DbSet.SqlQuery*


```
 var countOfParents =  context.Database.SqlQuery<int>("Select Count(*) from dbo.Parents where IsRich = 0");
```

3.**Database.ExecuteSql**


```
 var numberOfAffectedEtntities = context.Database.ExecuteSqlCommand("DELETE FROM dbo.Parents WHERE Id = 1");
```

4.**Database.Database.ExecuteSqlRaw**


```
 var numberOfAffectedEtntities = context.Database.ExecuteSqlRaw("DELETE FROM dbo.Parents WHERE Id = 1");
```