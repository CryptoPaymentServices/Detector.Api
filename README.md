# Crypto-Payment.Services Detector.API
This API allows to campaigns/addresses for which cash-in's/cash-out's must be detected and notifications send to your url or slack.

API (MainNet): https://crypto-payment.services/detector/swagger/index.html
API (TestNet): https://test.crypto-payment.services/detector/swagger/index.html

## How to use API
You can use API directly from your applications or you can call it directly from swagger.

## API Access Key
In order to use the system you need an API access key. Getting a key is free and easy, sign up here: https://test.crypto-payment.services (TestNet networks)

## Important
The payment detection will be started for your addresses only when you have positive balance for your user. You can find out how to add funds to your balance here: https://github.com/CryptoPaymentServices/User.Api

## How to add addresses
- Create campaign using `POST /api/campaigns`. The `active` property can be set to true only when `notifyUrlActive = true` or `notifySlackActive = true`
- Add addresses using POST `/api/campaigns/{campaignId}/addresses`

## How to setup url that can receive payment notifications
- The url must be able to recieve http POST requests and read message from request body.
- Please review details about structure of notification message in swagger in `PaymentNotification` model
- You can send test payment notification message to your url using `POST /test/url`

### c# example

```c#
public async Task<IActionResult> PostPayment([FromBody] PaymentRequest request)
{
  if (request.SecretKey != _secretKey)
  {
    return BadRequest("Invalid secret key");
  }
  
  var exists = await _paymentRepo.Exists(f => f.Id == request.Id);
  if (exists)
  {
    // return 200 status code if the payment was already processed
    return Ok();
  }

  // process payment here
  //...
  // end payment processing
  
  //save payment id
  await _paymentRepo.Save(request.Id);

  return Ok();
}
```

## How to get slack webhook url
- Sign in to the Slack desktop or web app.
- Select your <team name> drop-down menu. If you do not have a team set up, you will need to create one.
- Click Apps & integrations.
- Once redirected, type incoming webhooks in the "Search" field and click Incoming WebHooks from the search results.
- On the next page, click Add Configuration.
- In the "Post to Channel" section, select an existing Slack channel from the drop-down menu, or click create a new channel to make a new one. Once your channel is selected, click Add Incoming WebHooks integration.
- On the next page, a confirmation message, "New integration added!" is displayed in the top navigation.
- Locate the "Webhook URL" section, then highlight and copy the entire Webhook URL.
