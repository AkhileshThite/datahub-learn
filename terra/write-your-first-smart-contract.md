# Introduction

At some point, while building on the Terra blockchain, you will want to submit transactions in order to unlock the full power of Terra.

In this tutorial, we will learn how to submit transactions using a [**DataHub**](https://figment.io/datahub-waitlist/) ****Terra node. We will submit two transactions:

* Regular transfer of LUNA tokens to another account
* Swap transactions which will exchange LUNA to UUSD

# Prerequisites

Please make sure that you completed tutorials \#1 \("Connecting to a Terra node with DataHub"\), \#2 \("Creating your first Terra account with the Terra SDK"\), and \#3 \("Querying the Terra blockchain"\) before moving forward. We will be building on top of the Nodejs application created in these tutorials.

# Sending tokens

In the previous tutorials, we created our account and we used the testnet faucet to request test tokens. Now that we have some tokens to spend, let’s send them to another account.

Start by creating a new file `transfer.js` in the root project directory and add the code below:

```javascript
const { LCDClient, MnemonicKey, MsgSend, isTxError } = require('@terra-money/terra.js');
require('dotenv').config();

const main = async () => {
  const terra = new LCDClient({
    URL: process.env.TERRA_NODE_URL,
    chainID: process.env.TERRA_CHAIN_ID,
  });

  // Use key created in tutorial #2
  const mk = new MnemonicKey({
    mnemonic: process.env.MNEMONIC,
  });

  // Create a wallet out of you mnemonic key
  const wallet = terra.wallet(mk);

  const toAddress = 'terra1uwqg9vvg82sw29xuun777547jg8tnfrdh673fl';

  // Create a message
  const msg = new MsgSend(
    wallet.key.accAddress,
    toAddress,
    { uluna: 10 }
  );

  // Create and sign transaction
  const tx = await wallet.createAndSignTx({
    msgs: [msg],
    memo: "Hello from Figment Learn"
  });

  const txHash = await terra.tx.hash(tx);
  console.log('txHash: ', txHash);

  // Broadcast transaction
  const txResult = await terra.tx.broadcast(tx);

  if (isTxError(txResult)) {
    throw new Error(`encountered an error while running the transaction: ${txResult.code} ${txResult.codespace}`);
  }

  // Check for events from the first message
  console.log('logs: ', txResult.logs);
}

main().then(resp => {
  console.log(resp);
}).catch(err => {
  console.log(err)
})
```

Let's break this down. At the top, as usual, we import `terra.js` and `dotenv`. Then in the main function body, we connect to the DataHub Terra node and load our account stored in the `.env` file mnemonic.

The next step is to create a wallet using our mnemonic key:

```javascript
const wallet = terra.wallet(mk);
```

Once our wallet is created, we can build a message that will be included in our transaction. In this case, we build `MsgSend` where we specify the origin address, the destination address, and how much LUNAs we want to send:

```javascript
const msg = new MsgSend(
  wallet.key.accAddress,
  toAddress,
  { uluna: 10 }
);
```

Now it’s time to create and sign our first transaction using our wallet by writing:

```javascript
const tx = await wallet.createAndSignTx({
  msgs: [msg],
  memo: "Hello from Figment Learn"
});
```

Here you can notice that the `msgs` field is an array meaning that we can add multiple messages to our transaction.

Our transaction is ready to be sent to Terra. Broadcasting the transaction means that it will be sent to the node but we will not receive a response immediately. It will take some time for the validators to validate our transaction and add it to the block.

```javascript
const txResult = await terra.tx.broadcast(tx);
```

This is it! Congratulations, you’ve just submitted your first transaction to the Terra Tequila testnet using a DataHub node.

Now it’s time to see if our transaction has succeeded. Head back to your Stake ID account view and refresh the page. Now you should see that your balance is not `1,000` LUNAs anymore.

## Swapping LUNAs

Now that we’ve seen how to send tokens to a different account, let’s examine how we can exchange our LUNAs for a different denomination. In tutorial \#3, we issued a query to get exchange rates for different denominations. We would like to get the exchange rate for `uusd` , so let’s swap `1,000` LUNAs to UUSD.

Create a new file `swap.js` in the root project directory and in add the snippet below:

```javascript
const { LCDClient, MnemonicKey, MsgSwap, isTxError, Coin } = require('@terra-money/terra.js');
require('dotenv').config();

const main = async () => {
  const terra = new LCDClient({
    URL: process.env.TERRA_NODE_URL,
    chainID: process.env.TERRA_CHAIN_ID,
  });

  // Use key created in tutorial #2
  const mk = new MnemonicKey({
    mnemonic: process.env.MNEMONIC,
  });

  // Create a wallet out of you mnemonic key
  const wallet = terra.wallet(mk);

  // Create a message
  const msg = new MsgSwap(
    wallet.key.accAddress,
    new Coin('uluna', '1000'),
    'uusd'
  );

  // Create and sign transaction
  const tx = await wallet.createAndSignTx({
    msgs: [msg],
    memo: "Hello from Figment Learn"
  });

  // Broadcast transaction
  const txResult = await terra.tx.broadcast(tx);

  // Get transaction hash
  const txHash = await terra.tx.hash(tx);
  console.log('txHash: ', txHash);

  if (isTxError(txResult)) {
    throw new Error(`encountered an error while running the transaction: ${txResult.code} ${txResult.codespace}`);
  }

  // Check for events from the first message
  console.log('logs: ', txResult.logs);
}

main().then(resp => {
  console.log(resp);
}).catch(err => {
  console.log(err)
})
```

You can quickly notice that the bulk of the code in this file is the same as in the `send.js` file. The difference is the message that is attached to the transaction. Here we create `MsgSwap` instead of `MsgSend`:

```javascript
const msg = new MsgSwap(
  wallet.key.accAddress,
  new Coin('uluna', '1000'),
  'uusd'
);
```

This is a swap message which will use our wallet account to exchange `1,000` LUNAs to UUSD. Run the `swap.js` script and note the transaction hash from the output. Head to Stake ID, refresh your account view, and confirm that transaction has been successful.

The complete code for this tutorial can be found [**here**](https://github.com/figment-networks/tutorials/tree/main/terra/4_transactions). 

# Conclusion

Great job! Now you not only know how to read from the Terra blockchain, but also how to interact with it by submitting transactions with [**DataHub**](https://figment.io/datahub-waitlist/). 

# Next Steps

Terra.js has a lot more to offer. We just scratched the surface of what this package can do. In order to learn more about it, please visit: [**Terra.js**](https://terra-project.github.io/terra.js/)

If you had any difficulties following this tutorial or simply want to discuss Terra tech with us you can [join our community today](https://discord.gg/fszyM7K)!

