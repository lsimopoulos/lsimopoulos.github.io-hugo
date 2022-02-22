+++
date = "2022-02-22T13:33:00+02:00"
archives = ["2022/02"]
tags = ["MessagePack","HttpClient"]
categories = ["MessagePack"]
description = "MessagePack and HttpClient"
title = "MessagePack and HttpClient"
author = "Leonidas Simopoulos"
+++



* Controller method
```
   public async Task<IActionResult> SomeApiMethod()
   {
        try
        {
            using var ms = new MemoryStream();
            await Request.Body.CopyToAsync(ms);
            var  someClass = MessagePackSerializer.Deserialize<SomeClass>(ms.ToArray());
            //do something
		}	
        catch (Exception e)
        {
            return BadRequest(e.Message);
        }

        return Ok();
    }
```
    

*  HttpClient posts a class using MessagePack for serialization
```
    using var scope = serviceProvider.CreateScope();
    var httpClientFactory = scope.ServiceProvider.GetService<IHttpClientFactory>();
	var httpClient = httpClientFactory.CreateClient();
	var someClass = new SomeClass();
    var data = MessagePackSerializer.Serialize(someClass);
    var byteArrayContent = new ByteArrayContent(data);
    await httpClient.PostAsync($"{baseUrl}/api/controller/SomeApiMethod",
                                byteArrayContent);

```
