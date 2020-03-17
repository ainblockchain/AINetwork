# Transaction API

## ain\_getPendingTransactions

Returns currently pending transactions.

### Parameters

None.

### Returns

`Array` - A list of pending transactions.

### **Example**

`// Request  
curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"ain_getPendingTransactions"}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":[  
    {  
      "status":"PENDING",  
      "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
      "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
      "signature":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f3...",  
      "timestamp":1566736760322,  
      "nonce":-1,  
      "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56...",  
    },  
    {  
      "status":"PENDING",  
      "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
      "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
      "signature":"0x1ec191ef20b0e9628c4397665977cb...",  
      "timestamp":1566736800358,  
      "nonce":99  
    }  
  ]  
}`

## **ain\_getTransactionByBlockNumberAndIndex**

Returns the transaction at the {index} position within the block with the {block\_number}.

### **Parameters**

An object with 2 properties:

* block\_number: `Number` - block number
* index: `Number` - index of the transaction within the block

### Returns

`Object` - The transaction.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,  
  "method":"ain_getTransactionByBlockNumberAndIndex",  
  "params":{"block_number":10,"index":2}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    "block_hash":"0x1d59ff54b1eb26b013ce3cb5fc9dab3705b415a67127...",  
    "block_number":10,  
    "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
    "index":2,  
    "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
    "signature":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f3...",  
    "timestamp":1566736760322,  
    "nonce":-1,  
    "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56...",  
    "operation":{ ... }  
  }  
}`

## **ain\_getTransactionByBlockHashAndIndex**

Returns the transaction at the {index} position in the block with the {block\_hash}.

### **Parameters**

An object with 2 properties:

* block\_hash: `String` - block hash
* index: `Number` - index of the transaction within the block

### Returns

`Object` - The transaction.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getTransactionByBlockHashAndIndex",   
  "params":{"block_hash":"0x4c31dbb8d0237fa4c7ddc1e549f...","index":2}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    "block_hash":"0x4c31dbb8d0237fa4c7ddc1e549f...",  
    "block_number":6139707,  
    "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
    "index":7,  
    "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
    "signature":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f3...",  
    "timestamp":1566736760322,  
    "nonce":-1,  
    "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56...",  
    "operation":{ ... }  
  }  
}`

## ain\_getTransactionByHash

Returns the transaction with the hash.

### **Parameters**

An object with a property:

* hash: `String` - transaction hash

### Returns

`Object` - the transaction.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getTransactionByHash",   
  "params":{"hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a..."}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    "block_hash":"0x4c31dbb8d0237fa4c7ddc1e549f...",  
    "block_number":6139707,  
    "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",  
    "index":7,  
    "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",  
    "signature":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f3...",  
    "timestamp":1566736760322,  
    "nonce":-1,  
    "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56...",  
    "operation":{ ... }  
  }  
}`

## ain\_sendSignedTransaction

Sends the signature and the transaction object to the node.

### **Parameters**

An object with following properties:

* signature: `String` - signature of the transaction
* transaction: `Object` ****- transaction object

### Returns

`String` - the transaction's hash.

### Example

`// Request  
curl -X POST --data   
'{  
   "jsonrpc":"2.0",   
   "id":1,   
   "method":"ain_sendSignedTransaction",   
   "params":{  
     "signature":"0xdb61efd63af93089c3754e69a9eb887c5e15b2b7e4120f0d98f...",  
     "transaction":{  
       "nonce":123,  
       "timestamp":1566736760322,  
       "operation":{  
         "ref":"/account/0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812/balance",  
         "type":"SET_VALUE",  
         "value":1000  
       },  
       "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56..."  
     },  
   ]  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",  
  "id":1,  
  "result":"0x88df016429689c079f3b2f6ad39fa052532c56795b733da7..."  
}`

## ain\_sendSignedTransactionBatch

Sends multiple transactions at once.

### Parameters

An object with a property:

* `Array` - an array of transaction objects \(with signature and transaction properties\)

### Returns

`Array` - an array of transaction hashes.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_sendSignedTransactionBatch",   
  "params":{"tx_list":[  
    {  
      "signature":"0xaabc9ddafffb2ae0bac4107697547d22d9383...",  
      "transaction":{  
        "nonce":120,  
        "timestamp":1566736760322,  
        "operation":{"ref":"path/","value":"value","type":"SET_VALUE"}  
      }  
    },  
    {  
      "signature":"0x1ec191ef20b0e9628c4397665977cb...",  
      "transaction":{  
        "nonce":121,  
        "timestamp":1566736760400,  
        "operation":{"ref":"path/path/","value":100,"type":"SET_VALUE"}  
      }  
    }  
  ]}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",  
  "id":1,  
  "result":[  
    "0x88df016429689c079f3b2f6ad39fa052532c56795b733da7...",  
    "0x8e4340ea3983d86e4b6c44249362f716ec9e09849ef9b6e3..."  
  ]  
}`

