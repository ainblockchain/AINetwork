# Network API

## net\_listening

Returns whether the node is listening for network connections.

### Parameters

None.

### Returns

`Boolean` - true is the node is listening for connections; otherwise, false.

### **Example**

`// Request  
curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"net_listening"}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":true  
}`

## net\_nodeInfo

Returns the node's information.

### Parameters

None.

### Returns

`Object` - the object containing node's information.

### **Example**

`// Request  
curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"net_nodeInfo"}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    "name":"comcom_node",  
    "location":"KOR",  
    "version":"1.0.0"  
  }  
}`

## net\_peerCount

Returns the number of peers the node is connected to.

### Parameters

None.

### Returns

`Number` - number of peers.

### **Example**

`// Request  
curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"net_peerCount"}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":7  
}`

## net\_syncing

Returns whether the node is syncing with the network or not.

### Parameters

None.

### Returns

`Boolean` - true if the node is syncing, false otherwise.

### **Example**

`// Request  
curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"net_syncing"}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":true  
}`

## net\_id

Returns the network id.

### Parameters

None.

### Returns

`Number` - the network id.

* 0: main network
* 1: test network

### **Example**

`// Request  
curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"net_id"}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":0  
}`

