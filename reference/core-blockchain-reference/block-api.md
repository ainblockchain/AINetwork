# Block API

## ain\_getRecentBlock

Returns the most recent block.

### Parameters

None.

### Returns

`Object` - The most recent block.

### **Example**

`// Request  
curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"ain_getRecentBlock"}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    "timestamp":1564845946382,  
    "hash":"0x7a6c2a5a91ce3731310885eff761f7ee39484...",  
    "parent_hash":"0xe670ec64341771606e55d6b4ca35a1a6b75...",  
    "number":675,  
    "proposer":"0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812",  
    "validators":[  
      "0x4e65fda2159562a496f9f3522f89122a3088497a",  
      "0xd46e8dd67c5d32be8058bb8eb970870f07244567",  
      "0xb60e8dd61c5d32be8058bb8eb970870f07233155"  
    ],  
    "size":163591,  
    "transactions":[  
      {  
        "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
        "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
        "signature":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f3...",  
        "timestamp":1566736760322,  
        "nonce":-1,  
        "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56...",  
        "operation":{ ... }  
      },  
      {  
        "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
        "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
        "signature":"0x1ec191ef20b0e9628c4397665977cb...",  
        "timestamp":1566736780022,  
        "nonce":99,  
        "operation":{ ... }  
      },  
      ...  
    ]  
  }  
}`

## ain\_getRecentBlockNumber

Returns the most recent block's block number.

### Parameters

None.

### Returns

`Number` - The most recent block's block number.

### **Example**

`// Request  
curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"ain_getRecentBlockNumber"}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":98347  
}`

## ain\_getBlockByNumber

Returns the block with the given block number.

### **Parameters**

An object with properties:

* number: `Number` - the block number
* getFullTransactions: `Boolean` - if true, it returns full transaction objects; if false or undefined, it returns the transaction hashes only.

### Returns

`Object` - A block object.

### **Example**

`// Request  
curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"ain_getBlockByNumber","params":{"number":675,"getFullTransactions":true}}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    "timestamp":1564845946382,  
    "hash":"0x7a6c2a5a91ce3731310885eff761f7ee39484...",  
    "parent_hash":"0xe670ec64341771606e55d6b4ca35a1a6b75...",  
    "number":675,  
    "proposer":"0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812",  
    "validators":[  
      "0x4e65fda2159562a496f9f3522f89122a3088497a",  
      "0xd46e8dd67c5d32be8058bb8eb970870f07244567",  
      "0xb60e8dd61c5d32be8058bb8eb970870f07233155"  
    ],  
    "size":163591,  
    "transactions":[  
      {  
        "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
        "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
        "signature":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f3...",  
        "timestamp":1566736760322,  
        "nonce":-1,  
        "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56...",  
        "operation":{ ... }  
      },  
      {  
        "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
        "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
        "signature":"0x1ec191ef20b0e9628c4397665977cb...",  
        "timestamp":1566736780022,  
        "nonce":99,  
        "operation":{ ... }  
      },  
      ...  
    ]  
  }  
}`  


## ain\_getBlockByHash

Returns the block with the specified block hash.

### **Parameters**

An object with properties:

* hash: `String` - block hash
* getFullTransactions: `Boolean` - if true, it returns full transaction objects; if false or undefined, it returns the transaction hashes only.

### Returns

`Object` - The block.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getBlockByHash",  
  "params":{"hash":"0x7a6c2a5a91ce3731310885eff761f7ee39484...",  
      "getFullTransactions":true}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    "timestamp":1564845946382,  
    "hash":"0x7a6c2a5a91ce3731310885eff761f7ee39484...",  
    "parent_hash":"0xe670ec64341771606e55d6b4ca35a1a6b75...",  
    "number":67526,  
    "proposer":"0x04aac78e17374fd075d1f11bfe95ef7d8e4ed81",  
    "validators":[  
      "0x4e65fda2159562a496f9f3522f89122a3088497a",  
      "0xd46e8dd67c5d32be8058bb8eb970870f07244567",  
      "0xb60e8dd61c5d32be8058bb8eb970870f07233155"  
    ],  
    "size":163591,  
    "transactions":[  
      {  
        "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
        "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
        "signature":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f3...",  
        "timestamp":1566736760322,  
        "nonce":-1  
        "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56...",  
        "operation":{ ... }  
      },  
      {  
        "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
        "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
        "signature":"0x1ec191ef20b0e9628c4397665977cb...",  
        "timestamp":1566736760400,  
        "nonce":99,  
        "operation":{ ... }  
      },  
      ...  
    ]  
  }  
}`

## ain\_getBlocks

Returns a list of blocks that have a block number between "from" block number and "to" block number.

### Parameters

An object with properties:

* from: `Number` - the block number of the starting block
* to: `Number` - the block number of the last block to get

### Returns

`Array` - The list of blocks.

### **Example**

`// Request  
curl -X POST --data   
'{  
  "jsonrpc":"2.0",  
  "id":1,  
  "method":"ain_getBlocks",  
  "params":{"from":0,"to":100}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":  
  [  
    {  
      "timestamp":1564845946382,  
      "hash":"0x7a6c2a5a91ce3731310885eff761f7ee39484...",  
      "parent_hash":"",  
      "number":0,  
      "proposer":"0x04aac78e17374fd075d1f11bfe95ef7d8e4ed81",  
      "validators":[  
        "0x4e65fda2159562a496f9f3522f89122a3088497a",  
        "0xd46e8dd67c5d32be8058bb8eb970870f07244567",  
        "0xb60e8dd61c5d32be8058bb8eb970870f07233155"  
      ],  
      "size":163591,  
      "transactions":[  
        {  
          "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
          "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
          "signature":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f3...",  
          "timestamp":1566736760322,  
          "nonce":-1  
          "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56...",  
          "operation":{ ... }  
        },  
        {  
          "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
          "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
          "signature":"0x1ec191ef20b0e9628c4397665977cb...",  
          "timestamp":1566736760400,  
          "nonce":99,  
          "operation":{ ... }  
        },  
        ...  
      ]  
    },  
    ...  
  ]  
}`

## ain\_getBlockHeaders

Returns a list of block headers that have a block number between "from" block number and "to" block number.

### Parameters

An object with properties:

* from: `Number` - the block number of the starting block
* to: `Number` - the block number of the last block to get

### Returns

`Array` - The list of block headers.

### **Example**

`// Request  
curl -X POST --data   
'{  
  "jsonrpc":"2.0",  
  "id":1,  
  "method":"ain_getBlockHeaders",  
  "params":{"from":0,"to":100}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":  
  [  
    {  
      "timestamp":1564845946382,  
      "hash":"0x7a6c2a5a91ce3731310885eff761f7ee39484...",  
      "parent_hash":"",  
      "number":0,  
      "proposer":"0x04aac78e17374fd075d1f11bfe95ef7d8e4ed81",  
      "validators":[  
        "0x4e65fda2159562a496f9f3522f89122a3088497a",  
        "0xd46e8dd67c5d32be8058bb8eb970870f07244567",  
        "0xb60e8dd61c5d32be8058bb8eb970870f07233155"  
      ],  
      "size":163591,  
    },  
    ...  
  ]  
}`

## ain\_getBlockTransactionCountByNumber

Returns the number of transactions in the block with the specified block number.

### **Parameters**

An object with a property:

* number: `Number` - block number

### Returns

`Number` - Number of transactions in the block.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getBlockTransactionCountByNumber",  
  "params":{"number":"123"}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":11  
}`  


## ain\_getBlockTransactionCountByHash

Returns the number of transactions in the block with the specified block hash.

### **Parameters**

An object with a property:

* hash: `String` - block hash

### Returns

`Number` - Number of transactions

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getBlockTransactionCountByNumber",  
  "params":{"hash":"0x7a6c2a5a91ce3731310885eff761f7ee39484..."}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":11  
}`

## ain\_getProposerByHash

Returns the proposer who produced the block with the given block hash.

### **Parameters**

An object with a property:

* hash: `String` - block hash

### Returns

`String` - The address of the proposer.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getProposerByHash",  
  "params":{"hash":"0x7a6c2a5a91ce3731310885eff761f7ee39484..."}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":"0x04aac78e17374fd075d1f11bfe95ef7d8e4ed81"  
}`

## ain\_getProposerByNumber

Returns the proposer who produced the block with the given block number.

### **Parameters**

An object with a property:

* number: `Number` - block number

### Returns

`String` - The proposer's address.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,  
  "method":"ain_getProposerByNumber",  
  "params":{"number":456}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":"0x04aac78e17374fd075d1f11bfe95ef7d8e4ed81"  
}`

## ain\_getValidatorsByHash

Returns the validators who validated the block.

### **Parameters**

An object with a property:

* hash: `String` - block hash

### Returns

`Array` - The list of validators.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getValidatorsByHash",  
  "params":{"hash":"0x7a6c2a5a91ce3731310885eff761f7ee39484..."}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":[  
    "0x4e65fda2159562a496f9f3522f89122a3088497a",  
    "0xd46e8dd67c5d32be8058bb8eb970870f07244567",  
    "0xb60e8dd61c5d32be8058bb8eb970870f07233155"  
  ]  
}`

## ain\_getValidatorsByNumber

Returns the validators who validated the block.

### **Parameters**

An object with a property:

* number: `Number` - block number

### Returns

`Array` - The list of validators.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getValidatorsByNumber",  
  "params":{"number":2143}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":[  
    "0x4e65fda2159562a496f9f3522f89122a3088497a",  
    "0xd46e8dd67c5d32be8058bb8eb970870f07244567",  
    "0xb60e8dd61c5d32be8058bb8eb970870f07233155"  
  ]  
}`

