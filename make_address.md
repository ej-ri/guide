# Create Hupayx Wallet address

## Using cosmosjs

#### NodeJS
```
npm install @cosmostation/cosmosjs

const cosmosjs = require("@cosmostation/cosmosjs");
```
#### Browser
```
<script src='js/cosmosjs-bundle.js'></script>
```

### Generate Hupayx address 

#### using javascript

- cosmosjs
```
const cosmosjs = require("@cosmostation/cosmosjs");

const lcdUrl  = "lcd.hupay.io"
const chainId = "hupayx-hub";
const cosmos = cosmosjs.network(lcdUrl, chainId);

const mnemonic = "..."
cosmos.setPath("m/44'/118'/0'/0/0");
const address = cosmos.getAddress(mnemonic);
const ecpairPriv = cosmos.getECPairPriv(mnemonic);
```

- purejs
```
const bip39 = require('bip39');
const bip32 = require('bip32');
const bech32 = require('bech32');
const bitcoin = require('bitcoinjs-lib');

const path_hpx = "m/44'/118'/0'/0/0";
const seed = bip39.mnemonicToSeed(mnemonic, password);
const node = bip32.fromSeed(seed);
const bech32MainPrefix = "cosmos";

const child = node.derivePath(path_hpx);
const words = bech32.toWords(child.identifier);
const walletAddress = bech32.encode(bech32MainPrefix, words);  
return walletAddress;
```

#### using gaiacli

- create new account
```
gaiad keys add my-account
```

- recover mnemonic
```
gaiacli keys add [KEYNAME] --recover
```

- show list all account
```
gaiad keys list
```


