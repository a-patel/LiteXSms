# LiteXSms
Abstract interface to implement any kind of basic sms message services (e.g. Twilio, Plivo, Sinch, Nexmo)

## Add a dependency

### Nuget

Run the nuget command for installing the client as,
* `Install-Package LiteX.Sms.Core`
* `Install-Package LiteX.Sms.Twilio`
* `Install-Package LiteX.Sms.Plivo` //COMING SOON
* `Install-Package LiteX.Sms.Sinch` //COMING SOON
* `Install-Package LiteX.Sms.Nexmo` //COMING SOON


## Configuration

**AppSettings**
```js
{
  //LiteX Twilio settings
  "TwilioConfig": {
    "AccountSid": "--- REPLACE WITH YOUR AccountSid ---",
    "AuthToken": "--- REPLACE WITH YOUR AuthToken ---",
    "FromNumber": "--- REPLACE WITH YOUR FromNumber ---",
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
        var twilioConfig = new TwilioConfig();
        services.AddLiteXTwilioSms(twilioConfig);

        #endregion

        #endregion
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {

    }
}
```


## Usage

**Controller or Business layer**
```cs
/// <summary>
/// Customer controller
/// </summary>
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
    /// Send email to customer
    /// </summary>
    /// <param name="customer"></param>
    /// <returns></returns>
    public IActionResult SendSmsToCustomer(Customer customer)
    {
        try
        {
            string message = "test message!",
            toPhoneNumber = "+11234567890",

            _smsSender.SendSms(toPhoneNumber, message);
        }
        catch (Exception ex)
        {

            return BadRequest(ex);
        }
        return Ok();
    }

    #endregion

    #region Utilities

    private IList<Customer> GetCustomers()
    {
        IList<Customer> customers = new List<Customer>();

        customers.Add(new Customer() { Id = 1, Username = "ashish", Sms = "toaashishpatel@outlook.com" });

        return customers;
    }

    private Customer GetCustomerById(int id)
    {
        Customer customer = null;

        customer = GetCustomers().ToList().FirstOrDefault(x => x.Id == id);

        return customer;
    }

    #endregion
}
```
