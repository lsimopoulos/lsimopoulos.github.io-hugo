+++
date = "2022-12-15T22:43:00+02:00"
archives = ["2022/12"]
tags = ["Azure"]
categories = ["Azure","Linux"]
description = "Azure Ubuntu vm - Update the user's ssh key"
title = "Azure Ubuntu vm - Update the user's ssh key"
author = "Leonidas Simopoulos"
image = "banners/Azure.png"
+++



```
az account set --subscription subscriptionId
az vm user update  --resource-group TargetResourceGroup  --name NameOfVM  --username NameOfAdmin --ssh-key-value ~newkey.pub

```

