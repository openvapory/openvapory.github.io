# The `eth` Module

## The default block parameter

The following methods have an optional extra `defaultBlock` parameter:

- [eth_getBalance](#eth_getbalance)
- [eth_getCode](#eth_getcode)
- [eth_getTransactionCount](#eth_gettransactioncount)
- [eth_getStorageAt](#eth_getstorageat)
- [eth_call](#eth_call)

When requests are made that act on the state of Ethereum, the last parameter determines the height of the block.

The following options are possible for the `defaultBlock` parameter:

- `QUANTITY`/`INT` - an integer block number;
- `STR "earliest"` for the earliest/genesis block;
- `STR "latest"` - for the latest mined block;
- `STR "pending"` - for the pending state/transactions.

## JSON-RPC methods

* [eth_protocolVersion](#eth_protocolversion)
* [eth_syncing](#eth_syncing)
* [eth_coinbase](#eth_coinbase)
* [eth_mining](#eth_mining)
* [eth_hashrate](#eth_hashrate)
* [eth_gasPrice](#eth_gasprice)
* [eth_accounts](#eth_accounts)
* [eth_blockNumber](#eth_blocknumber)
* [eth_getBalance](#eth_getbalance)
* [eth_getStorageAt](#eth_getstorageat)
* [eth_getTransactionCount](#eth_gettransactioncount)
* [eth_getBlockTransactionCountByHash](#eth_getblocktransactioncountbyhash)
* [eth_getBlockTransactionCountByNumber](#eth_getblocktransactioncountbynumber)
* [eth_getUncleCountByBlockHash](#eth_getunclecountbyblockhash)
* [eth_getUncleCountByBlockNumber](#eth_getunclecountbyblocknumber)
* [eth_getCode](#eth_getcode)
* [eth_sign](#eth_sign)
* [eth_sendTransaction](#eth_sendtransaction)
* [eth_sendRawTransaction](#eth_sendrawtransaction)
* [eth_call](#eth_call)
* [eth_estimateGas](#eth_estimategas)
* [eth_getBlockByHash](#eth_getblockbyhash)
* [eth_getBlockByNumber](#eth_getblockbynumber)
* [eth_getTransactionByHash](#eth_gettransactionbyhash)
* [eth_getTransactionByBlockHashAndIndex](#eth_gettransactionbyblockhashandindex)
* [eth_getTransactionByBlockNumberAndIndex](#eth_gettransactionbyblocknumberandindex)
* [eth_getTransactionReceipt](#eth_gettransactionreceipt)
* [eth_getUncleByBlockHashAndIndex](#eth_getunclebyblockhashandindex)
* [eth_getUncleByBlockNumberAndIndex](#eth_getunclebyblocknumberandindex)
* [eth_getCompilers](#eth_getcompilers)
* [eth_compileLLL](#eth_compilelll)
* [eth_compileSolidity](#eth_compilesolidity)
* [eth_compileSerpent](#eth_compileserpent)
* [eth_newFilter](#eth_newfilter)
* [eth_newBlockFilter](#eth_newblockfilter)
* [eth_newPendingTransactionFilter](#eth_newpendingtransactionfilter)
* [eth_uninstallFilter](#eth_uninstallfilter)
* [eth_getFilterChanges](#eth_getfilterchanges)
* [eth_getFilterLogs](#eth_getfilterlogs)
* [eth_getLogs](#eth_getlogs)
* [eth_getWork](#eth_getwork)
* [eth_submitWork](#eth_submitwork)
* [eth_submitHashrate](#eth_submithashrate)

## JSON RPC API Reference

***

#### eth_protocolVersion

Returns the current ethereum protocol version.

##### Parameters
none

##### Returns

`String` - The current ethereum protocol version

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_protocolVersion","params":[],"id":67}' localhost:8545

// Result
{
  "id":67,
  "jsonrpc": "2.0",
  "result": "54"
}
```

***

#### eth_syncing

Returns an object with data about the sync status or `false`.


##### Parameters
none

##### Returns

`Object|Boolean`, An object with sync status data or `FALSE`, when not syncing:
  - `startingBlock`: `QUANTITY` - The block at which the import started (will only be reset, after the sync reached his head)
  - `currentBlock`: `QUANTITY` - The current block, same as eth_blockNumber
  - `highestBlock`: `QUANTITY` - The estimated highest block

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_syncing","params":[],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": {
    startingBlock: '0x384',
    currentBlock: '0x386',
    highestBlock: '0x454'
  }
}
// Or when not syncing
{
  "id":1,
  "jsonrpc": "2.0",
  "result": false
}
```

***

#### eth_coinbase

Returns the client coinbase address.


##### Parameters
none

##### Returns

`DATA`, 20 bytes - the current coinbase address.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_coinbase","params":[],"id":64}' localhost:8545

// Result
{
  "id":64,
  "jsonrpc": "2.0",
  "result": "0x407d73d8a49eeb85d32cf465507dd71d507100c1"
}
```

***

#### eth_mining

Returns `true` if client is actively mining new blocks.

##### Parameters
none

##### Returns

`Boolean` - returns `true` of the client is mining, otherwise `false`.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_mining","params":[],"id":71}' localhost:8545

// Result
{
  "id":71,
  "jsonrpc": "2.0",
  "result": true
}

```

***

#### eth_hashrate

Returns the number of hashes per second that the node is mining with.

##### Parameters
none

##### Returns

`QUANTITY` - number of hashes per second.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_hashrate","params":[],"id":71}' localhost:8545

// Result
{
  "id":71,
  "jsonrpc": "2.0",
  "result": "0x38a"
}

```

***

#### eth_gasPrice

Returns the current price per gas in wei.

##### Parameters
none

##### Returns

`QUANTITY` - integer of the current gas price in wei.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":73}' localhost:8545

// Result
{
  "id":73,
  "jsonrpc": "2.0",
  "result": "0x09184e72a000" // 10000000000000
}
```

***

#### eth_accounts

Returns a list of addresses owned by client.


##### Parameters
none

##### Returns

`Array of DATA`, 20 Bytes - addresses owned by the client.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_accounts","params":[],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": ["0x407d73d8a49eeb85d32cf465507dd71d507100c1"]
}
```

***

#### eth_blockNumber

Returns the number of most recent block.

##### Parameters
none

##### Returns

`QUANTITY` - integer of the current block number the client is on.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":83}' localhost:8545

// Result
{
  "id":83,
  "jsonrpc": "2.0",
  "result": "0x4b7" // 1207
}
```

***

#### eth_getBalance

Returns the balance of the account of given address.

##### Parameters

1. `DATA`, 20 Bytes - address to check for balance.
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

```js
params: [
   '0x407d73d8a49eeb85d32cf465507dd71d507100c1',
   'latest'
]
```

##### Returns

`QUANTITY` - integer of the current balance in wei.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1", "latest"],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x0234c8a3397aab58" // 158972490234375000
}
```

***

#### eth_getStorageAt

Returns the value from a storage position at a given address.


##### Parameters

1. `DATA`, 20 Bytes - address of the storage.
2. `QUANTITY` - integer of the position in the storage.
3. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)


```js
params: [
   '0x407d73d8a49eeb85d32cf465507dd71d507100c1',
   '0x0', // storage position at 0
   '0x2' // state at block number 2
]
```

##### Returns

`DATA`, 32 Bytes - the value at this storage position.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getStorageAt","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1", "0x0", "0x2"],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x0000000000000000000000000000000000000000000000000000000000000003"
}
```

***

#### eth_getTransactionCount

Returns the number of transactions *sent* from an address.


##### Parameters

1. `DATA`, 20 Bytes - address.
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

```js
params: [
   '0x407d73d8a49eeb85d32cf465507dd71d507100c1',
   'latest' // state at the latest block
]
```

##### Returns

`QUANTITY` - integer of the number of transactions send from this address.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1","latest"],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_getBlockTransactionCountByHash

Returns the number of transactions in a block from a block matching the given block hash.


##### Parameters

1. `DATA`, 32 Bytes - hash of a block

```js
params: [
   '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238'
]
```

##### Returns

`QUANTITY` - integer of the number of transactions in this block.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByHash","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xb" // 11
}
```

***

#### eth_getBlockTransactionCountByNumber

Returns the number of transactions in a block from a block matching the given block number.


##### Parameters

1. `QUANTITY|TAG` - integer of a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](#the-default-block-parameter).

```js
params: [
   '0xe8', // 232
]
```

##### Returns

`QUANTITY` - integer of the number of transactions in this block.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByNumber","params":["0xe8"],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xa" // 10
}
```

***

#### eth_getUncleCountByBlockHash

Returns the number of uncles in a block from a block matching the given block hash.


##### Parameters

1. `DATA`, 32 Bytes - hash of a block

```js
params: [
   '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238'
]
```

##### Returns

`QUANTITY` - integer of the number of uncles in this block.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getUncleCountByBlockHash","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id"Block:1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_getUncleCountByBlockNumber

Returns the number of uncles in a block from a block matching the given block number.


##### Parameters

1. `QUANTITY` - integer of a block number, or the string "latest", "earliest" or "pending", see the [default block parameter](#the-default-block-parameter)

```js
params: [
   '0xe8', // 232
]
```

##### Returns

`QUANTITY` - integer of the number of uncles in this block.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getUncleCountByBlockNumber","params":["0xe8"],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_getCode

Returns code at a given address.


##### Parameters

1. `DATA`, 20 Bytes - address
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

```js
params: [
   '0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b',
   '0x2'  // 2
]
```

##### Returns

`DATA` - the code from the given address.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getCode","params":["0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b", "0x2"],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x600160008035811a818181146012578301005b601b6001356025565b8060005260206000f25b600060078202905091905056"
}
```

***

#### eth_sign

Signs data with a given address.

**Note** the address to sign must be unlocked.

##### Parameters

1. `DATA`, 20 Bytes - address
2. `DATA`, Data to sign

##### Returns

`DATA`: Signed data

##### Example

```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_sign","params":["0xd1ade25ccd3d550a7eb532ac759cac7be09c2719", "Schoolbus"],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x2ac19db245478a06032e69cdbd2b54e648b78431d0a47bd1fbab18f79f820ba407466e37adbe9e84541cab97ab7d290f4a64a5825c876d22109f3bf813254e8628"
}
```



***

#### eth_sendTransaction

Creates new message call transaction or a contract creation, if the data field contains code.

##### Parameters

1. `Object` - The transaction object
  - `from`: `DATA`, 20 Bytes - The address the transaction is send from.
  - `to`: `DATA`, 20 Bytes - (optional when creating new contract) The address the transaction is directed to.
  - `gas`: `QUANTITY`  - (optional, default: 90000) Integer of the gas provided for the transaction execution. It will return unused gas.
  - `gasPrice`: `QUANTITY`  - (optional, default: To-Be-Determined) Integer of the gasPrice used for each paid gas
  - `value`: `QUANTITY`  - (optional) Integer of the value send with this transaction
  - `data`: `DATA`  - The compiled code of a contract OR the hash of the invoked method signature and encoded parameters. For details see [Ethereum Contract ABI](https://github.com/ethereum/wiki/wiki/Ethereum-Contract-ABI)
  - `nonce`: `QUANTITY`  - (optional) Integer of a nonce. This allows to overwrite your own pending transactions that use the same nonce.

```js
params: [{
  "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
  "to": "0xd46e8dd67c5d32be8058bb8eb970870f072445675",
  "gas": "0x76c0", // 30400,
  "gasPrice": "0x9184e72a000", // 10000000000000
  "value": "0x9184e72a", // 2441406250
  "data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"
}]
```

##### Returns

`DATA`, 32 Bytes - the transaction hash, or the zero hash if the transaction is not yet available.

Use [eth_getTransactionReceipt](#eth_gettransactionreceipt) to get the contract address, after the transaction was mined, when you created a contract.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_sendTransaction","params":[{see above}],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"
}
```

***

#### eth_sendRawTransaction

Creates new message call transaction or a contract creation for signed transactions.

##### Parameters

1. `DATA`, The signed transaction data.

```js
params: ["0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"]
```

##### Returns

`DATA`, 32 Bytes - the transaction hash, or the zero hash if the transaction is not yet available.

Use [eth_getTransactionReceipt](#eth_gettransactionreceipt) to get the contract address, after the transaction was mined, when you created a contract.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":[{see above}],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"
}
```

***

#### eth_call

Executes a new message call immediately without creating a transaction on the block chain.


##### Parameters

1. `Object` - The transaction call object
  - `from`: `DATA`, 20 Bytes - (optional) The address the transaction is send from.
  - `to`: `DATA`, 20 Bytes  - The address the transaction is directed to.
  - `gas`: `QUANTITY`  - (optional) Integer of the gas provided for the transaction execution. eth_call consumes zero gas, but this parameter may be needed by some executions.
  - `gasPrice`: `QUANTITY`  - (optional) Integer of the gasPrice used for each paid gas
  - `value`: `QUANTITY`  - (optional) Integer of the value send with this transaction
  - `data`: `DATA`  - (optional) Hash of the method signature and encoded parameters. For details see [Ethereum Contract ABI](https://github.com/ethereum/wiki/wiki/Ethereum-Contract-ABI)
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Returns

`DATA` - the return value of executed contract.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_call","params":[{see above}],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x0"
}
```

***

#### eth_estimateGas

Makes a call or transaction, which won't be added to the blockchain and returns the used gas, which can be used for estimating the used gas.

##### Parameters

See [eth_call](#eth_call) parameters, expect that all properties are optional.

##### Returns

`QUANTITY` - the amount of gas used.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_estimateGas","params":[{see above}],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x5208" // 21000
}
```

***

#### eth_getBlockByHash

Returns information about a block by hash.


##### Parameters

1. `DATA`, 32 Bytes - Hash of a block.
2. `Boolean` - If `true` it returns the full transaction objects, if `false` only the hashes of the transactions.

```js
params: [
   '0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331',
   true
]
```

##### Returns

`Object` - A block object, or `null` when no block was found:

  - `number`: `QUANTITY` - the block number. `null` when its pending block.
  - `hash`: `DATA`, 32 Bytes - hash of the block. `null` when its pending block.
  - `parentHash`: `DATA`, 32 Bytes - hash of the parent block.
  - `sealFields`: an array of the fields for the block's seal or `null` when its pending block. For Ethash, this is the `mixHash` (`DATA`, 32 Bytes) followed by the `nonce` (`DATA`, 8 Bytes).
  - `sha3Uncles`: `DATA`, 32 Bytes - SHA3 of the uncles data in the block.
  - `logsBloom`: `DATA`, 256 Bytes - the bloom filter for the logs of the block. `null` when its pending block.
  - `transactionsRoot`: `DATA`, 32 Bytes - the root of the transaction trie of the block.
  - `stateRoot`: `DATA`, 32 Bytes - the root of the final state trie of the block.
  - `receiptsRoot`: `DATA`, 32 Bytes - the root of the receipts trie of the block.
  - `miner`: `DATA`, 20 Bytes - the address of the beneficiary to whom the mining rewards were given.
  - `difficulty`: `QUANTITY` - integer of the difficulty for this block.
  - `totalDifficulty`: `QUANTITY` - integer of the total difficulty of the chain until this block.
  - `extraData`: `DATA` - the "extra data" field of this block.
  - `size`: `QUANTITY` - integer the size of this block in bytes.
  - `gasLimit`: `QUANTITY` - the maximum gas allowed in this block.
  - `gasUsed`: `QUANTITY` - the total used gas by all transactions in this block.
  - `timestamp`: `QUANTITY` - the unix timestamp for when the block was collated.
  - `transactions`: `Array` - Array of transaction objects, or 32 Bytes transaction hashes depending on the last given parameter.
  - `uncles`: `Array` - Array of uncle hashes.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockByHash","params":["0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331", true],"id":1}' localhost:8545

// Result
{
"id":1,
"jsonrpc":"2.0",
"result": {
    "number": "0x1b4", // 436
    "hash": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331",
    "parentHash": "0x9646252be9520f6e71339a8df9c55e4d7619deeb018d2a3f2d21fc165dde5eb5",
    "sealFields": ["0xe04d296d2460cfb8472af2c5fd05b5a214109c25688d3704aed5484f9a7792f2", "0x0000000000000042"],
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "logsBloom": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331",
    "transactionsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "stateRoot": "0xd5855eb08b3387c0af375e9cdb6acfc05eb8f519e419b874b6ff2ffda7ed1dff",
    "miner": "0x4e65fda2159562a496f9f3522f89122a3088497a",
    "difficulty": "0x027f07", // 163591
    "totalDifficulty":  "0x027f07", // 163591
    "extraData": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "size":  "0x027f07", // 163591
    "gasLimit": "0x9f759", // 653145
    "minGasPrice": "0x9f759", // 653145
    "gasUsed": "0x9f759", // 653145
    "timestamp": "0x54e34e8e" // 1424182926
    "transactions": [{...},{ ... }] 
    "uncles": ["0x1606e5...", "0xd5145a9..."]
  }
}
```

***

#### eth_getBlockByNumber

Returns information about a block by block number.

##### Parameters

1. `QUANTITY|TAG` - integer of a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](#the-default-block-parameter).
2. `Boolean` - If `true` it returns the full transaction objects, if `false` only the hashes of the transactions.

```js
params: [
   '0x1b4', // 436
   true
]
```

##### Returns

See [eth_getBlockByHash](#eth_getblockbyhash)

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0x1b4", true],"id":1}' localhost:8545
```

Result see [eth_getBlockByHash](#eth_getblockbyhash)

***

#### eth_getTransactionByHash

Returns the information about a transaction requested by transaction hash.


##### Parameters

1. `DATA`, 32 Bytes - hash of a transaction

```js
params: [
   "0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"
]
```

##### Returns

`Object` - A transaction object, or `null` when no transaction was found:

  - `hash`: `DATA`, 32 Bytes - hash of the transaction.
  - `nonce`: `QUANTITY` - the number of transactions made by the sender prior to this one.
  - `blockHash`: `DATA`, 32 Bytes - hash of the block where this transaction was in. `null` when its pending.
  - `blockNumber`: `QUANTITY` - block number where this transaction was in. `null` when its pending.
  - `transactionIndex`: `QUANTITY` - integer of the transactions index position in the block. `null` when its pending.
  - `from`: `DATA`, 20 Bytes - address of the sender.
  - `to`: `DATA`, 20 Bytes - address of the receiver. `null` when its a contract creation transaction.
  - `value`: `QUANTITY` - value transferred in Wei.
  - `gasPrice`: `QUANTITY` - gas price provided by the sender in Wei.
  - `gas`: `QUANTITY` - gas provided by the sender.
  - `input`: `DATA` - the data send along with the transaction.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionByHash","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}' localhost:8545

// Result
{
"id":1,
"jsonrpc":"2.0",
"result": {
    "hash":"0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b",
    "nonce":"0x",
    "blockHash": "0xbeab0aa2411b7ab17f30a99d3cb9c6ef2fc5426d6ad6fd9e2a26a6aed1d1055b",
    "blockNumber": "0x15df", // 5599
    "transactionIndex":  "0x1", // 1
    "from":"0x407d73d8a49eeb85d32cf465507dd71d507100c1",
    "to":"0x85h43d8a49eeb85d32cf465507dd71d507100c1",
    "value":"0x7f110" // 520464
    "gas": "0x7f110" // 520464
    "gasPrice":"0x09184e72a000",
    "input":"0x603880600c6000396000f300603880600c6000396000f3603880600c6000396000f360",
  }
}
```

***

#### eth_getTransactionByBlockHashAndIndex

Returns information about a transaction by block hash and transaction index position.


##### Parameters

1. `DATA`, 32 Bytes - hash of a block.
2. `QUANTITY` - integer of the transaction index position.

```js
params: [
   '0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331',
   '0x0' // 0
]
```

##### Returns

See [eth_getBlockByHash](#eth_gettransactionbyhash)

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionByBlockHashAndIndex","params":[0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b, "0x0"],"id":1}' localhost:8545
```

Result see [eth_getTransactionByHash](#eth_gettransactionbyhash)

***

#### eth_getTransactionByBlockNumberAndIndex

Returns information about a transaction by block number and transaction index position.


##### Parameters

1. `QUANTITY|TAG` - a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](#the-default-block-parameter).
2. `QUANTITY` - the transaction index position.

```js
params: [
   '0x29c', // 668
   '0x0' // 0
]
```

##### Returns

See [eth_getBlockByHash](#eth_gettransactionbyhash)

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionByBlockNumberAndIndex","params":["0x29c", "0x0"],"id":1}' localhost:8545
```

Result see [eth_getTransactionByHash](#eth_gettransactionbyhash)

***

#### eth_getTransactionReceipt

Returns the receipt of a transaction by transaction hash.

**Note** That the receipt is available even for pending transactions.

##### Parameters

1. `DATA`, 32 Bytes - hash of a transaction

```js
params: [
   '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238'
]
```

##### Returns

`Object` - A transaction receipt object, or `null` when no receipt was found:

  - `transactionHash `: `DATA`, 32 Bytes - hash of the transaction.
  - `transactionIndex`: `QUANTITY` - integer of the transactions index position in the block.
  - `blockHash`: `DATA`, 32 Bytes - hash of the block where this transaction was in.
  - `blockNumber`: `QUANTITY` - block number where this transaction was in.
  - `cumulativeGasUsed `: `QUANTITY ` - The total amount of gas used when this transaction was executed in the block.
  - `gasUsed `: `QUANTITY ` - The amount of gas used by this specific transaction alone.
  - `contractAddress `: `DATA`, 20 Bytes - The contract address created, if the transaction was a contract creation, otherwise `null`.
  - `logs`: `Array` - Array of log objects, which this transaction generated.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionReceipt","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}' localhost:8545

// Result
{
"id":1,
"jsonrpc":"2.0",
"result": {
     transactionHash: '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238',
     transactionIndex:  '0x1', // 1
     blockNumber: '0xb', // 11
     blockHash: '0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b',
     cumulativeGasUsed: '0x33bc', // 13244
     gasUsed: '0x4dc', // 1244
     contractAddress: '0xb60e8dd61c5d32be8058bb8eb970870f07233155' // or null, if none was created
     logs: [{
         // logs as returned by getFilterLogs, etc.
     }, ...]
  }
}
```

***

#### eth_getUncleByBlockHashAndIndex

Returns information about a uncle of a block by hash and uncle index position.


##### Parameters


1. `DATA`, 32 Bytes - hash a block.
2. `QUANTITY` - the uncle's index position.

```js
params: [
   '0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b',
   '0x0' // 0
]
```

##### Returns

See [eth_getBlockByHash](#eth_getblockbyhash)

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getUncleByBlockHashAndIndex","params":["0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b", "0x0"],"id":1}' localhost:8545
```

Result see [eth_getBlockByHash](#eth_getblockbyhash)

**Note**: An uncle doesn't contain individual transactions.

***

#### eth_getUncleByBlockNumberAndIndex

Returns information about a uncle of a block by number and uncle index position.


##### Parameters

1. `QUANTITY|TAG` - a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](#the-default-block-parameter).
2. `QUANTITY` - the uncle's index position.

```js
params: [
   '0x29c', // 668
   '0x0' // 0
]
```

##### Returns

See [eth_getBlockByHash](#eth_getblockbyhash)

**Note**: An uncle doesn't contain individual transactions.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getUncleByBlockNumberAndIndex","params":["0x29c", "0x0"],"id":1}' localhost:8545
```

Result see [eth_getBlockByHash](#eth_getblockbyhash)

***

#### eth_getCompilers

Returns a list of available compilers in the client.

##### Parameters
none

##### Returns

`Array` - Array of available compilers.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getCompilers","params":[],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": ["solidity", "lll", "serpent"]
}
```

***

#### eth_compileSolidity

Returns compiled solidity code.

##### Parameters

1. `String` - The source code.

```js
params: [
   "contract test { function multiply(uint a) returns(uint d) {   return a * 7;   } }",
]
```

##### Returns

`DATA` - The compiled source code.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_compileSolidity","params":["contract test { function multiply(uint a) returns(uint d) {   return a * 7;   } }"],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": {
      "code": "0x605880600c6000396000f3006000357c010000000000000000000000000000000000000000000000000000000090048063c6888fa114602e57005b603d6004803590602001506047565b8060005260206000f35b60006007820290506053565b91905056",
      "info": {
        "source": "contract test {\n   function multiply(uint a) constant returns(uint d) {\n       return a * 7;\n   }\n}\n",
        "language": "Solidity",
        "languageVersion": "0",
        "compilerVersion": "0.9.19",
        "abiDefinition": [
          {
            "constant": true,
            "inputs": [
              {
                "name": "a",
                "type": "uint256"
              }
            ],
            "name": "multiply",
            "outputs": [
              {
                "name": "d",
                "type": "uint256"
              }
            ],
            "type": "function"
          }
        ],
        "userDoc": {
          "methods": {}
        },
        "developerDoc": {
          "methods": {}
        }
      }

}
```

***

#### eth_compileLLL

Returns compiled LLL code.

##### Parameters

1. `String` - The source code.

```js
params: [
   "(returnlll (suicide (caller)))",
]
```

##### Returns

`DATA` - The compiled source code.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_compileLLL","params":["(returnlll (suicide (caller)))"],"id":1}' localhost: 8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x603880600c6000396000f3006001600060e060020a600035048063c6888fa114601857005b6021600435602b565b8060005260206000f35b600081600702905091905056" // the compiled source code
}
```

***

#### eth_compileSerpent

Returns compiled serpent code.

##### Parameters

1. `String` - The source code.

```js
params: [
   "/* some serpent */",
]
```

##### Returns

`DATA` - The compiled source code.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_compileSerpent","params":["/* some serpent */"],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x603880600c6000396000f3006001600060e060020a600035048063c6888fa114601857005b6021600435602b565b8060005260206000f35b600081600702905091905056" // the compiled source code
}
```

***

#### eth_newFilter

Creates a filter object, based on filter options, to notify when the state changes (logs).
To check if the state has changed, call [eth_getFilterChanges](#eth_getfilterchanges).

##### A note on specifying topic filters:
Topics are order-dependent. A transaction with a log with topics [A, B] will be matched by the following topic filters:
* `[]` "anything"
* `[A]` "A in first position (and anything after)"
* `[null, B]` "anything in first position AND B in second position (and anything after)"
* `[A, B]` "A in first position AND B in second position (and anything after)"
* `[[A, B], [A, B]]` "(A OR B) in first position AND (A OR B) in second position (and anything after)"

##### Parameters

1. `Object` - The filter options:
  - `fromBlock`: `QUANTITY|TAG` - (optional, default: `"latest"`) Integer block number, or `"latest"` for the last mined block or `"pending"`, `"earliest"` for not yet mined transactions.
  - `toBlock`: `QUANTITY|TAG` - (optional, default: `"latest"`) Integer block number, or `"latest"` for the last mined block or `"pending"`, `"earliest"` for not yet mined transactions.
  - `address`: `DATA|Array`, 20 Bytes - (optional) Contract address or a list of addresses from which logs should originate.
  - `topics`: `Array of DATA`,  - (optional) Array of 32 Bytes `DATA` topics. Topics are order-dependent. Each topic can also be an array of DATA with "or" options.

```js
params: [{
  "fromBlock": "0x1",
  "toBlock": "0x2",
  "address": "0x8888f1f195afa192cfee860698584c030f4c9db1",
  "topics": ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b", null, [0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b, 0x000000000000000000000000aff3454fce5edbc8cca8697c15331677e6ebccc]]
}]
```

##### Returns

`QUANTITY` - A filter id.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_newFilter","params":[{"topics":["0x12341234"]}],"id":1}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_newBlockFilter

Creates a filter in the node, to notify when a new block arrives.
To check if the state has changed, call [eth_getFilterChanges](#eth_getfilterchanges).

##### Parameters
None

##### Returns

`QUANTITY` - A filter id.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_newBlockFilter","params":[],"id":73}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc":  "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_newPendingTransactionFilter

Creates a filter in the node, to notify when new pending transactions arrive.
To check if the state has changed, call [eth_getFilterChanges](#eth_getfilterchanges).

##### Parameters
None

##### Returns

`QUANTITY` - A filter id.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_newPendingTransactionFilter","params":[],"id":73}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc":  "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_uninstallFilter

Uninstalls a filter with given id. Should always be called when watch is no longer needed.
Additonally Filters timeout when they aren't requested with [eth_getFilterChanges](#eth_getfilterchanges) for a period of time.


##### Parameters

1. `QUANTITY` - The filter id.

```js
params: [
  "0xb" // 11
]
```

##### Returns

`Boolean` - `true` if the filter was successfully uninstalled, otherwise `false`.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_uninstallFilter","params":["0xb"],"id":73}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": true
}
```

***

#### eth_getFilterChanges

Polling method for a filter, which returns an array of logs which occurred since last poll.


##### Parameters

1. `QUANTITY` - the filter id.

```js
params: [
  "0x16" // 22
]
```

##### Returns

`Array` - Array of log objects, or an empty array if nothing has changed since last poll.

- For filters created with `eth_newBlockFilter` the return are block hashes (`DATA`, 32 Bytes), e.g. `["0x3454645634534..."]`.
- For filters created with `eth_newPendingTransactionFilter ` the return are transaction hashes (`DATA`, 32 Bytes), e.g. `["0x6345343454645..."]`.
- For filters created with `eth_newFilter` logs are objects with following params:

  - `type`: `TAG` - `pending` when the log is pending. `mined` if log is already mined.
  - `logIndex`: `QUANTITY` - integer of the log index position in the block. `null` when its pending log.
  - `transactionIndex`: `QUANTITY` - integer of the transactions index position log was created from. `null` when its pending log.
  - `transactionHash`: `DATA`, 32 Bytes - hash of the transactions this log was created from. `null` when its pending log.
  - `blockHash`: `DATA`, 32 Bytes - hash of the block where this log was in. `null` when its pending. `null` when its pending log.
  - `blockNumber`: `QUANTITY` - the block number where this log was in. `null` when its pending. `null` when its pending log.
  - `address`: `DATA`, 20 Bytes - address from which this log originated.
  - `data`: `DATA` - contains one or more 32 Bytes non-indexed arguments of the log.
  - `topics`: `Array of DATA` - Array of 0 to 4 32 Bytes `DATA` of indexed log arguments. (In *solidity*: The first topic is the *hash* of the signature of the event (e.g. `Deposit(address,bytes32,uint256)`), except you declared the event with the `anonymous` specifier.)

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getFilterChanges","params":["0x16"],"id":73}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": [{
    "logIndex": "0x1", // 1
    "blockNumber":"0x1b4" // 436
    "blockHash": "0x8216c5785ac562ff41e2dcfdf5785ac562ff41e2dcfdf829c5a142f1fccd7d",
    "transactionHash":  "0xdf829c5a142f1fccd7d8216c5785ac562ff41e2dcfdf5785ac562ff41e2dcf",
    "transactionIndex": "0x0", // 0
    "address": "0x16c5785ac562ff41e2dcfdf829c5a142f1fccd7d",
    "data":"0x0000000000000000000000000000000000000000000000000000000000000000",
    "topics": ["0x59ebeb90bc63057b6515673c3ecf9438e5058bca0f92585014eced636878c9a5"]
    },{
      ...
    }]
}
```

***

#### eth_getFilterLogs

Returns an array of all logs matching filter with given id.


##### Parameters

1. `QUANTITY` - The filter id.

```js
params: [
  "0x16" // 22
]
```

##### Returns

See [eth_getFilterChanges](#eth_getfilterchanges)

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getFilterLogs","params":["0x16"],"id":74}' localhost:8545
```

Result see [eth_getFilterChanges](#eth_getfilterchanges)

***

#### eth_getLogs

Returns an array of all logs matching a given filter object.

##### Parameters

1. `Object` - the filter object, see [eth_newFilter parameters](#eth_newfilter).

```js
params: [{
  "topics": ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]
}]
```

##### Returns

See [eth_getFilterChanges](#eth_getfilterchanges)

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getLogs","params":[{"topics":["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]}],"id":74}' localhost:8545
```

Result see [eth_getFilterChanges](#eth_getfilterchanges)

***

#### eth_getWork

Returns the hash of the current block, the seedHash, and the boundary condition to be met ("target").

##### Parameters
none

##### Returns

`Array` - Array with the following properties:
  1. `DATA`, 32 Bytes - current block header pow-hash.
  2. `DATA`, 32 Bytes - the seed hash used for the DAG.
  3. `DATA`, 32 Bytes - the boundary condition ("target"), 2^256 / difficulty.
  4. `QUANTITY` - the current block number.

##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_getWork","params":[],"id":73}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": [
      "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
      "0x5EED00000000000000000000000000005EED0000000000000000000000000000",
      "0xd1ff1c01710000000000000000000000d1ff1c01710000000000000000000000",
      "0x1"
    ]
}
```

***

#### eth_submitWork

Used for submitting a proof-of-work solution.


##### Parameters

1. `DATA`, 8 Bytes - The nonce found (64 bits)
2. `DATA`, 32 Bytes - The header's pow-hash (256 bits)
3. `DATA`, 32 Bytes - The mix digest (256 bits)

```js
params: [
  "0x0000000000000001",
  "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
  "0xD1FE5700000000000000000000000000D1FE5700000000000000000000000000"
]
```

##### Returns

`Boolean` - returns `true` if the provided solution is valid, otherwise `false`.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0", "method":"eth_submitWork", "params":["0x0000000000000001", "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef", "0xD1GE5700000000000000000000000000D1GE5700000000000000000000000000"],"id":73}' localhost:8545

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": true
}
```

***

#### eth_submitHashrate

Used for submitting mining hashrate.


##### Parameters

1. `Hashrate`, a hexadecimal string representation (32 bytes) of the hash rate 
2. `ID`, String - A random hexadecimal(32 bytes) ID identifying the client

```js
params: [
  "0x0000000000000000000000000000000000000000000000000000000000500000",
  "0x59daa26581d0acd1fce254fb7e85952f4c09d0915afd33d3886cd914bc7d283c"
]
```

##### Returns

`Boolean` - returns `true` if submitting went through succesfully and `false` otherwise.


##### Example
```js
// Request
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0", "method":"eth_submitHashrate", "params":["0x0000000000000000000000000000000000000000000000000000000000500000", "0x59daa26581d0acd1fce254fb7e85952f4c09d0915afd33d3886cd914bc7d283c"],"id":73}' localhost:8545

// Result
{
  "id":73,
  "jsonrpc":"2.0",
  "result": true
}
```