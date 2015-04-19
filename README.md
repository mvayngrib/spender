Simple Spend
============

A JavaScript component to create simple Bitcoin / Testnet transactions for integration testing with
the actual network. Can be used in Node.js or the browser (via Browserify).


Install
-------

    npm i --save simple-spend


Usage
-----

### simpleSend(fromWIF, toAddress, amount, [changeAddress], callback)

- `fromWIF`: Private key with matching address that contains funds. Should be base58 check encoded `string`.
- `toAddress`: Recipient address. Should be base58 encoded `string`.
- `amount`: Amount in **satoshis**. Should be an integer. Either `number` or `string`.
- `changeAddress`: Optional change address. If not specified, address calculated from `fromWIF` will be used.
- `callback`: Callback with result. Signature: `(err, txId)`.


### Common Blockchain

Common Blockchain is a unified way to access a blockchain via an API provider. i.e. it provides the same methods and
normalizes results no matter who the API provider is.

You'll need to bring your own [Common Blockchain](https://github.com/common-blockchain/common-blockchain) provider.
Here's a list: https://github.com/common-blockchain/common-blockchain/issues/21


**Example:**

```js
var Blockchain = require('cb-insight') // npm i --save cb-insight
var simpleSend = require('simple-send')

// set common blockchain provider
simpleSend.blockchain = new Blockchain('https://test-insight.bitpay.com')

var fromWIF = '...'
var toAddress = '...'
var amountSatoshis = 500000

simpleSend(fromWIF, toAddress, amountSatoshis, function (err, txId) {
  // use txId to track transaction
  console.log(txId)
})
```


### Limitations

- fixed fee
- bitcoin/testnet only at the moment
- simplified outputs (may change to allow additional like `OP_RETURN`)
- merges all UTXOs


License
-------

MIT
