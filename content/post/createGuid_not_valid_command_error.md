+++
date = "2017-07-15T22:08:32+02:00"
categories = ["Visual Studio"]
tags = ["visual studio"]
title = "Create GUID: The command is not a valid executable"
author = "Leonidas Simopoulos"
archives= ["2017/07"]
image = "banners/vstudio.jpg"
+++

My hdd died two days ago and  I re-installed windows 10 Pro(64 bit) and Visual Studio 2017. While I was programming today for one project  I came across with the following error : "The command is not a valid executable". I did try to find the "genguid.exe" on the path "C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools\" but the exe was not there.

![error](/images/vs_guid_error.jpg)


I googled around and I found this [site](https://developercommunity.visualstudio.com/content/problem/4852/create-guid-utility-doesnt-work.html). Apparently you need to install the Desktop Developement with C++ in order the CreateGuid to work(see the above image).

![install Desktop Developement with C++](/images/c++.jpg)

