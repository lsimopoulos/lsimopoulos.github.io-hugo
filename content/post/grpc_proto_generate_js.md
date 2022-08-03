+++
date = "2022-06-10T20:47:00+02:00"
archives = ["2022/06"]
tags = ["GRPC","Proto"]
categories = ["GRPC"]
description = "Generate js files with protoc for GRPC web on Windows"
title = "Generate js files with protoc for GRPC web on Windows"
author = "Leonidas Simopoulos"
image = "banners/grpc.png"
+++


* Download [protoc](https://github.com/protocolbuffers/protobuf/releases/tag/v3.20.0)
* Download [protoc-gen-grpc-web](https://github.com/grpc/grpc-web/releases)
* Add to system environment variable PATH  the path to protoc-gen-grpc-web for example : C:\protoc-gen-grpc-web\
* Then run on powershell or windows command the following command :
```
protoc --proto_path=proto --js_out=import_style=commonjs,binary:proto --grpc-web_out=import_style=commonjs,mode=grpcwebtext:proto pathToProto/myProto.proto
```

