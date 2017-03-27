Social Wallet Android SDK
==================

The Social Wallet Android SDK makes it easy to add Social Wallet payments to mobile apps.
## Contents

- [Use Cases](#use-cases)
- [Integration with the Social Wallet App](#integration-with-the-social-wallet-app)
- [Requirements](#requirements)
- [Add the SDK to Your Project](#add-the-sdk-to-your-project)
- [Credentials](#credentials)
- [International Support](#international-support)
- [Documentation](#documentation)
- [Usability](#usability)
- [Next Steps](#next-steps)
- [License](#license)

## Add the SDK to Your Project

The Social Wallet Android SDK is now available at [JCenter Repository](https://bintray.com/solitondigital/com.solitondigital.mobilewallet.sdk). The latest version is available via `jcenter()`:

```groovy
compile 'com.solitondigital.mobilewallet.sdk:socialwallet-android-sdk:0.0.1'
```


## Use Cases

The SDK supports single use cases for making payments - **Single Payment**


### Single Payment

Receive a one-time payment from a customer's Social Wallet account.

1. [Accept a Single Payment](docs/single_payment.md) and receive back a proof of payment.
2. After you receive the proof of payment, merchant are recommended to verify the payment using [Social Wallet's API.](https://docs.google.com/document/d/1zg92PCq_8by1ZGDWMhFD6kAC-_Irrq88iNyCL79M_m4/edit?usp=sharing)

## Integration with the Social Wallet App

The SDK will now use the newest version of the Social Wallet App if present on the device to log in to a customer account.  No additional configuration is required to enable this feature. A user who logged in to the Social Wallet App may not need to log-in again when paying with your app.

## Requirements

* Android 4.2 (API 17) or later
* Phone or tablet

## Credentials

Your mobile integration requires different `merchant_id` values for each environment: Live and Test

Your server integrations for verifying or creating payments will also require the corresponding `merchant_password` for each `merchant_id`.

You can obtain these Social Wallet API credentials by [contacting us](#contact)

### Test Envivroment

You will be given **test credentials**, including Client ID, which will let you test your Android integration against the Social Wallet without deducting real money.

You should define test enviroment on when you setup the social wallet configuration.

### Live

Before releasing your app to public, you should define live enviroment in the social wallet configuration. This will deduct real money from social wallet.

## International Support

### Localizations

The SDK currently only support english.

### Currencies

The SDK currently supports Malaysia Ringgit only.


## Documentation

* These docs in the SDK, which include an overview of usage, step-by-step integration instructions, and sample code.
* The sample app included in this SDK.


## Usability

User interface appearance and behavior is set within the library itself. For the sake of usability and user experience consistency, apps should not attempt to modify the SDK's behavior beyond the documented methods.


## Next Steps

Depending on your use case, you can now:

* [Accept a single payment](docs/single_payment.md)

## Contact

You may reached us at sdk@solitondigital.io


## License

Please refer to this repo's [license file](LICENSE).
