# Account API

## ain\_getBalance

Returns the balance of an account.

### **Parameters**

An object with a property:

* address: `String` - address of the account to get the balance of.

### Returns

`Number` - The balance.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getBalance",  
  "params":{"address":"0xc94770007dda54cF92009BFF0dE90c06F603a09f"}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":98347  
}`

## ain\_getConsensusStakeAmount

Returns the amount of AIN the account \(node\) is staking for participating in the consensus protocol.

### **Parameters**

An object with a property:

* address: `String` - address of the account.

### Returns

`Number` - The amount at stake.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getConsensusStakeAmount",  
  "params":{"address":"0xc94770007dda54cF92009BFF0dE90c06F603a09f"}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":1000  
}`

## ain\_getNonce

Returns the nonce \(= number of transactions an address has sent\) of an address.

### **Parameters**

An object with a property:

* address: `String` - address of the account to get the transaction count of

### Returns

`Number` - The nonce.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getNonce",  
  "params":{"address":"0xc94770007dda54cF92009BFF0dE90c06F603a09f"}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":10  
}`

## ain\_isValidator

Returns whether the node is currently a validator or not.

### **Parameters**

An object with a property:

* address: `String` - address of the account to check if it's currently in the validator set

### Returns

`Boolean` - Whether the node is a validator or not.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_isValidator",  
  "params":{"address":"0xc94770007dda54cF92009BFF0dE90c06F603a09f"}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":true  
}`

