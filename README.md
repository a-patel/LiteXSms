# LiteXSms

> LiteXSms is simple yet powerful and very high-performance sms sending mechanism and incorporating both synchronous and asynchronous usage with some advanced usages which can help us to handle sending sms more easier!



Provide sms service for ASP.NET Core (2.0 and later) applications.

Small library to abstract sms functionalities. Quick setup for any sms provider and very simple wrapper for the widely used sms providers. LiteXSms uses the least common denominator of functionality between the supported providers to send sms solution. Abstract interface to implement any kind of basic sms services. Having a default/generic implementation to wrap the Twilio, Plivo, Nexmo, Sinch. A sms abstraction.

Very simple configuration in advanced ways. Purpose of this package is to bring a new level of ease to the developers who deal with different sms provider integration with their system and implements many advanced features. You can also write your own and extend it also extend existing providers. Easily migrate or switch between one to another provider with no code breaking changes.

LiteXSms is an interface to unify the programming model for various sms providers. The Core library contains all base interfaces and tools. One should install at least one other LiteXSms package to get sms implementation.





## Cache Providers :books:

- [Twilio](docs/Twilio.md) [![](https://img.shields.io/nuget/dt/LiteX.Sms.Twilio.svg)](https://www.nuget.org/packages/LiteX.Sms.Twilio/) [![](https://img.shields.io/nuget/v/LiteX.Sms.Twilio.svg)](https://www.nuget.org/packages/LiteX.Sms.Twilio/)
- [Plivo](docs/Plivo.md) [![](https://img.shields.io/nuget/dt/LiteX.Sms.Plivo.svg)](https://www.nuget.org/packages/LiteX.Sms.Plivo/) [![](https://img.shields.io/nuget/v/LiteX.Sms.Plivo.svg)](https://www.nuget.org/packages/LiteX.Sms.Plivo/)
- [Nexmo](docs/Nexmo.md) [![](https://img.shields.io/nuget/dt/LiteX.Sms.Nexmo.svg)](https://www.nuget.org/packages/LiteX.Sms.Nexmo/) [![](https://img.shields.io/nuget/v/LiteX.Sms.Nexmo.svg)](https://www.nuget.org/packages/LiteX.Sms.Nexmo/)
- [Sinch](docs/Sinch.md) [![](https://img.shields.io/nuget/dt/LiteX.Sms.Sinch.svg)](https://www.nuget.org/packages/LiteX.Sms.Sinch/) [![](https://img.shields.io/nuget/v/LiteX.Sms.Sinch.svg)](https://www.nuget.org/packages/LiteX.Sms.Sinch/)



## Features :pager:

- Async compatible
- Thread safe, concurrency ready
- Multiple provider support (using provider factory)
- Obsolete sync methods
- Interface based API to support the test driven development and dependency injection
- Leverages a provider model on top of ILiteXSmsSender under the hood and can be extended with your own implementation
- Voice Sms



## Basic Usage :page_facing_up:

### Step 1 : Install the package :package:

> Choose one kinds of sms provider type that you needs and install it via [Nuget](https://www.nuget.org/profiles/iamaashishpatel).
> To install LiteXSms, run the following command in the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)

```Powershell
PM> Install-Package LiteX.Sms.Twilio
PM> Install-Package LiteX.Sms.Plivo
PM> Install-Package LiteX.Sms.Nexmo
PM> Install-Package LiteX.Sms.Sinch
```

### Step 2 : Configuration 🔨

> Different types of sms provider have their own way to config.
> Here are samples that show you how to config.

##### 2.1 : AppSettings

```js
{
  //LiteX Twilio Sms settings
  "TwilioConfig": {
    "AccountSid": "--- REPLACE WITH YOUR Twilio SID ---",
    "AuthToken": "--- REPLACE WITH YOUR Twilio Auth Token ---",
    "FromNumber": "--- REPLACE WITH Twilio From Number ---",
    "EnableLogging": true
  },

  //LiteX Plivo Sms settings
  "PlivoConfig": {
    "AuthId": "--- REPLACE WITH YOUR Plivo Account SID ---",
    "AuthToken": "--- REPLACE WITH YOUR Plivo Auth Token ---",
    "FromNumber": "--- REPLACE WITH Plivo From Number ---",
    "EnableLogging": true
  },

  //LiteX Nexmo Sms settings
  "NexmoConfig": {
    "ApiKey": "--- REPLACE WITH YOUR Nexmo ApiKey ---",
    "ApiSecret": "--- REPLACE WITH YOUR Nexmo ApiSecret ---",
    "ApplicationId": "--- REPLACE WITH YOUR Nexmo ApplicationId ---",
    "ApplicationKey": "--- REPLACE WITH YOUR Nexmo ApplicationKey ---",
    "FromNumber": "--- REPLACE WITH Nexmo From Number ---",
    "EnableLogging": true
  },

  //LiteX Sinch Sms settings
  "SinchConfig": {
    "ApiKey": "--- REPLACE WITH YOUR Sinch ApiKey ---",
    "ApiSecret": "--- REPLACE WITH YOUR Sinch ApiSecret ---",
    "FromNumber": "--- REPLACE WITH Sinch From Number ---",
    "EnableLogging": true
  }
}
```


##### 2.2 : Configure Startup Class

```cs
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        #region LiteX Sms (Twilio)

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

        #endregion

        #region LiteX Sms (Plivo)

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

        #endregion

        #region LiteX Sms (Nexmo)

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

        #endregion

        #region LiteX Sms (Sinch)

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

        #endregion


        // add logging (optional)
        services.AddLiteXLogging();
    }
}
```


### Step 3 : Use in Controller or Business layer :memo:

```cs
/// <summary>
/// Customer controller
/// </summary>
[Route("api/[controller]")]
public class CustomerController : Controller
{
    #region Fields

    private readonly ILiteXSmsSender _smsSender;

    #endregion

    #region Ctor

    /// <summary>
    /// Ctor
    /// </summary>
    /// <param name="smsSender"></param>
    public CustomerController(ILiteXSmsSender smsSender)
    {
        _smsSender = smsSender;
    }

    #endregion

    #region Methods

    /// <summary>
    /// Get Sms Provider Type
    /// </summary>
    /// <returns></returns>
    [HttpGet]
    [Route("get-sms-provider-type")]
    public IActionResult GetSmsProviderType()
    {
        return Ok(_smsSender.SmsProviderType.ToString());
    }

    /// <summary>
    /// Send sms
    /// </summary>
    /// <param name="toPhoneNumber">To phone number</param>
    /// <param name="messageText">message text</param>
    /// <returns></returns>
    [HttpPost]
    [Route("send-sms")]
    public async Task<IActionResult> SendSms(string toPhoneNumber, string messageText)
    {
        toPhoneNumber = toPhoneNumber ?? "+919426432254";
        messageText = messageText ?? "I am LiteX Sms!";

        // async
        var result = await _smsSender.SendSmsAsync(toPhoneNumber, messageText);

        // sync
        //var result = _smsSender.SendSms(toPhoneNumber, messageText);

        return Ok(result);
    }

    #endregion
}
```



## Todo List :clipboard:

#### Sms Providers

- [x] Twilio
- [x] Plivo
- [x] Nexmo
- [x] Sinch


#### Basic Sms API

- [x] Send Sms
- [] Voice Sms
- [] Send Bulk Sms


#### Coming soon

- .NET Standard 2.1 support
- .NET 5.0 support
- Remove sync methods
- Bulk Sms





---





## Give a Star! :star:

Feel free to request an issue on github if you find bugs or request a new feature. Your valuable feedback is much appreciated to better improve this project. If you find this useful, please give it a star to show your support for this project.



## Support :telephone:

> Reach out to me at one of the following places!

- Email :envelope: at <a href="mailto:toaashishpatel@gmail.com" target="_blank">`toaashishpatel@gmail.com`</a>
- NuGet :package: at <a href="https://www.nuget.org/profiles/iamaashishpatel" target="_blank">`@iamaashishpatel`</a>



## Author :boy:

* **Ashish Patel** - [A-Patel](https://github.com/a-patel)


##### Connect with me

| Linkedin | Website | Medium | NuGet | GitHub | Microsoft | Facebook | Twitter | Instagram | Tumblr |
|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|
| [![linkedin](https://img.icons8.com/ios-filled/96/000000/linkedin.png)](https://www.linkedin.com/in/iamaashishpatel) | [![website](https://img.icons8.com/wired/96/000000/domain.png)](https://aashishpatel.netlify.app/) | [![medium](https://img.icons8.com/ios-filled/96/000000/medium-monogram.png)](https://medium.com/@iamaashishpatel) | [![nuget](https://img.icons8.com/windows/96/000000/nuget.png)](https://nuget.org/profiles/iamaashishpatel) | [![github](https://img.icons8.com/ios-glyphs/96/000000/github.png)](https://github.com/a-patel) | [![microsoft](https://img.icons8.com/ios-filled/90/000000/microsoft.png)](https://docs.microsoft.com/en-us/users/iamaashishpatel) | [![facebook](https://img.icons8.com/ios-filled/90/000000/facebook.png)](https://www.facebook.com/aashish.mrcool) | [![twitter](https://img.icons8.com/ios-filled/96/000000/twitter.png)](https://twitter.com/aashish_mrcool) | [![instagram](https://img.icons8.com/ios-filled/90/000000/instagram-new.png)](https://www.instagram.com/iamaashishpatel/) | [![tumblr](https://img.icons8.com/ios-filled/96/000000/tumblr--v1.png)](https://iamaashishpatel.tumblr.com/) |



## Donate :dollar:

If you find this project useful — or just feeling generous, consider buying me a beer or a coffee. Cheers! :beers: :coffee:

| PayPal | BMC | Patreon |
| ------------- | ------------- | ------------- |
| [![PayPal](https://www.paypalobjects.com/webstatic/en_US/btn/btn_donate_pp_142x27.png)](https://www.paypal.me/iamaashishpatel) | [![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/iamaashishpatel) | [![Patreon](https://c5.patreon.com/external/logo/become_a_patron_button.png)](https://www.patreon.com/iamaashishpatel) |



## License :lock:

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
