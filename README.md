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

Receive a one-time payment from a customer's Social Wallet account. This can be either (1) an **immediate** payment which your servers should subsequently **verify**, or (2) an **authorization** for a payment which your servers must subsequently **capture**, or (3) a payment for an **order** which your servers must subsequently **authorize** and **capture**:

1. [Accept a Single Payment](docs/single_payment.md) and receive back a proof of payment.
2. On your server, [Verify the Payment](https://docs.google.com/document/d/1zg92PCq_8by1ZGDWMhFD6kAC-_Irrq88iNyCL79M_m4/edit?usp=sharing), [Capture the Payment](https://docs.google.com/document/d/1zg92PCq_8by1ZGDWMhFD6kAC-_Irrq88iNyCL79M_m4/edit?usp=sharing), or [Process the Order](https://docs.google.com/document/d/1zg92PCq_8by1ZGDWMhFD6kAC-_Irrq88iNyCL79M_m4/edit?usp=sharing) (Social Wallet Developer site) using Social Wallet's API.

## Integration with the Social Wallet App

The SDK will now use the newest version of the Social Wallet App if present on the device to log in to a customer account.  No additional configuration is required to enable this feature. A user who logged in to the Social Wallet App may not need to log-in again when paying with your app.

### Limitations

* The integration will _not_ be enabled in any of the [testing](#testing) modes, as the Wallet app does not support this developer testing environment.

## Requirements

* Android 4.2 (API 17) or later
* Phone or tablet

## Credentials

Your mobile integration requires different `client_id` values for each environment: Live and Test (Sandbox).

Your server integrations for verifying or creating payments will also require the corresponding `client_secret` for each `client_id`.

You can obtain these Social Wallet API credentials by [contacting us](#contact)

### Sandbox

Once logged in on this Applications page, you will be assigned **test credentials**, including Client ID, which will let you test your Android integration against the Social Wallet Sandbox.

While testing your app, when logging in to Social Wallet in the SDK's UI you should use a *personal* Sandbox account email and password. I.e., not your Sandbox *business* credentials.

You can create both business and personal Sandbox accounts by [contacting us](#contact)

### Live

To obtain your **live** credentials, you will need to have a business account. If you don't yet have a business account, [please email us](#contact)


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
