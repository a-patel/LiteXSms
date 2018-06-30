# LiteX Plivo Sms
LiteX.Sms.Plivo is a sms library which is based on LiteX.Sms.Core and Plivo Sms API.
      
Allow sending texts via Plivo.
      
Wrapper around Plivo api to send sms messages from any type of application.

Small library for manage sms with Plivo. A quick setup for Plivo Sms.

Wrapper library is just written for the purpose to bring a new level of ease to the developers who deal with Plivo integration with your system.


## Basic Usage


### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.Sms.Plivo/).

```Powershell
PM> Install-Package LiteX.Sms.Plivo
```

##### AppSettings
```js
{  
  //LiteX Plivo Sms settings
  "PlivoConfig": {
    "AuthId": "--- REPLACE WITH YOUR Plivo Account SID ---",
    "AuthToken": "--- REPLACE WITH YOUR Plivo Auth Token ---",
    "FromNumber": "--- REPLACE WITH Plivo From Number ---",
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
        // 1. Use default configuration from appsettings.json's 'PlivoConfig'
        services.AddLiteXPlivoSms();

        //OR
        // 2. Load configuration settings using options.
        services.AddLiteXPlivoSms(option =>
        {
            option.AuthId = "";
            option.AuthToken = "";
            option.FromNumber = "";
            option.EnableLogging = true;
        });

        //OR
        // 3. Load configuration settings on your own.
        // (e.g. appsettings, database, hardcoded)
        var plivoConfig = new PlivoConfig()
        {
            AuthId = "",
            AuthToken = "",
            FromNumber = "",
            EnableLogging = true
        };
        services.AddLiteXPlivoSms(plivoConfig);        
        
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

