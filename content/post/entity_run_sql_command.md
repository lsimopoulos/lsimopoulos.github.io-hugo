+++
date = "2022-11-01T19:02:53+02:00"
archives = ["2022/11"]
categories = ["Entity Framework"]
tags = ["entity framework"]
title = "Run a raw sql query/command via EF 6"
description = "How to run a  raw sql query/command via EF 6"
author = "Leonidas Simopoulos"
image = "banners/entity-framework.png"
+++

There are different ways to run a SQL command/query via Entity framework. 



1.**SqlQuery**

In the entity(table) level :
```
var parentsList =  context.Parents
						.SqlQuery("Select * from dbo.Parents  where IsRich = 0 ")
						.ToList();			
```
or in the database level:

```
 var parentsList =  context.Database.SqlQuery<string>("Select * from dbo.Parents where IsRich = 0")
                              .ToList<Parents>();
```

2.**ExecuteSqlCommand*


```
  var numberOfAffectedEtntities = context.Database.ExecuteSqlCommand(" "DELETE FROM Parents WHERE Id = 1";");
```

3.**ObjectQuery.Execute**

Old way(deprecated)
```
var objectContext = ((IObjectContextAdapter)context).ObjectContext;
var objectSet = objectContext.CreateObjectSet<Parent>();

var queryString = @"SELECT VALUE p FROM Parent AS p WHERE p.IsRich = @IsRich";
var parentQuery = objectContext.CreateQuery<Product>(queryString, new ObjectParameter("IsRich", 0);
var parentResults = parentQuery.Execute(MergeOption.AppendOnly);
``