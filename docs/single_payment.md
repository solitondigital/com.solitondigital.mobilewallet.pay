Single Payment
==============

Receive a single, immediate payment from your customer through Social Wallet.

_If you haven't already, see the [README](../README.md) for an initial overview and instructions for adding the SDK to your project._

Overview
--------

* The Social Wallet Android SDK...
    1. Presents UI to gather payment information from the user.
    2. Coordinates payment with Social Wallet.
    3. Returns a proof of payment to your app.
* Your code...
    1. Receives proof of payment from the Social Wallet Android SDK.
    2. [Sends proof of payment to your servers for verification](https://docs.google.com/document/d/1zg92PCq_8by1ZGDWMhFD6kAC-_Irrq88iNyCL79M_m4/edit?usp=sharing).
    3. Provides the user their goods or services.

Sample Code
-----------

The sample app provides a more complete example. However, at minimum, you must:

1. Add Social Wallet Android SDK dependency to your `build.gradle` file as shown in README.md

1. Create a `SocialWalletConfiguration` object
    ```java
    private static SocialWalletConfiguration config = new SocialWalletConfiguration()

            // Start with mock environment.  When ready, switch to sandbox (ENVIRONMENT_SANDBOX)
            // or live (ENVIRONMENT_PRODUCTION)
            .environment(SocialWalletConfiguration.ENVIRONMENT_NO_NETWORK)

            .clientId("<YOUR_CLIENT_ID>");
    ```

2. Start `SocialWalletService` when your activity is created and stop it upon destruction:

    ```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Intent intent = new Intent(this, SocialWalletService.class);

        intent.putExtra(SocialWalletService.EXTRA_SOCIALWALLET_CONFIGURATION, config);

        startService(intent);
    }

    @Override
    public void onDestroy() {
        stopService(new Intent(this, SocialWalletService.class));
        super.onDestroy();
    }
    ```

3. Create the payment and launch the payment intent, for example, when a button is pressed:

    ```java
    public void onBuyPressed(View pressed) {

        // PAYMENT_INTENT_SALE will cause the payment to complete immediately.
        // Change PAYMENT_INTENT_SALE to 
        //   - PAYMENT_INTENT_AUTHORIZE to only authorize payment and capture funds later.
        //   - PAYMENT_INTENT_ORDER to create a payment for authorization and capture
        //     later via calls from your server.

        SocialWalletPayment payment = new SocialWalletPayment(new BigDecimal("1.75"), "MYR", "sample item",
                SocialWalletPayment.PAYMENT_INTENT_SALE);

        Intent intent = new Intent(this, PaymentActivity.class);

        // send the same configuration for restart resiliency
        intent.putExtra(SocialWalletService.EXTRA_SOCIALWALLET_CONFIGURATION, config);

        intent.putExtra(PaymentActivity.EXTRA_PAYMENT, payment);

        startActivityForResult(intent, 0);
    }
    ```

4. Implement `onActivityResult()`:

    ```java
    @Override
    protected void onActivityResult (int requestCode, int resultCode, Intent data) {
        if (resultCode == Activity.RESULT_OK) {
            PaymentConfirmation confirm = data.getParcelableExtra(PaymentActivity.EXTRA_RESULT_CONFIRMATION);
            if (confirm != null) {
                try {
                    Log.i("paymentExample", confirm.toJSONObject().toString(4));

                    // TODO: send 'confirm' to your server for verification.
                    // see https://docs.google.com/document/d/1zg92PCq_8by1ZGDWMhFD6kAC-_Irrq88iNyCL79M_m4/edit?usp=sharing
                    // for more details.

                } catch (JSONException e) {
                    Log.e("paymentExample", "an extremely unlikely failure occurred: ", e);
                }
            }
        }
        else if (resultCode == Activity.RESULT_CANCELED) {
            Log.i("paymentExample", "The user canceled.");
        }
        else if (resultCode == PaymentActivity.RESULT_EXTRAS_INVALID) {
            Log.i("paymentExample", "An invalid Payment or SocialWalletConfiguration was submitted. Please see the docs.");
        }
    }
    ```

5. [Send the proof of payment to your servers for verification](https://docs.google.com/document/d/1zg92PCq_8by1ZGDWMhFD6kAC-_Irrq88iNyCL79M_m4/edit?usp=sharing),
   as well as any other processing required for your business, such as fulfillment.

   **Tip:** At this point, the payment has been completed, and the user
   has been charged. If you can't reach your server, it is important that you save the proof
   of payment and try again later.

### Hint

Mobile networks are unreliable. Save the proof of payment to make sure it eventually reaches your server.

Next Steps
----------

**Avoid fraud!** Be sure to [verify the proof of payment](https://docs.google.com/document/d/1zg92PCq_8by1ZGDWMhFD6kAC-_Irrq88iNyCL79M_m4/edit?usp=sharing).
