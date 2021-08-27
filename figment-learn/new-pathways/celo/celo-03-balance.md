Now we have our account created, but wouldn’t it be nice to keep track of cUSD and CELO balances. In this step, we will examine how we can do just that.

{% hint style="info" %}
The Celo blockchain has two native assets, **CELO** (CELO) and the **Celo Dollar** (cUSD). Both of these assets implement the `ERC20` token standard from Ethereum. The CELO asset is managed by the CELO smart contract and Celo Dollars is managed by the cUSD contract. 
{% endhint %}

------------------------

# Challenge

{% hint style="tip" %}
In `pages/api/celo/balance.ts`, complete the code of the **balance** function.
{% endhint %}

**Take a few minutes to figure this out**

```typescript
//...
  try {
    const { address } = req.body
    const url = getSafeUrl();
    const kit = newKit(url);

    const goldtoken = undefined;
    const celoBalance = undefined;
    
    const stabletoken = undefined;
    const cUSDBalance = undefined;


    res.status(200).json({ 
        attoCELO: celoBalance.toString(), 
        attoUSD: cUSDBalance.toString() 
    })
  }
//...
```

**Need some help?** Check out these links
* [**We can access the CELO contract via the SDK with kit.contracts.getGoldToken()**](https://github.com/enigmampc/SecretJS-Templates/blob/master/3_query_node/query.js)
* [**We can access the cUSD contract with kit.contracts.getStableToken()**](https://github.com/enigmampc/SecretJS-Templates/blob/master/3_query_node/query.js)
* [**code example**](https://docs.celo.org/developer-guide/start/hellocelo#reading-alfajores)

{% hint style="info" %}
[**You can join us on Discord, if you have questions**](https://discord.gg/fszyM7K)
{% endhint %}

Still not sure how to do this? No problem! The solution is below so you don't get stuck.

------------------------

# Solution

```typescript
//...
  try {
    const { address } = req.body
    const url = getSafeUrl();
    const kit = newKit(url);

    const goldtoken = await kit.contracts.getGoldToken();
    const celoBalance = await goldtoken.balanceOf(address);

    const stabletoken = await kit.contracts.getStableToken();
    const cUSDBalance = await stabletoken.balanceOf(address);

    res.status(200).json({ 
        attoCELO: celoBalance.toString(), 
        attoUSD: cUSDBalance.toString() 
    })
  }
//...
```

**What happened in the code above?**
* First, we create a new `kit` instance.
* Next, we call `getGoldToken` method of `contracts` module to access CELO contract, then providing the input address to `balanceOf` return the balance of **CELO** token.
* Next, we call `getStableToken` method of `contracts` module to access CELO contract, then providing the input address to `balanceOf` return the balance of **cUSD** token.

{% hint style="tip" %}
The amount returned by is denominated in **aCELO** and **acUSD**, so to convert it to **CELO** and **acUSD** you'll need to divide it by 10**18 (a stand for `atto`)
{% endhint %}

------------------------

# Make sure it works

Once the code is complete and the file is saved, Next.js will rebuild the API route. Click on **Check Balance** and you should see the balance displayed on the page:

![](../../../.gitbook/assets/pathways/celo/celo-balance.png)

-----------------------------

# Next

Querying the balance information is fun, but being able to submit transactions and change the state of a blockchain is even better. In our next step, we will dive deeper and submit our first transactions on Celo.
