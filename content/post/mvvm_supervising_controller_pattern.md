+++
date = "2017-06-26T20:11:26+02:00"
categories = ["MVVM", "WPF","UWP"]
tags = ["mvvm","wpf","UWP", "wpf","xamarin"]
title = "Supervising controller pattern and MVVM"
+++

I have been familiar with MVVM framework since the era of Silverlight. Since then I am always try to follow the approach clean code behind when it's achievable.
One of the big benefits of mvvm is that ,except of the separation of concern, you can make unit tests covering all the logics in the ViewModels.  


When using the mvvm pattern sometimes you encounter some challenges. Some functions need to be defined on the code behind which are tight coupled with GUI and include some logic. 
In these cases  you need to try to separate the logic from the code behind and move the it to the VM. 

Martin Fowler introduced the design pattern called [Supervising Controller](https://martinfowler.com/eaaDev/SupervisingPresenter.html). 

"Factor the UI into a view and controller where the view handles simple mapping to the underlying model and the the controller handles input response and complex view logic."

I am going to present  how can you implement the Supervising Controller pattern on MVVM and tackle the aforementioned challenges.

* First create an interface  ```IInterface.cs```


```
public interface IInterface
{
	void DoSomething();
}
```


* In the code behind of the view :

```
public partial class View : UserControl, IInterface
{
    public View()
	{
		((ViewModel)DataContext).View = this as IInterface;
    }
	
	public void DoSomething()
	{
		//implement the gui related functionality here
    }
}
```

* In the viewmodel :


```

public IInterface View
{
	get; set;
}

//You can invoke the method of View from VM
// and implement the logic here
public void DoSomething()
{
	if (View == null) return;
		View.DoSomething();
	//implement the logic here
}
```


***Conclusion***


By applying this design pattern , the logic ,that is tightly coupled with the functionality on the code behind(Probably an event), can be targeted by unit test now and have the logic on the ViewModel. This can be handy at specific cases but of course this should not be applied for every case.
 The disadvantage is that this implementation violates the "rule" : the View should not be aware of the ViewModel and vice versa. 


