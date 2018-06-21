# LiteXSms
Abstract interface to implement any kind of basic sms message services (e.g. Twilio, Plivo, Sinch, Nexmo)

## Add a dependency

### Nuget

Run the nuget command for installing the client as,
* `Install-Package LiteX.Sms.Core`
* `Install-Package LiteX.Sms.Twilio`
* `Install-Package LiteX.Sms.Plivo`
* `Install-Package LiteX.Sms.Sinch`
* `Install-Package LiteX.Sms.Nexmo`


## Configuration

**AppSettings**
```js
{
  //LiteX Twilio Sms settings
  "TwilioConfig": {
    "AccountSid": "--- REPLACE WITH YOUR Twilio SID ---",
    "AuthToken": "--- REPLACE WITH YOUR Twilio Auth Token ---",
    "FromNumber": "--- REPLACE WITH Twilio From Number ---"
  },

  //LiteX Plivo Sms settings
  "PlivoConfig": {
    "AuthId": "--- REPLACE WITH YOUR Plivo Account SID ---",
    "AuthToken": "--- REPLACE WITH YOUR Plivo Auth Token ---",
    "FromNumber": "--- REPLACE WITH Plivo From Number ---"
  },

  //LiteX Nexmo Sms settings
  "NexmoConfig": {
    "ApiKey": "--- REPLACE WITH YOUR Nexmo ApiKey ---",
    "ApiSecret": "--- REPLACE WITH YOUR Nexmo ApiSecret ---",
    "ApplicationId": "--- REPLACE WITH YOUR Nexmo ApplicationId ---",
    "ApplicationKey": "--- REPLACE WITH YOUR Nexmo ApplicationKey ---",
    "FromNumber": "--- REPLACE WITH Nexmo From Number ---"
  },

  //LiteX Sinch Sms settings
  "SinchConfig": {
    "ApiKey": "--- REPLACE WITH YOUR Sinch ApiKey ---",
    "ApiSecret": "--- REPLACE WITH YOUR Sinch ApiSecret ---",
    "FromNumber": "--- REPLACE WITH Sinch From Number ---"
  }
}
```

**Startup Configuration**
```cs
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        #region LiteX Sms

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
        });

        //OR
        // 3. Load configuration settings on your own.
        // (e.g. appsettings, database, hardcoded)
        var twilioConfig = new TwilioConfig()
        {
            AccountSid = "",
            AuthToken = "",
            FromNumber = ""
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
        });

        //OR
        // 3. Load configuration settings on your own.
        // (e.g. appsettings, database, hardcoded)
        var plivoConfig = new PlivoConfig()
        {
            AuthId = "",
            AuthToken = "",
            FromNumber = ""
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
            FromNumber = ""
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
        });

        //OR
        // 3. Load configuration settings on your own.
        // (e.g. appsettings, database, hardcoded)
        var sinchConfig = new SinchConfig()
        {
            ApiKey = "",
            ApiSecret = "",
            FromNumber = ""
        };
        services.AddLiteXSinchSms(sinchConfig);

        #endregion

        #endregion
    }
}
```


## Usage

**Controller or Business layer**
```cs
/// <summary>
/// Customer controller
/// </summary>
[Route("api/[controller]")]
public class CustomerController : Controller
{
    #region Fields

    private readonly ISmsSender _smsSender;

    #endregion

    #region Ctor

    /// <summary>
    /// Ctor
    /// </summary>
    /// <param name="smsSender"></param>
    public CustomerController(ISmsSender smsSender)
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
    /// Send email to customer
    /// </summary>
    /// <param name="toPhoneNumber">To phone number</param>
    /// <param name="messageText">message text</param>
    /// <returns></returns>
    [HttpPost]
    [Route("send-sms-to-customer")]
    public IActionResult SendSmsToCustomer(string toPhoneNumber, string messageText)
    {
        try
        {
            toPhoneNumber = toPhoneNumber ?? "+919426432254";
            messageText = messageText ?? "I am LiteX Sms!";

            _smsSender.SendSms(toPhoneNumber, messageText);

            // Async
            //await _smsSender.SendSmsAsync(toPhoneNumber, messageText);

            return Ok();
        }
        catch (Exception ex)
        {
            return BadRequest(ex);
        }
    }

    #endregion
}
```


### Coming soon...
* Voice Sms
* Bulk Sms
