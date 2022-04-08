+++
date = "2022-04-08T12:10:00+02:00"
archives = ["2022/04"]
tags = ["Nginx"]
categories = ["Nginx"]
title = "Nginx error : could not build the server_names_hash, you should increase server_names_hash_bucket_size"
author = "Leonidas Simopoulos"
image = "banners/nginx.png"
+++



*  **Error:**  
```
[emerg]could not build the server_names_hash, 
you should increase server_names_hash_bucket_size
```

* **Solution:**

In nginx.conf :

```

http {
	include       /etc/nginx/mime.types;
	default_type  application/octet-stream;
	# --- Add these two lines --- 
	server_names_hash_bucket_size 128;
	server_names_hash_max_size 1024;
			.
			. 
	}
```

