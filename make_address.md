# Hupayx Wallet address

## Using cosmosjs

### import

#### NodeJS
```
npm install @cosmostation/cosmosjs

const cosmosjs = require("@cosmostation/cosmosjs");
```
#### Browser
```
<script src='js/cosmosjs-bundle.js'></script>
```

### - Generate Hupayx address from mnemonic
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




