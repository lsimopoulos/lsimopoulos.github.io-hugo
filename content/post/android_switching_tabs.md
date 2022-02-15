+++
date = "2018-08-10T8:20:23+02:00"
categories = ["Android"]
tags = ["Android","lagging swiping tabs" ,"viewPager"]
title = "Android: lagging when switching/swiping between tabs"
archives= ["2018/10"]
image = "banners/android.jpg"
+++

If a lag is experienced when swiping between pages on a ViewPager :
 
```
viewPager.setOffscreenLimit(size) 
```

Where size : the number of pages