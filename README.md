# Crypto-Payment.Services Detector.API
This API allows to campaigns/addresses for which cash-in's/cash-out's must be detected and notifications send to your url or slack.

API (TestNet): https://test.crypto-payment.services/detector/swagger/index.html

## How to use API
You can use API directly from your applications or you can call it directly from swagger.

## API Access Key
In order to use the system you need an API access key. Getting a key is free and easy, sign up here: https://test.crypto-payment.services (TestNet networks)

## How to add addresses
- Create campaign using `POST /api/campaigns`. The `active` property can be set to true only when `notifyUrlActive = true` or `notifySlackActive = true`
- Add addresses to monitor using POST `/api/campaigns/{campaignId}/addresses`

## Important
The payment detection will be started for your addresses only when you have positive balance for your user. You can find out how to add funds to your balance here: https://github.com/CryptoPaymentServices/User.Api
