# Example UI of SPL `token-swap`

## Usage

Install dependencies:

```bash
$ yarn
```

Set the `SWAP_HOST_FEE_ADDRESS` in `.env` file:

```
SWAP_HOST_FEE_ADDRESS='YOUR_WALLET_ADDRESS'
```

> `solana address` should return your local wallet address

Start Solana local testnet:

```bash
$ solana-test-validator
```

Deploy the `token-swap` program. This requires you to deploy the program from the [`source`](https://github.com/solana-labs/solana-program-library/tree/master/token-swap):

Clone the `solana-program-library` repo:

```bash
$ git clone https://github.com/solana-labs/solana-program-library.git
```

Enter `token-swap` folder:

```bash
$ cd token-swap
```

Build `token-swap`:

```bash
$ cargo build-bpf
...
To deploy this program:
  $ solana program deploy /Users/YOUR_PROJECT_PATH/solana-program-library/target/deploy/spl_token_swap.so
```

Deploy to local testnet:

```bash
$ solana program deploy /Users/YOUR_PROJECT_PATH/solana-program-library/target/deploy/spl_token_swap.so
Program Id: 2Wh8iQvyKLHR1dCHsvKa9jJxnPEUfYLqC77y7NRxFBSg
```

We now get the `Program Id` from the deployment result. Next, we need to update the program ID of `token-swap` from the file `ids.tsx`:

```ts
...
  {
    name: "localnet",
    swap: () => ({
      current: {
        pubkey: new PublicKey("2Wh8iQvyKLHR1dCHsvKa9jJxnPEUfYLqC77y7NRxFBSg"),
        layout: TokenSwapLayout,
      },
      legacy: [],
    }),
  },
...
```

Run the dev server:

```bash
$ yanr run start
```

### Add Liquidity

Before adding liquidity from the UI, make sure you mint the token first and transfer to your testing account:

```bash
$ spl-token create-token
9pymQwovXDiAhWbnNdKjL4XUS9tip6hGfkrRNqrgJ4QX
```

```bash
$ spl-token create-account 9pymQwovXDiAhWbnNdKjL4XUS9tip6hGfkrRNqrgJ4QX
```

```bash
$ spl-token mint 9pymQwovXDiAhWbnNdKjL4XUS9tip6hGfkrRNqrgJ4QX 100
```

```bash
$ spl-token transfer 9pymQwovXDiAhWbnNdKjL4XUS9tip6hGfkrRNqrgJ4QX 10 YOUR_ADDRESS --fund-recipient --allow-unfunded-recipient
```

## ⚠️ Warning

Any content produced by Solana, or developer resources that Solana provides, are for educational and inspiration purposes only. Solana does not encourage, induce or sanction the deployment of any such applications in violation of applicable laws or regulations.

## Deployment

App is using to enviroment variables that can be set before deployment:

- `SWAP_HOST_FEE_ADDRESS` used to distribute fees to host of the application

To inject varibles to the app, set the SWAP_HOST_FEE_ADDRESS environment variable to the addresses of your SOL account.

You may want to put these in local environment files (e.g. .env.development.local, .env.production.local). See the documentation on environment variables for more information.

NOTE: remember to re-build your app before deploying for your referral addresses to be reflected.
