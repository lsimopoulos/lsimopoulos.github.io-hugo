+++
date = "2022-04-01T20:04:12+02:00"
archives = ["2022/04"]
categories = ["Android"]
tags = ["Android"]
title = "Android: actionbar back button is showing in preview not on mobile"
image = "banners/android.jpg"
+++

* **Solution**

```
<android.support.v7.widget.Toolbar
    android:id="@+id/toolbarId"
    android:layout_width="match_parent"
    android:layout_height="?attr/actionBarSize"
    android:focusable="true"
    android:focusableInTouchMode="true"
    android:theme="@style/ToolBarStyle"
    app:navigationIcon="?attr/homeAsUpIndicator" />


<style name="ToolBarStyle" parent="Theme.AppCompat.Light.NoActionBar">
    <item name="colorControlNormal">@android:color/white</item>
</style>
```