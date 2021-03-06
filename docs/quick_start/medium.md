# Intermediate: Use NEAR in an existing app

If you have an app with an existing front-end that you want to hook into the smart contract on the back end, you will need to import our JavaScript SDK on the front-end and write/deploy the smart contract on the back end.

## 1. Import the SDK on your front end

```text
<script src="https://cdn.jsdelivr.net/npm/nearlib@0.2.4/dist/nearlib.js"></script>
```

## 2. Write the smart contract

Write the code!

## 3. Deploy the smart contract

### Option A: Deploy to your local DevNet

You will need to build and run a local DevNet node. See the following section for how to do this.

Once you have done this, make sure you are within the application's directory and run:

```text
npm install
npm run build
npm run-script deploy -- --contract guestbook
```

### Option B: Deploy to our hosted DevNet

Deploy your contract to the same DevNet which the NEAR Studio IDE deploys to.

Download near cli tools

```text
npm install -g near-shell
```

Navigate to your source directory in command line, and do the following

1. Create an account for your contract

```bash
near create_account --node_url https://studio.nearprotocol.com/devnet --account_id <yourcontractname>
```

1. Build your contract

```bash
near build
```

1. Deploy your contract to DevNet

```bash
near deploy --node_url https://studio.nearprotocol.com/devnet --contract_name <yourcontractname>
```

For help using cli tools, you can use `near help`

