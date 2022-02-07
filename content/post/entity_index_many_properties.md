+++
date = "2017-07-05T19:02:53+02:00"
archives = ["2017/07"]
categories = ["Entity Framework"]
tags = ["entity framework"]
title = "Configure an Index on many properties in entity framework 6.1"
author = "Leonidas Simopoulos"
image = "banners/entity-framework.png"
+++

There are few ways to configure an Index on more than one property in the entity framework 6.1. I created a new WebApplication project from Visual Studio and I selected MVC. 



1.**Attributes**


For this tutorial I am going to create two models: Server and Instance.

```
public class Server
{
	public int Id { get; set; }
    public string Name { get; set; }
}

public class Instance
{
	public int Id { get; set; }
    public string Name { get; set; }
}
```
* Modify the ApplicationUser class:

```
public class ApplicationUser : IdentityUser
{
	public async Task<ClaimsIdentity> GenerateUserIdentityAsync(UserManager<ApplicationUser> manager)
	{
		// Note the authenticationType must match the one defined in CookieAuthenticationOptions.AuthenticationType
		var userIdentity = await manager.CreateIdentityAsync(this, DefaultAuthenticationTypes.ApplicationCookie);
		// Add custom user claims here
		return userIdentity;
    }
	
    public Server Server { get; set; }

    ForeignKey(nameof(Server))]
    [Index("IX_ServerInstance", 1, IsUnique = true)]
    public int ServerId { get; set; }


    public Instance Instance { get; set; }

    [ForeignKey(nameof(Instance))]
    [Index("IX_ServerInstance", 2, IsUnique = true)]
    public int InstanceId { get; set; }
}
```

**IMPORTANT NOTE**

If the property  "instaceId" was a string , the [MaxLength(somenumber)] attribute would be needed to be applied. 

For example:


```
	[MaxLength(50)]
	[Index("IX_ServerInstance", 2, IsUnique = true)]
    public string InstanceName { get; set; }
```



2.**Fluent Api**

* In the ApplicationDbContext override the method OnModelCreating and add the following code:

```
protected override void OnModelCreating(DbModelBuilder modelBuilder)
{
    modelBuilder
        .Entity<ApplicationUser>()
        .Property(t => t.ServerId)
        .HasColumnAnnotation(
            IndexAnnotation.AnnotationName,
            new IndexAnnotation(
                new IndexAttribute("IX_FirstNameLastName", 1) { IsUnique = true }));

     modelBuilder
        .Entity<ApplicationUser>()
        .Property(t => t.InstanceId)
        .HasColumnAnnotation(
            IndexAnnotation.AnnotationName,
            new IndexAnnotation(
                ew IndexAttribute("IX_ServerInstance", 2) { IsUnique = true }));

}
```

3.**Migrations**

If a migration is created( Add-Migration) and 1st way(with the attribute) was used, the following code is generated automatically:

```
 CreateTable(
                "dbo.AspNetUsers",
                c => new
                    {
                        Id = c.String(nullable: false, maxLength: 128),
                        ServerId = c.Int(nullable: false),
                        InstanceId = c.Int(nullable: false),
                        Email = c.String(maxLength: 256),
                        EmailConfirmed = c.Boolean(nullable: false),
                        PasswordHash = c.String(),
                        SecurityStamp = c.String(),
                        PhoneNumber = c.String(),
                        PhoneNumberConfirmed = c.Boolean(nullable: false),
                        TwoFactorEnabled = c.Boolean(nullable: false),
                        LockoutEndDateUtc = c.DateTime(),
                        LockoutEnabled = c.Boolean(nullable: false),
                        AccessFailedCount = c.Int(nullable: false),
                        UserName = c.String(nullable: false, maxLength: 256),
                    })
                .PrimaryKey(t => t.Id)
                .ForeignKey("dbo.Instances", t => t.InstanceId, cascadeDelete: true)
                .ForeignKey("dbo.Servers", t => t.ServerId, cascadeDelete: true)
                .Index(t => new { t.ServerId, t.InstanceId }, unique: true, name: "IX_ServerInstance")
                .Index(t => t.UserName, unique: true, name: "UserNameIndex");
``` 

But it's possible to create index on many properties on a later migration. For example on the up method of the new migration the following code is needed to be added:

```
//Another alternative 
CreateIndex("dbo.AspNetUsers", new []{ "ServerId", "InstanceId" },true, "IX_ServerInstance");
```

***Result***

![SQL Index](/images/Inxex_SQL.JPG)

![Error when trying to insert an entry with same indexes](/images/Index_constraint.JPG)


***References***
[MSDN](https://msdn.microsoft.com/en-us/data/jj591617.aspx#PropertyIndex)
