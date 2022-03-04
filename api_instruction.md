# Hupayx-mainnet api instruction

### - Regular explation of accounts OR validating accounts API

```
gaiacli 
```

### - access the best height API

```
 gaiacli q block 2 --chain-id hupayx-hub
```


### - access the account history API

```
gaiacli query txs --tags='message.sender:[addr]' --page 1 --limit 30
{"total_count":"0","count":"0","page_number":"1","page_total":"0","limit":"30","txs":[]}
```


### - access the detailed informations of a trade

* TODO 

### - how to determine a trade is accurate to avoid cheating recharge（please describe it）

* TODO 

### - Tranfer process: sign transcation offline and broadcast it online

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

### - access the balance of an account
```
gaiacli query bank balances [address]
```
 

