+++
date = "2022-01-15T10:47:00+02:00"
archives = ["2022/01"]
tags = ["MSSQL"]
categories = ["MSSQL"]
description = "SQL tips"
title = "SQL Tips"
author = "Leonidas Simopoulos"
image = "banners/sql.png"
+++


# SQL Tips 
<!--more-->
* ##  Check if a column contains a string



```
SELECT [DatabaseId]
      ,[Category]
  FROM [dbo].[SomeTable]
  Where Category LIKE '%theString%'
```


* ## Run a sql command multiple times

```
  INSERT INTO [dbo].[SomeTable] (
   	Type, Message,	Time
)
VALUES
    (
	'some type',' some message', '2022-04-27 09:51:22.0000000 +01:00'
	)
	
GO 10000000
```
