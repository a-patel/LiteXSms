
# LiteX Nexmo Sms
LiteX.Sms.Nexmo is a sms library which is based on LiteX.Sms.Core and Nexmo Sms API.
      
Allow sending texts via Nexmo.
      
Wrapper around Nexmo api to send sms messages from any type of application.

Small library for manage sms with Nexmo. A quick setup for Nexmo Sms.

Wrapper library is just written for the purpose to bring a new level of ease to the developers who deal with Nexmo integration with your system.


## Basic Usage


### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.Sms.Nexmo/).

```Powershell
PM> Install-Package LiteX.Sms.Nexmo
```

##### AppSettings
```js
{  
  //LiteX Nexmo Sms settings
  "NexmoConfig": {
    "ApiKey": "--- REPLACE WITH YOUR Nexmo ApiKey ---",
    "ApiSecret": "--- REPLACE WITH YOUR Nexmo ApiSecret ---",
    "ApplicationId": "--- REPLACE WITH YOUR Nexmo ApplicationId ---",
    "ApplicationKey": "--- REPLACE WITH YOUR Nexmo ApplicationKey ---",
    "FromNumber": "--- REPLACE WITH Nexmo From Number ---",
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
        // 1. Use default configuration from appsettings.json's 'NexmoConfig'
        services.AddLiteXNexmoSms();

        //OR
        // 2. Load configuration settings using options.
        services.AddLiteXNexmoSms(option =>
        {
            option.ApiKey = "";
            option.ApiSecret = "";
            option.ApplicationId = "";
            option.ApplicationKey = "";
            option.FromNumber = "";
            option.EnableLogging = true;
        });

        //OR
        // 3. Load configuration settings on your own.
        // (e.g. appsettings, database, hardcoded)
        var nexmoConfig = new NexmoConfig()
        {
            ApiKey = "",
            ApiSecret = "",
            ApplicationId = "",
            ApplicationKey = "",
            FromNumber = "",
            EnableLogging = true
        };
        services.AddLiteXNexmoSms(nexmoConfig);        
        
        
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
