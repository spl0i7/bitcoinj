
### Welcome to bitcoinrwj

The bitcoinrwj library is a Java implementation of the Bitcoin protocol, which allows it to maintain a wallet and send/receive transactions without needing a local copy of Bitcoin Core. It comes with full documentation and some example apps showing how to use it.

#### Building from the command line

To perform a full build use
```
mvn clean package
```

### Example applications

These are found in the `examples` module.


#### Other GUI Wallet considerations

1) [breadwallet](https://github.com/breadwallet/breadwallet-core) - SPV bitcoin C library
2) [spvwallet](https://github.com/OpenBazaar/spvwallet) - P2P SPV Wallet/Library in Go used in OpenBazaar 2.0
3) [webcoin](https://github.com/mappum/webcoin) - SPV Bitcoin client for Node.js and the browser

#### How to make bitcoinj work for BitcoinRework ?

1) BitcoinRework forked at height `504964` and changed difficulty to 1 (nBits = `0x1d00ffff`) to allow mining of blocks feasible but that caused problem with `checkDifficultyTransitions()` (see commit [35d2391658c515ae1b8efb5383dba2e94fe5abc0](https://github.com/spl0i7/bitcoinrwj/commit/35d2391658c515ae1b8efb5383dba2e94fe5abc0) ) in bitcoinj so that had to be taken care of.

2) `ForkNetParams` (see commit [35d2391658c515ae1b8efb5383dba2e94fe5abc0](https://github.com/spl0i7/bitcoinrwj/commit/35d2391658c515ae1b8efb5383dba2e94fe5abc0) ) was also adjusted according to network parameter requirement for BitcoinRework, please use this class instead of `MainNetParams`.

3) You'll need to add peers manaully when using `ForkNetParamsjava`
```java
bitcoin.setPeerNodes(new PeerAddress(InetAddress.getByName("0x9F598BF6"), 7337));
bitcoin.setPeerNodes(new PeerAddress(InetAddress.getByName("0x9F598120"), 7337));
bitcoin.setPeerNodes(new PeerAddress(InetAddress.getByName("0xA5E3323E"), 7337));
```
Where `bitcoin` in an instance of `WalletAppKit`

4) ProfoBuf serialization of transaction hash is getting corrupted (see commit [35d2391658c515ae1b8efb5383dba2e94fe5abc0](https://github.com/spl0i7/bitcoinrwj/commit/35d2391658c515ae1b8efb5383dba2e94fe5abc0) )  as of now, so warning had to be turned off.

#### Bitcoin Testing status

Tested on linux environment? √
Tested on windows? √

#### Current Issues 

- Fix Protobuf serialization issue.

### Where next?

Now you are ready to [follow the tutorial](https://bitcoinj.github.io/getting-started).

