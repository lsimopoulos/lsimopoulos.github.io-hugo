+++
date = "2022-10-10T22:00:00+02:00"
archives = ["2022/10"]
tags = ["GRPC","Proto"]
categories = ["GRPC"]
description = "Grpc web error:  google.protobuf.Empty is not defined."
title =  "Grpc web  getting  error _google.protobuf.Empty is not defined."
author = "Leonidas Simopoulos"
image = "banners/grpc.png"
+++


* Error :
```
error : "google.protobuf.Empty" is not defined.
```
* Solution 
```
protoc -I {proto_path}\include --proto_path=proto --js_out=import_style=commonjs,binary:proto --grpc-web_out=import_style=commonjs,mode=grpcwebtext:proto pathToProto/someproto.proto
```

