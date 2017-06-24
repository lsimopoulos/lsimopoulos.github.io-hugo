+++
date = "2017-06-24T13:20:43+02:00"
categories = ["Android"]
tags = ["Android","emulator","connection timeout error"]
title = "Android: connection timeout error on emulator"
+++

Usually when I am developing mobile apps, I host the server on the cloud. But this time I decided to host it locally on the same machine where I'm developing the android app.
When I tried to connect to the local webserver from the android emulator by using the local ip, I got connection timeout error after few seconds. 



What did I  try and it did not work:
-----------------
* Made sure that the required ports of firewall were open.
* Increased the timeout of the httpclient.
* Made sure that the android manifest included the following lines:

	```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
	```

	
How did I solve the problem
-----------------
After googling around, I found in the official android [website](https://developer.android.com/studio/run/emulator-networking.html)  that : 

"
	Each instance of the emulator runs behind a virtual router/firewall service that isolates it from your development machine network interfaces
	and settings and from the internet. An emulated device can't see your development machine or other emulator instances on the network. Instead,
	it sees only that it is connected through Ethernet to a router/firewall.
"


Since I was using my local IP on the address, the emulator could not access it and got the connection timeout error. If I had used the external IP  and  the port was open I would not have gotten this error but it's not the best approach.
Therefore whenever you want to access the server that is hosted on the same machine, just use ```10.0.2.2```.  


![Android](/images/android.png)


