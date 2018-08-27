
# LiteX Twilio Sms
> LiteX.Sms.Twilio is a sms library which is based on LiteX.Sms.Core and Twilio Sms API.

Allow sending texts sms via Twilio.

This client library enables working with the Twilio API to sending text messages.

Small library to abstract sending text messages to Twilio API. Quick setup for Twilio API and very simple wrapper for the Twilio API to text messages.

Very simple configuration in advanced ways. Purpose of this package is to bring a new level of ease to the developers who deal with Twilio API integration with their system.



## Basic Usage

### Install the package

> Install via [Nuget](https://www.nuget.org/packages/LiteX.Sms.Twilio/).

```Powershell
PM> Install-Package LiteX.Sms.Twilio
```

##### AppSettings
```js
{
  //LiteX Twilio Sms settings
  "TwilioConfig": {
    "AccountSid": "--- REPLACE WITH YOUR Twilio SID ---",
    "AuthToken": "--- REPLACE WITH YOUR Twilio Auth Token ---",
    "FromNumber": "--- REPLACE WITH Twilio From Number ---",
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
        // 1. Use default configuration from appsettings.json's 'TwilioConfig'
        services.AddLiteXTwilioSms();

        //OR
        // 2. Load configuration settings using options.
        services.AddLiteXTwilioSms(option =>
        {
            option.AccountSid = "";
            option.AuthToken = "";
            option.FromNumber = "";
            option.EnableLogging = true;
        });

        //OR
        // 3. Load configuration settings on your own.
        // (e.g. appsettings, database, hardcoded)
        var twilioConfig = new TwilioConfig()
        {
            AccountSid = "",
            AuthToken = "",
            FromNumber = "",
            EnableLogging = true
        };
        services.AddLiteXTwilioSms(twilioConfig);        
        
        
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

