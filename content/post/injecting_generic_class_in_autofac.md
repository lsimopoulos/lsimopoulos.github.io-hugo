+++
date = "2017-07-16T19:47:48+02:00"
archives = ["2017/07"]
categories = ["Autofac"]
tags = ["Autofac"]
title = "Injecting classes that inherit from a generic one in Autofac"
author = "Leonidas Simopoulos"
image = "banners/autofac.jpg"
+++

Lets say we have a generic class defined like :

```
public class Foundation<TClass>  where TClass : class
{
	private readonly InjectedClass _injectedClass;

    protected Foundation(InjectedClass injectedClass)
    {
		_injectedClass = injectedClass;
    }
}
```

Autofac has a method : [RegisterGeneric()](http://docs.autofac.org/en/latest/register/registration.html) we can use in order to register generic classes.

Usage :

```
builder.RegisterGeneric(typeof(Foundation<>)).InstancePerLifetimeScope();
```

This works perfectly but what about the classes that inherit from this generic class? 
For example:


```
public class CustomFoundation<TClass> : Foundation<TClass> where TClass :class
{
	public CustomFoundation(InjectedClass injectedClass) : base(injectedClass)
    {

    }
}
```

Using "RegisterGeneric()"  wont work.

There are few ways to solve this problem :

1.

```
 builder.RegisterAssemblyTypes(typeof(Foundation<>).Assembly)
             .Where(t => t.BaseType!= null && t.BaseType.IsGenericType 
			 && t.BaseType.GetGenericTypeDefinition() == typeof(Foundation<>)));
```

[RegisterAssemblyTypes](http://docs.autofac.org/en/latest/register/scanning.html)  registers all components that are defined within the assembly of the Foundation class. Here we are registering  all the components whose basetype is generic and is type of Foundation.
2.

```
 builder.RegisterAssemblyTypes(typeof(Foundation<>).Assembly)
             .AsClosedTypesOf(typeof(Foundation<>));
```

""According to the api doc of Autofac: The [AsClosedTypesOf](https://autofac.org/apidoc/html/150314CB.htm) specifies that a type from a scanned assembly is registered if it implements an interface that closes the provided open generic interface type.""

3.

```
builder.RegisterAssemblyTypes(typeof(Foundation<>).Assembly)
	.Where(t => t.Name.EndsWith("Foundation"));
```
	
Same logic as the first step but this requires that we have a naming strategy in place and name all the derived class with the ending string "Foundation" such as "ExampleFoundation", "TestFoundation" etc.



	


