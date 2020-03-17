# Transaction

## Definitions

### Transaction Data

Transaction data is an object that can be hashed and signed to be sent to the AIN network. Below is the spec of transaction data. Note that this transaction data spec is a part of the transaction schema in AIN blockchain. In AIN blockchain's blocks, transactions will have additional derived information such as "address", "signature" and "hash".

| Name | Type | Description |
| :--- | :--- | :--- |
| operation | Operation \| SetMultiOperation | The state changing operation\(s\). |
| nonce | Number | If transaction has a nonce field, it's strictly ordered with natural number nonces. Otherwise, the transaction is loosely ordered with a timestamp and its nonce will be -1.  |
| timestamp | Number | The time at which the transaction was created and first sent to the network. |
| parent\_tx\_hash | String \| undefined | \[Optional\] Hash of parent transaction for nested transaction. `null`when it doesn't have a parent transaction. |

### Operations in Transactions

Each transaction can contain one operation type \("SET\_VALUE" \| "INC\_VALUE" \| "DEC\_VALUE" \| "SET\_RULE" \| "SET\_FUNC" \| "SET"\) and more than one Operation objects or one SetMultiOperation object. Each Operation object contains information on which path the operation will be done, what the new value at the path will be, and if it's a change in rules, whether the new rule will extend or override the closest ancestor's rule.

#### Operation

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
      <td style="text-align:left">type</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Can be one of the following: &quot;SET_VALUE&quot;, &quot;INC_VALUE&quot;,
          &quot;DEC_VALUE&quot;, &quot;SET_RULE&quot;, &quot;SET_FUNC&quot;.</p>
        <p>If type is set to &quot;INC_VALUE&quot; or &quot;DEC_VALUE&quot; but the
          existing value at the path is not a <code>Number</code>, the transaction
          will fail.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ref</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">The path in the global state tree to the value, concatenated with slashes
        (/).</td>
    </tr>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">Object | Number | String | Boolean</td>
      <td style="text-align:left">The value, rule or function hash that will be set or incremented by at
        {ref}. If <code>type</code> is &quot;INC_VALUE&quot; or &quot;DEC_VALUE&quot;,
        the type of <code>value</code> should be <code>Number</code>.</td>
    </tr>
  </tbody>
</table>#### SetMultiOperation

| Name | Type | Description |
| :--- | :--- | :--- |
| type | String | "SET" |
| op\_list | Array | An array of `Operation` objects. |

## getTransaction

```text
ain.getTransaction(transactionHash)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| transactionHash | String | Hash of the transaction. |

### Returns

`Promise` returns `Object` - A transaction object with its hash `transactionHash`:

| Name | Type | Description |
| :--- | :--- | :--- |
| hash | String | Hash of the transaction. |
| nonce | Number | The number of transactions made by the sender prior to this one. Will have a value of `-1` if the transaction is not strictly numbered and uses a timestamp instead. |
| timestamp | Number | The unix time in milliseconds when the transaction has been created and sent to the network.  |
| block\_hash | String | Hash of the block where this transaction was in. `null` when it's pending. |
| block\_number | Number | Block number where this transaction was in. `null` when it's pending. |
| index | Number | Integer of the transactions index position in the block. `null`when it's pending. |
| address | String | Address of the sender. |
| operation | Operation \| SetMultiOperation | The operation type and Operation object\(s\) that define what operations will be executed. If it's an `Operation` object, it will have a type field that can be one of "SET\_VALUE", "INC\_VALUE", "DEC\_VALUE", "SET\_RULE" or "SET\_FUNC". Additionally it will have ref and value fields. It it's an `SetMultiOperation`, it will have a type of "SET" and an op\_list field that is an array of `Operation` objects. |
| parent\_tx\_hash | String | Hash of parent transaction for nested transaction. `null`when it doesn't have a parent transaction. |

### Example

```text
ain.getTransaction("0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...")
.then(console.log);

> {
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
```

## sendTransaction

```text
ain.sendTransaction(transactionInput)
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
      <td style="text-align:left">operation</td>
      <td style="text-align:left">Operation | SetMultiOperation</td>
      <td style="text-align:left">The set/increment/decrement operation(s) to be done with this transaction.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional, defaults to &lt;current nonce + 1&gt;] If unspecified, the
          transaction will be regarded as a nonced transaction, and the field will
          be filled in with the current nonce of the transaction creator.
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
        if not specified. If defaultAccount is not set, sender must specify this
        property.</td>
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
ain.sendTransaction({
    operation: {type: "SET_VALUE", ref: "path/to/value", value: 100},
    nonce: 17,
    address: '0x11F26Fc7b19cB04eeAD03F3d32aeDf5A6e726dA6',
    parent_tx_hash: '0xd96c7966aa6e6155af3b0ac69ec180a905958919566e86c88aef12c94d936b5e'
})
.then(function(res){ ... });
```

## sendTransactionBatch

```text
ain.sendTransactionBatch(transactionInputs)
```

### Parameters

transactionInputs is an array containing one or more transactionInput objects with following properties:

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
      <td style="text-align:left">operation</td>
      <td style="text-align:left">Operation | SetMultiOperation</td>
      <td style="text-align:left">The set/increment/decrement operation(s) to be done with this transaction.</td>
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
          only after all the transactions with nonces up to number - 1 are processed.
          Note that the order of the transactions matter, so if a nonced transaction
          is placed before another nonced transaction, it should have a nonce strictly
          less than the one after.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] The address for the sending account. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify this
        property.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns `Array<Object>` that is an array of objects with the result and transaction hashes and/or errors.

### Example

```text
ain.sendTransactionBatch([
  {
    operation: {type: "SET_VALUE", ref: "path/to/value1", value: 100},
    nonce: 17,
    address: '0x11F26Fc7b19cB04eeAD03F3d32aeDf5A6e726dA6',
    parent_tx_hash: '0xd96c7966aa6e6155af3b0ac69ec180a905958919566e86c88aef12c94d936b5e'
  },
  {
    operation: {type: "SET_VALUE", ref: "path/to/value2", value: "test_string"},
    address: '0x11F26Fc7b19cB04eeAD03F3d32aeDf5A6e726dA6',
    nonce: 18
  }
])
.then(function(resultList){ ... });
```

## sendSignedTransaction

```text
ain.sendSignedTransaction(signature, transactionData)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| signature | String | The signature of the transaction. |
| transactionData | Object | The transaction data. When parsed, it should have 1\) an operation property that is an `Operation` or `SetMultiOperation` object, 2\) a nonce or a timestamp and 3\) if applicable, a parent\_tx\_hash. |

### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.sendSignedTransaction(
  '0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca589...',
  {
    nonce: 17,
    operation: {
      type: "SET_VALUE",
      ref: "path/to/value",
      value: 100
    },
    parent_tx_hash: "0xd96c7966aa6e6155af3b0ac69ec180a905958919566e86ce..."
  }
)
.then(function(res){ ... });
```



