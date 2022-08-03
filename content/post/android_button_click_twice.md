+++
date = "2022-05-11T21:54:12+02:00"
archives = ["2022/05"]
categories = ["Android"]
tags = ["Android"]
title = "Android: button needs to be clicked twice"
description = "Android: button needs to be clicked twice"
image = "banners/android.jpg"
+++

When the button needs to clicked twice in order to be effective:

* **Solution**

```
android:focusable="true"
android:focusableInTouchMode="true" 
```