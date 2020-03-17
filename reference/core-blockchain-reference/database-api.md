# Database API

## ain\_getValue

Returns the value at the given path in the global state tree.

### **Parameters**

An object with a "ref" property.

### Returns

`Object` \| `String` \| `Number` \| `Array` \| `Boolean` \| `null` - The data at the path.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getValue",   
  "params":{"ref":"/path/to/some/values"}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    "username":"user123",  
    "email":"email@ainetwork.ai",  
    "createdAt":"123456789"  
  }  
}`

## ain\_getRule

Returns the rule at the given path in the global state tree.

### **Parameters**

An object with a "ref" property.

### Returns

`String` - The rule or function hash at the path.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_get",   
  "params":{"ref":"/path/to/some/rules"}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    ".write": true  
  }  
}`

## ain\_getFunc

Returns the hash of the function at the given path in the global state tree.

### **Parameters**

An object with a "ref" property.

### Returns

`String` - The rule or function hash at the path.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_get",   
  "params":{"ref":"path/to/some/function/"}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    ".func": "0xabcd...1234"  
  }  
}`

## ain\_getOwner

Returns the value, rule or function \(TBD\) at the given path in the global state tree.

### **Parameters**

An object with a "ref" property.

### Returns

`Object` - An object containing an "inherit" property, which is an array of path strings that the ref inherits owner configs from, as well as "owners" property that consists of owner objects – each with the address of an owner as a key and the permissions given to the owner as an object mapped to the key.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_getOwner",   
  "params":{"ref":"path/to/some/value/"}  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":{  
    ".owner":{  
      "inherit":[],  
      "owners":{  
        "*":{"write_owner":fasle,"write_rule":false,"branch_owner":true},  
        "0xabcd...1234":{"write_owner":fasle,"write_rule":true,"branch_owner":true}  
      }  
    }  
  }  
}`

## ain\_get

Returns the value, rule or function \(TBD\) at the given path in the global state tree.

### **Parameters**

An object with a property "op\_list" which maps to a non-empty list of get operations. Each get operation is an object with type and ref properties. A type can take one of the following string values: "GET\_VALUE", "GET\_RULE", "GET\_OWNER" and "GET\_FUNC".

### Returns

Array of data/rule/owner data/function hash at each path. The order will be preserved, and if there isn't data present at the path, `null` will be at the path's index.

### **Example**

`// Request  
curl -X POST --data  
'{  
  "jsonrpc":"2.0",  
  "id":1,   
  "method":"ain_get",   
  "params":{  
    "op_list": [  
      {"ref": "afan/user123/balance","type": "GET_VALUE"},  
      {"ref": "afan/$userId","type": "GET_RULE"}  
    ]  
  }  
}'  
  
// Response  
{   
  "jsonrpc":"2.0",   
  "id":1,  
  "result":[1000, "'$userId' === auth"]  
}`

