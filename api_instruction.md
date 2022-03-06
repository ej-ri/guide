# Hupayx-mainnet api instruction

### - Regular explation of accounts OR validating accounts API

|          |      Address bech32 Prefix      |  Pubkey bech32 Prefix | curve| address byte length | pubkey byte length |
|----------|:-------------:|------:|------:|------:| ------:|
| Accounts |  cosmos | cosmospub | secp256k1 | 20 | 33 |
| Validator Operator | cosmosvaloper   | cosmosvaloperpub | secp256k1 | 20 | 33 |
| Consensus Nodes | cosmosvalcons | cosmosvalconspub | ed25519 | 20 | 32 |


### - access the best height API

```
 gaiad status
```

```
{
  "node_info": {
    "protocol_version": {
      "p2p": "7",
      "block": "10",
      "app": "0"
    },
    "id": "51b548950b624ce64a0b66e8944721889dfcbe52",
    "listen_addr": "tcp://0.0.0.0:26656",
    "network": "hupayx-hub",
    "version": "0.32.8",
    "channels": "4020212223303800",
    "moniker": "hxval01",
    "other": {
      "tx_index": "on",
      "rpc_address": "tcp://0.0.0.0:26657"
    }
  },
  "sync_info": {
    "latest_block_hash": "391EDAF3B6C71D9AD46DE7E75B39F1FAC10D6CD70D356132F345280D219CF391",
    "latest_app_hash": "60AC8591C1B72FA0611316F8986A072A3C3CECB9D81574389E9174FC3E42B369",
    "latest_block_height": "11287974",
    "latest_block_time": "2022-03-06T07:25:09.971962613Z",
    "catching_up": false
  },
  "validator_info": {
    "address": "58240D8C9F06387872CB39F79CD9EB721C48EFEC",
    "pub_key": {
      "type": "tendermint/PubKeyEd25519",
      "value": "e/LaHY8cJl7/uS63chaDWRAiUl9sZ3lnAbvLy5y6EEc="
    },
    "voting_power": "2500138"
  }
}
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



