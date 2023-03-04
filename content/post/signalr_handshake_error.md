+++
date = "2022-07-13T23:47:00+02:00"
archives = ["2022/07"]
tags = ["SignalR"]
categories = ["SignalR"]
description = "SignalR:Failed connection handshake"
title = "SignalR:Failed connection handshake"
author = "Leonidas Simopoulos"
image = "banners/signalr.png"
+++

### Error ###

```
Error : [Debug] Microsoft.AspNetCore.SignalR.HubConnectionContext Failed connection handshake.
System.ArgumentOutOfRangeException: Specified argument was out of the range of valid values. (Parameter 'delay')
at System.Threading.CancellationTokenSource.CancelAfter(TimeSpan delay)
at Microsoft.AspNetCore.SignalR.HubConnectionContext.HandshakeAsync(TimeSpan timeout, IReadOnlyList`1 supportedProtocols, IHubProtocolResolver protocolResolver, IUserIdProvider userIdProvider, Boolean enableDetailedErrors)
```

### Cause ###
```
 services.AddSignalR(options =>
                {
                    options.EnableDetailedErrors = true;
            ---->   options.HandshakeTimeout = TimeSpan.MaxValue;
                })
         .AddMessagePackProtocol();
```
In my case due to network latency I had set HandshakeTimeout to  TimeSpan.MaxValue, which caused the error. 