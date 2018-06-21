# LiteX Plivo Sms
LiteX.Sms.Plivo is a sms library which is based on LiteX.Sms.Core and Plivo Sms API.

## Add a dependency

### Nuget

Run the nuget command for installing the client as,
* `Install-Package LiteX.Sms.Core`
* `Install-Package LiteX.Sms.Plivo`


## Configuration

**AppSettings**
```js
{
  //LiteX Plivo Sms settings
  "PlivoConfig": {
    "AuthId": "--- REPLACE WITH YOUR Plivo Account SID ---",
    "AuthToken": "--- REPLACE WITH YOUR Plivo Auth Token ---",
    "FromNumber": "--- REPLACE WITH Plivo From Number ---"
  }
}
```

**Startup Configuration**
```cs
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
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

