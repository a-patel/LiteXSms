
# LiteX Sinch Sms
> LiteX.Sms.Sinch is a sms library which is based on LiteX.Sms.Core and Sinch Sms API.
      
Allow sending texts via Sinch API.
      
Wrapper around Sinch api to send sms messages from any type of application.

Small library for manage sms with Sinch. A quick setup for Sinch Sms.

Wrapper library is just written for the purpose to bring a new level of ease to the developers who deal with Sinch integration with your system.


## Basic Usage

### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.Sms.Sinch/).

```Powershell
PM> Install-Package LiteX.Sms.Sinch
```

##### AppSettings
```js
{  
  //LiteX Sinch Sms settings
  "SinchConfig": {
    "ApiKey": "--- REPLACE WITH YOUR Sinch ApiKey ---",
    "ApiSecret": "--- REPLACE WITH YOUR Sinch ApiSecret ---",
    "FromNumber": "--- REPLACE WITH Sinch From Number ---",
    "EnableLogging": true
  }
}
```

##### Configure Startup Class
```cs
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // 1. Use default configuration from appsettings.json's 'SinchConfig'
        services.AddLiteXSinchSms();

        //OR
        // 2. Load configuration settings using options.
        services.AddLiteXSinchSms(option =>
        {
            option.ApiKey = "";
            option.ApiSecret = "";
            option.FromNumber = "";
            option.EnableLogging = true;
        });

        //OR
        // 3. Load configuration settings on your own.
        // (e.g. appsettings, database, hardcoded)
        var sinchConfig = new SinchConfig()
        {
            ApiKey = "",
            ApiSecret = "",
            FromNumber = "",
            EnableLogging = true
        };
        services.AddLiteXSinchSms(sinchConfig);
        
        
        // add logging (optional)
        services.AddLiteXLogging();
    }
}
```

### Sample Usage Example
> Same for all providers. 

For more helpful information about LiteX Sms, Please click [here.](https://github.com/a-patel/LiteXSms/blob/master/README.md#step-3--use-in-controller-or-business-layer-memo)


### Coming soon...
* Voice Sms
* Bulk Sms

