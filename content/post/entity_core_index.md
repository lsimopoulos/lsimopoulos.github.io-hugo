+++
date = "2022-03-15T18:00:00+02:00"
archives = ["2022/03"]
categories = ["Entity Framework Core"]
tags = ["entity framework core"]
title = "Configure an unique Index in entity framework core"
author = "Leonidas Simopoulos"
image = "banners/entity-framework.png"
+++


1.**Attributes**



```
[Index(nameof(Name),nameof(Uuid), IsUnique = true, Name = "SomeIndex")]
public class Server
{
	public int Id { get; set; }
    public string Name { get; set; }
	public string SomeUid { get; set; }
}
```

2.**Fluent Api**

* In the ApplicationDbContext override the method OnModelCreating and add the following code:

```
protected override void OnModelCreating(DbModelBuilder modelBuilder)
{
   modelBuilder.Entity<Server>(entity =>
              entity
                  .HasIndex(i => new {i.Name, i.SomeUid})
                  .IsUnique()
                  .HasName("SomeIndex"));

}
```
