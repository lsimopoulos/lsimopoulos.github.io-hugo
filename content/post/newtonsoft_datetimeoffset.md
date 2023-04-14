+++
date = "2022-09-15T11:50:00+02:00"
archives = ["2022/09"]
tags = ["Json.NET"]
categories = ["Json.NET"]
title = "Json.NET : Serialization handling of DateTimeOffset"
author = "Leonidas Simopoulos"
image = "banners/newtonsoft.png"
+++


In the Startup.cs :

```
   public void ConfigureServices(IServiceCollection services)
   {
        services.AddControllers().AddJsonOptions(options =>
        {
            options.SerializerSettings.DateTimeZoneHandling = DateTimeZoneHandling.Utc;
            options.SerializerSettings.DateParseHandling = DateParseHandling.DateTimeOffset;
            options.SerializerSettings.DateFormatHandling = DateFormatHandling.IsoDateFormat;

        });

   }

```

