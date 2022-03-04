# Hupayx-mainnet install guide

## Download files

### Download execute file

[gaiad](https://raw.githubusercontent.com/HUPAYX/guide/main/mainnet/gaiad)

[gaiacli](https://raw.githubusercontent.com/HUPAYX/guide/main/mainnet/gaiacli) 

### Download genesis file

[genesis.json](https://raw.githubusercontent.com/HUPAYX/guide/main/config/genesis.json) link or curl

```
   curl https://raw.githubusercontent.com/HUPAYX/guide/main/config/genesis.json --output <yourPath>/config/genesis.json
```

## init mainnet

```
gaiad init <node-name> --chain-id hupayx-hub --home <yourPath>
```

`--home` options you can change custom block data direrctory

### change genesis.json
```
cp genesis.json <yourPath>/config/
```

### Your blockchain in development can be configured with `config.yml`.
```
 vi <yourPath>/config/config.toml
```

line 16
```
moniker = "<node-name>"
```

line 168
```  gaiad tendermint show-node-id --home <yourPath>
seeds 51b548950b624ce64a0b66e8944721889dfcbe52@13.124.27.83:26657 
```

you can change rpc port line 77 ~ 80
```
 ##### rpc server configuration options #####
 [rpc]
 
 # TCP or UNIX socket address for the RPC server to listen on
 laddr = "tcp://127.0.0.1:26657"
```


## run gaiad

```
gaiad start --home <yourPath> --rpc.laddr tcp://0.0.0.0:26657 --trace
```

## Learn more

- [gaiad command](gaiad_command.md)
- [gaiadcli command](gaiacli_command.md)
- [Cosmos SDK docs](https://docs.cosmos.network)

