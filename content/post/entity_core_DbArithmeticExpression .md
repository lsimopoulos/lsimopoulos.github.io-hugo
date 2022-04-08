+++
date = "2022-03-30T22:50:23+02:00"
archives = ["2022/03"]
categories = ["Entity Framework Core"]
tags = ["entity framework core"]
title = "DbArithmeticExpression arguments must have a numeric common type"
author = "Leonidas Simopoulos"
image = "banners/entity-framework.png"
+++

* Error

```
System.ArgumentException: DbArithmeticExpression arguments must have a numeric common type.
```

* Code caused the exception

```
ctx.Incidents
   .Where(x => (DateTime.Now - x.Time).Days == 0)
   .OrderByDescending(d => d.Time)
   .Take(50)
   .ToList();
```

* Solution:

```
ctx.Incidents
   .Where(x => DbFunctions.DiffDays(DateTime.Now ,x.Time) == 0)
   .OrderByDescending(d => d.Time)
   .Take(50)
   .ToList();
```