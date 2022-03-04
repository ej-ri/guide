# Hupayx-mainnet command list by gaiacli

- key recover
```
gaiacli keys add [KEYNAME] --recover
```
- key list
```
gaiacli keys list
```
- key remove

```
gaiacli keys delete [KEYNAME]
```

- check account balance 

```
gaiacli query account [ACCOUNT-ADDR] --chain-id [CHAIN-ID] --node [NODE]
```

- send transaction

```
gaiacli tx send  [TO-ADDR] [AMOUNT] --fees [FEES] --from [FROM-ADDR]
```

- check rewards
```
gaiacli query distribution rewards <delegatorAddress>
```

- withdraw rewards
```
gaiacli tx distribution  withdraw-all-rewards --from <delegatorAddress>
```
 
## Learn more

- [gaia docs](https://hub.cosmos.network/main/resources/gaiad.html)
- [gaia github](https://github.com/cosmos/gaia/tree/v2.0.4)


