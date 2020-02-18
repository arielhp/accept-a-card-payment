# Accepting a card payment

**Demo**

Web: See a [hosted version](https://hhqhp.sse.codesandbox.io/)

All the samples run in test mode -- use the below test card numbers with any CVC code + a future expiration date to test for certain behavior.

<!-- prettier-ignore -->
| Test card number     | Using webhooks | Without webhooks | Declining on card authentication |
:--- | :--- | :--- | :---
**4242424242424242** | Succeeds  | Succeeds  | Succeeds |
**4000000000003220** | Displays a pop-up modal to authenticate  | Displays a pop-up modal to authenticate  | Declines and asks customer for new card |

<img src="./web-elements-card-payment.gif" alt="Accepting a card payment" align="center">


## How to run locally

Follow the steps below to run locally.

**1. Clone and configure**

You can manually clone and configure:

```
git clone https://github.com/arielhp/accept-a-card-payment
```

Copy the .env.example file into a file named .env in the folder of the server you want to use. For example:

```
cp .env.example using-webhooks/server/node/.env
```

You will need a Stripe account. Once you set up your account, go to the Stripe [developer dashboard](https://stripe.com/docs/development#api-keys) to find your API keys.

```
STRIPE_PUBLISHABLE_KEY=<replace-with-your-publishable-key>
STRIPE_SECRET_KEY=<replace-with-your-secret-key>
```

`STATIC_DIR` tells the server where to the client files are located and does not need to be modified unless you move the server files.

**2. Follow the server instructions on how to run:**

Run the Node server in `using-webhooks`:

```
cd using-webhooks/server/node # there's a README in this folder with instructions
npm install
npm start
```

**3. Run a webhook locally:**

If you want to test the `using-webhooks` integration with a local webhook on your machine, you can use the Stripe CLI to easily spin one up.

First [install the CLI](https://stripe.com/docs/stripe-cli) and [link your Stripe account](https://stripe.com/docs/stripe-cli#link-account).

```
stripe listen --forward-to localhost:4242/webhook
```

The CLI will print a webhook secret key to the console. Set `STRIPE_WEBHOOK_SECRET` to this value in your .env file.

You should see events logged in the console where the CLI is running.
