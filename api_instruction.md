# Hupayx-mainnet api instruction

### - Regular explation of accounts OR validating accounts API

|          |      Address bech32 Prefix      |  Pubkey bech32 Prefix | curve| address byte length | pubkey byte length |
|----------|:-------------:|------:|------:|------:| ------:|
| Accounts |  cosmos | cosmospub | secp256k1 | 20 | 33 |
| Validator Operator | cosmosvaloper   | cosmosvaloperpub | secp256k1 | 20 | 33 |
| Consensus Nodes | cosmosvalcons | cosmosvalconspub | ed25519 | 20 | 32 |


### - access the best height API

```
 gaiacli q block 2 --chain-id hupayx-hub
```


### - access the account history API
- using commend
```
gaiacli query txs --tags='message.sender:[addr]' --page 1 --limit 30
{"total_count":"0","count":"0","page_number":"1","page_total":"0","limit":"30","txs":[]}
```
 
- using cosmosjs
```
let page = 1;
let limit = 30;

let txs = await cosmos.searchTxs (page, limit, address);
```


### - access the detailed informations of a trade

* TODO 

### - how to determine a trade is accurate to avoid cheating recharge（please describe it）

* TODO 

### - Tranfer process: sign transcation offline and broadcast it online
- using commend
```
## step 1 generate unsignedTx
gaiacli tx bank send [from_key_or_address] [to_address] [amount] [flags] \
  --chain-id=<chain_id> \
  --generate-only > unsignedSendTx.json

## step 2 generate signedTx file
gaiacli tx sign unsignedTx.json --from <delegatorKeyName> --offline --chain-id <chain_id> --sequence <sequence> --account-number <account-number> > signedTx.json

## step 3 broadcast
gaiacli tx broadcast signedTx.json
```

- using cosmosjs
```
## step 1 generate unsignedTx
let stdSignMsg = cosmos.NewStdMsg({
       type: 'cosmos-sdk/MsgSend',
       from_address: from_addr,
       to_address: to_addr,
       amountDenom,
       amount: web3.toWei(amount, 'mwei'),
       feeDenom: 'uhpx',
       fee: tx_fee,
       gas: gas_fee,
       memo: '',
       account_number: data.result.value.account_number,
       sequence: data.result.value.sequence
});

## step 2 generate signedTx
let signedTx = cosmos.sign(stdSignMsg, ecpairPriv, 'sync');

## step 3 broadcast
let tx = await cosmos.broadcast(JSON.parse(signedTx));
```


### - access the balance of an account
- using commend
```
gaiacli query bank balances [address]
```
 
 - using cosmosjs
```
  let balance = null;
  try {
    balance = await cosmos.getBalance(address);
  } catch (err) {
    log(err)
    throw err;
  }
  if (balance.error) {
    return balance;
  }
  let symbol = 'hpx';
  if (balance.result.length > 0) {
    balance.result = _.filter(balance.result, data => {
      return data.denom.substr(1) === symbol;
    });
    if (balance.result.length > 0) {
      balance.result = _.map(balance.result, data => {
        return { symbol: data.denom.substr(1), uamount: data.amount, amount: web3.fromWei(data.amount, 'mwei') };
      });
      return balance.result[0].amount;
    } else {
      return '0';
    }
  } else {
    return '0';
  }
  ```

## Learn more
- [cosmosjs](https://github.com/OWDIN/cosmosjs)



