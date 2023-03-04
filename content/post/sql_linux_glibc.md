+++
date = "2022-05-20T20:47:00+02:00"
archives = ["2022/05"]
tags = ["MSSQL"]
categories = ["MSSQL"]
description = "SQL installation error on linux : GLIBC_2.27 not found"
title = "SQL installation error on linux : GLIBC_2.27 not found"
author = "Leonidas Simopoulos"
image = "banners/sql.jpg"
+++


* ### Error

```
/opt/mssql/bin/sqlservr: /lib/x86_64-linux-gnu/libc.so.6: version `GLIBC_2.27' not found (required by /opt/mssql/bin/sqlservr)
Initial setup of Microsoft SQL Server failed. Please consult the ERRORLOG
in /var/opt/mssql/log for more information.
```

* ### Solution

```
sudo apt-get install mssql-server=15.0.4023.6-2   
sudo systemctl start mssql-server 
```
