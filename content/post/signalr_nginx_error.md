+++
date = "2022-07-17T23:47:00+02:00"
archives = ["2022/07"]
tags = ["SignalR","Nginx"]
categories = ["Nginx"]
description = "Nginx and SignalR:This endpoint is only for web-socket requests' when status code '101' was expected"
title = "Nginx and SignalR:This endpoint is only for web-socket requests' when status code '101' was expected"
author = "Leonidas Simopoulos"
image = "banners/nginx.png"
+++

### Error ###

```
The server returned status code '200 This endpoint is only for web-socket requests' when status code '101' was expected
```
or
```
The server returned status code '400 This endpoint is only for web-socket requests' when status code '101' was expected
```
### Cause and soluion ###
```
location ~ ^/server(.*)$ {
	  proxy_ssl_server_name on;
      proxy_ssl_session_reuse off;
      proxy_ssl_verify off;
      #the response is sent to the client synchronously.
      proxy_buffering off;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      set $url https://serveraddress$1$is_args$args;
      proxy_pass $url;
	
-->	  location  /server/signalr {
		# Configure WebSockets
		proxy_pass https://serveraddress/sr;
	
		# Configuration for WebSockets
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection $connection_upgrade;
		proxy_cache off;
	
		# WebSockets were implemented after http/1.0
		proxy_http_version 1.1;
	
		# Configuration for ServerSentEvents
		proxy_buffering off;
	
		# Configuration for LongPolling or if your KeepAliveInterval is longer than 60 seconds
		proxy_read_timeout 100s;
	
		proxy_set_header Host $host;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-Forwarded-Proto $scheme;
	  }
}
```

After i moved out the nested location, signalr works with nginx as reverse proxy.Here how it looks like :

```
location  /server/signalr {
	  # Configure WebSockets
      proxy_pass https://serveraddress/sr;

      # Configuration for WebSockets
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection $connection_upgrade;
      proxy_cache off;

      # WebSockets were implemented after http/1.0
      proxy_http_version 1.1;

      # Configuration for ServerSentEvents
      proxy_buffering off;

      # Configuration for LongPolling or if your KeepAliveInterval is longer than 60 seconds
      proxy_read_timeout 100s;

      proxy_set_header Host $host;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;
}
location ~ ^/server(.*)$ {
      proxy_ssl_server_name on;
      proxy_ssl_session_reuse off;
      proxy_ssl_verify off;
      #the response is sent to the client synchronously.
      proxy_buffering off;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      set $url https://serveraddress$1$is_args$args;
      proxy_pass $url;
}
```