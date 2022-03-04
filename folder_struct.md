# Hupayx mainnet directory structure

```
<yourPath>
    ├── config
    │   ├── addrbook.json
    │   ├── app.toml             # Application-related configuration file.
    │   ├── config.toml          # Tendermint-related configuration file.
    │   └── genesis.json
    ├── data                     # Contains the databases used by the node
    │   ├── application.db
    │   ├── blockstore.db
    │   ├── cs.wal
    │   ├── evidence.db
    │   ├── state.db
    │   └── tx_index.db
    └── keys
        ├── accounts.txt
        └── keys.db 
```

### genesis.json

A genesis file is a JSON file which defines the initial state of your blockchain. It can be seen as height 0 of your blockchain. The first block, at height 1, will reference the genesis file as its parent.

The state defined in the genesis file contains all the necessary information, like initial token allocation, genesis time, default parameters, and more. Let us break down these information.

The genesis_time is defined at the top of the genesis file. It is a UTC timestamps which specifies when the blockchain is due to start. At this time, genesis validators are supposed to come online and start participating in the consensus process. The blockchain starts when more than 2/3rd of the genesis validators (weighted by voting power) are online.