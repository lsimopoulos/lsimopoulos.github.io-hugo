+++
date = "2017-07-03T20:11:26+02:00"
categories = ["Xamarin", "WPF", "Autofac", "UWP", "MVVM Light"]
tags = ["mvvm light","autofac","dependency injection", "wpf","xamarin","uwp"]
title = "Integrate Autofac with MVVM Light"
+++

I am going to show how to integrate [Autofac](https://autofac.org/) with the [Mvvm Light](http://www.mvvmlight.net/) easy and quick for most simple scenarios. Autofac is very powerful IOC Container and MVVM Light is one of the best MVVM frameworks. 

1.Create a new project from mvvm light templates in the visual studio

![Project Templates](/images/mvvmlight_project_templates.JPG)
 
2.Install [Autofac](https://www.nuget.org/packages/Autofac/) and  [Autofac.Extras.CommonServiceLocator](https://www.nuget.org/packages/Autofac.Extras.CommonServiceLocator/) as NuGet packages.

3.Expand the folder ViewModel on the SolutionExplorer in the Visual Studio and open the file ViewModelLocator.

![Solution Explorer](/images/ViewmodelLocatorSolutionExplorer.JPG)

4.MVVM Light uses its own IOC container called SimpleIoc. The constructor of the  ViewModelLocator is defined:

```
static ViewModelLocator()
{
    ServiceLocator.SetLocatorProvider(() => SimpleIoc.Default);

    if (!ViewModelBase.IsInDesignModeStatic
        && !UseDesignTimeData)
    {
        // Use this service in production.
        SimpleIoc.Default.Register<IDataService, DataService>();
    }
    else
    {
        // Use this service in Blend or when forcing the use of design time data.
        SimpleIoc.Default.Register<IDataService, DesignDataService>();
    }

    SimpleIoc.Default.Register<MainViewModel>();
}
```

Before the replacement of the SimpleIoc with Autofac, create a folder "Config" and a new c# class called  AutofacConfig :

```
using Autofac;
using SolutionName.ViewModel;

namespace SolutionName.Config
{
    public static class AutofacConfig
    {
        public static IContainer Config()
        {
            var builder = new ContainerBuilder();
			builder.RegisterType<DataService>().As<IDataService>();
            builder.RegisterType<MainViewModel>();
            return builder.Build();
        }

    }
}

```

5.On the ViewModelLocator.cs replace the constructor with following code:

```
static ViewModelLocator()
{
    ServiceLocator.SetLocatorProvider(() => new AutofacServiceLocator(AutofacConfig.Config()));
}
```







