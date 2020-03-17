# ain.db

## Reference

```text
ain.db.Reference
```

Class that creates a reference to a path in the AIN Database.

## ref

```text
ain.db.ref(path)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| path | String | The path to get a `Reference` of. |

### Returns

| Name | Type | Description |
| :--- | :--- | :--- |
| reference | Reference | An instance of `Reference` at the path. |

### Example

```text
const ref = ain.db.ref('afan_app/users/user123/uid');
```

## Reference.getFunction

```text
ain.db.ref('path/to/something').getFunction(path)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| path | String \| undefined | \[Optional\] A relative path to the location of child data. |

### Returns

`Promise` returns data.

| Name | Type | Description |
| :--- | :--- | :--- |
| data | Object \| null | The function config at the path. |

### Example

```text
ain.db.ref('afan_app/users/user123').getFunction()
.then(console.log);

> {
    registry_service: "functions.ainetwork.ai",
    event_listener: "events.ainetwork.ai",
    function_hash: '0xFUNCTION_HASH'    
  }
```

## Reference.getOwner

```text
ain.db.ref('path/to/something').getOwner(path)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| path | String \| undefined | \[Optional\] A relative path to the location of child data. |

### Returns

`Promise` returns data.

| Name | Type | Description |
| :--- | :--- | :--- |
| data | Object \| null | The owner rules at the path. |

### Example

```text
ain.db.ref('afan_app/users/user123').getOwner()
.then(console.log);

> {
    .owner: {
      inherit: [
        "/afan_app",
        "/afan_app/users"
      ],
      owners: {
        "*": {
          write_owner: false,
          write_rule: false,
          branch_owner: false,
        },
        "0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812": {
          write_owner: true,
          write_rule: true,
          branch_owner: true,
        }
      }
    }    
  }
```

## Reference.getRule

```text
ain.db.ref('path/to/something').getRule(path)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| path | String \| undefined | \[Optional\] A relative path to the location of child data. |

### Returns

`Promise` returns write rules at the path.

| Name | Type | Description |
| :--- | :--- | :--- |
| data | String \| null | The value, write rules, owner or function hash at the path. |

### Example

```text
ain.db.ref('/afan_app/users/user123').getRule('/email')
.then(console.log);

> "auth === '0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812'"
```

## Reference.getValue

```text
ain.db.ref('path/to/something').getValue(path)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| path | String \| undefined  | \[Optional\] A relative path to the location of child data. |

### Returns

`Promise` returns data at the path.

| Name | Type | Description |
| :--- | :--- | :--- |
| data | Object \| String \| Number \| Array \| Boolean \| null | The value at the path. |

### Example

```text
ain.db.ref('afan_app/users/user123').getValue()
.then(console.log);

> {
    username: "user123",
    email: "user123@ainetwork.ai",
    ...
   }
```

## Reference.get

```text
ain.db.ref('path/to/something').get(getRequests)
```

### Parameters

getRequests is an array of get requests. Each get request object contains these properties:

| Name | Type | Description |
| :--- | :--- | :--- |
| type | String | A string of value "GET\_VALUE", "GET\_RULE", "GET\_OWNER" or "GET\_FUNC". |
| ref | String \| undefined | A relative path to the location of child data. If left undefined, the get operation will be done on the Reference's path. |

### Returns

`Promise` returns an array of data, preserving the order of the requests.

| Name | Type | Description |
| :--- | :--- | :--- |
| data | Object \| String \| Number \| Array \| Boolean \| null | The value, write rules, owner or function hash at the path. |

### Example

```text
ain.db.ref('afan_app/users/user123').get([
  { type: 'GET_RULE', ref: '' },
  { type: 'GET_VALUE', ref: '' }
])
.then(console.log);

> [
    {
      .write: "auth === '0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812'"
    },
    {
      username: "user123",
      email: "user123@ainetwork.ai",
      ...
    }
  ]
```

## Reference.setFunction

```text
ain.db.ref('path/to/value').setFunction(transactionInput)
```

### Parameters

transactionInput is an object with following properties:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">Number | String | Boolean | Array | Object</td>
      <td style="text-align:left">The value (function config) to be set at the path.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] The address for the sending account. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        address argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.db.ref('path/to/something').setFunction({
    value: {
      registry_service: "functions.ainetwork.ai",
      event_listener: "events.ainetwork.ai",
      function_hash: '0xFUNCTION_HASH'
    },
    nonce: 123
  })
```

## Reference.setOwner

```text
ain.db.ref('path/to/rules').setOwner(transactionInput)
```

### Parameters

transactionInput is an object with following properties:



<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left">The owner rule object to be set at the path.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] The address for the sending account. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        address argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>An owner rule object can have following keys:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">inherit</td>
      <td style="text-align:left">Array</td>
      <td style="text-align:left">
        <p>An array of ancestor paths If it&#x2019;s given, the owners list on the
          specified paths are included in the owners list. Default value: <code>undefined</code>.</p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">owners</td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left">A mapping of owner&apos;s address to the permissions that the owner has.
        Each owner can have three permissions: owner_update, rule_update and branch.
        Each permission&apos;s default value is <code>false</code>.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.db.ref('afan_app/users/user123').setRule({
  value: {
    inherit: ["test/"],
    owners: {
      "*": {
        owner_update: true,
        rule_update: true,
        branch: true
      },
      "0x11F26Fc7b19cB04eeAD03F3d32aeDf5A6e726dA6": {
        owner_update: false,
        rule_update: false,
        branch: true
      }
    }
  },
  address: "0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812"
})
.then(function(result){ ... });
```

## Reference.setRule

```text
ain.db.ref('path/to/rules').setRule(transactionInput)
```

Sets a write rule at the path.

### Parameters

transactionInput is an object with following properties:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">The write rule string to be set at the path.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] The address for the sending account. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        address argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>A rule object can have following keys:

| Name | Type | Description |
| :--- | :--- | :--- |
| .write | String | Javascript snippet that gets evaluated before writing to the location. If the evaluation of the write rule returns true, the transaction creator has the permission to set values at the path. |

### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.db.ref('afan_app/users/user123').setRule({
  value: "auth === '0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812'",
  address: "0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812"
})
.then(function(result){ ... });
```

## Reference.setValue

```text
ain.db.ref('path/to/value').setValue(transactionInput)
```

### Parameters

transactionInput is an object with following properties:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">Number | String | Boolean | Array | Object</td>
      <td style="text-align:left">The value to be set at the path.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] The address for the sending account. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        address argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.db.ref('afan_app/users/user123').setValue({
  value: {"balance": 100},
  nonce: 9,
  address: "0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812"
})
.then(function(result){ ... });
```

## Reference.incrementValue

```text
ain.db.ref('path/to/value').incrementValue(transactionInput)
```

### Parameters

transactionInput object has following properties:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">The value to increase the existing value by.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] The address for the sending account. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        address argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.db.ref('afan_app/users/user123/balance').incrementValue({value: 100})
.then(function(result){ ... });
```

## Reference.decrementValue

```text
ain.db.ref('path/to/value').decrementValue(transactionInput)
```

### Parameters

transactionInput has the following properties:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">The value to decrease the existing value by.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] The address for the sending account. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        address argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.db.ref('afan_app/users/user123/balance').decrementValue({value: 10})
.then(function(result){ ... });
```

## Reference.deleteValue

```text
ain.db.ref('path/to/value').deleteValue(transactionInput)
```

### Parameters

The parameter could be undefined or a transactionInput, which is an object with following properties:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] The address for the sending account. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        address argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.db.ref('afan_app/users/user123').deleteValue()
.then(function(result){ ... });
```

## Reference.set

```text
ain.db.ref().set(transactionInput)
```

### Parameters

transactionInput is an object with following properties:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">op_list</td>
      <td style="text-align:left">Array</td>
      <td style="text-align:left">An array of <code>Operation</code> objects.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] The address for the sending account. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        address argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.db.ref().set({
  op_list: [
    {
      type: "SET_RULE",
      ref: "afan_app/users/user123/balance",
      value: {".admin": "0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812"}
    },
    {
      type: "SET_VALUE",
      ref: "afan_app/users/user123/balance",
      value: 10
    }
  ],
  nonce: 123
})
.then(function(result){ ... });
```

## Reference.evalRule

```text
ain.db.ref('path/to/something').evalRule({ ref, address, value, timestamp })
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| ref | String \| undefined | \[Optional\] A relative path to the location of child data. |
| address | String \| undefined | \[Optional\] The address to be used in evaluation. Uses the `ain.defaultAccount` property, if not specified. If defaultAccount is not set, sender must specify the address argument. |
| value | any | The value to be used in evaluation. |
| timestamp | Number \| undefined | \[Optional\] The timestamp to be used in evaluation. If not specified, it will be set to the time at the evaluation. |

### Returns

`Promise` returns `Boolean`. If true, the given parameters satisfy the write rule; otherwise, it returns false.

### Example

```text
ain.db.ref('afan_app/users/user123').evalRule({ value: "Hello" }) // true or false
```

## Reference.evalOwner

```text
ain.db.ref('path/to/something').evalOwner({ ref, address })
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| ref | String \| undefined | \[Optional\] A relative path to the location of child data. |
| address | String \| undefined | \[Optional\] The address to be used in evaluation. Uses the `ain.defaultAccount` property, if not specified. If defaultAccount is not set, sender must specify the address argument. |

### Returns

`Promise` returns an `Object`. The object contains key-value mappings of owner rules and permissions. If the value for a type of owner rule is false, the address is not authorized for the particular action.

### Example

```text
ain.db.ref('afan_app/users/user123').evalOwner()
.then(console.log);

> {
    "branch_owner": false,
    "write_function": true,
    "write_owner": true,
    "write_rule": false,
  }
```



