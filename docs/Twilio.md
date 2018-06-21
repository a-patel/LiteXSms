
# LiteX Twilio Sms
LiteX.Sms.Twilio is a sms library which is based on LiteX.Sms.Core and Twilio Sms API.


## Add a dependency

### Nuget

Run the nuget command for installing the client as,
* `Install-Package LiteX.Sms.Core`
* `Install-Package LiteX.Sms.Twilio`


## Configuration

**AppSettings**
```js
{
  //LiteX Twilio Sms settings
  "TwilioConfig": {
    "AccountSid": "--- REPLACE WITH YOUR Twilio SID ---",
    "AuthToken": "--- REPLACE WITH YOUR Twilio Auth Token ---",
    "FromNumber": "--- REPLACE WITH Twilio From Number ---"
  }
}
```

**Startup Configuration**
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
