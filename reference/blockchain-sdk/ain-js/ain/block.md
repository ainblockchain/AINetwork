# Block

## getBlock

```text
ain.getBlock(blockHashOrBlockNumber[, returnTransactionObjects])
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| blockHashOrBlockNumber | String \| Number | The block hash or block number. Or the string `"genesis"`, `"latest"` or `"pending"`. |
| returnTransactionObjects | Boolean \| undefined | \[Optional, default `false`\] If `true`, the returned block will contain all transactions as objects, if `false` it will only contains the transaction hashes. |

### Returns

`Promise` returns `Object` - The block object:

| Name | Type | Description |
| :--- | :--- | :--- |
| number | Number | The block number. `null` when its pending block |
| hash | String | Hash of the block. `null` when its pending block. |
| parent\_hash | String | Hash of the parent block. `null` when its pending block. |
| proposer | String | The address of the node who proposed the block. |
| validators | Array | The list of addresses of the nodes who validated the block. |
| size | Number | Integer the size of this block in bytes. |
| timestamp | Number | The unix timestamp for when the block was collated. |
| transactions | Array | Array of transaction objects, or transaction hashes, depending on the `returnTransactionObjects` parameter. |

### Example

```text
ain.getBlock(675, true).then(console.log);> {    "timestamp":1564845946382,    "hash":"7a6c2a5a91ce3731310885eff761f7ee39484...",    "parent_hash":"0xe670ec64341771606e55d6b4ca35a1a6b75...",    "number":675,    "proposer":"0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812",    "validators":[      "0x4e65fda2159562a496f9f3522f89122a3088497a",      "0xd46e8dd67c5d32be8058bb8eb970870f07244567",      "0xb60e8dd61c5d32be8058bb8eb970870f07233155"    ],    "size":163591,    "transactions":[      {        "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",        "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",        "signature":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f3...",        "timestamp":1566736760322,        "parent_tx_hash":"0x88df016429689c079f3b2f6ad39fa052532c56...",        "operation":{ ... }      },      {        "hash":"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99...",        "address":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",        "signature":"0x1ec191ef20b0e9628c4397665977cb...",        "nonce":99,        "operation":{ ... }      },      ...    ]  }
```

## getProposer

```text
ain.getProposer(blockHashOrBlockNumber)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| blockHashOrBlockNumber | String \| Number | The block hash or block number. Or the string `"genesis"`, `"latest"` or `"pending"`. |

### Returns

`Promise` returns `String` 

| Name | Type | Description |
| :--- | :--- | :--- |
| proposer | String | The address of the node who proposed the block. |

### Example

```text
ain.getProposer(675).then(console.log);> "0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812"
```

## getValidators

```text
ain.getValidators(blockHashOrBlockNumber)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| blockHashOrBlockNumber | String \| Number | The block hash or block number. Or the string `"genesis"`, `"latest"` or `"pending"`. |

### Returns

`Promise` returns `Array` 

| Name | Type | Description |
| :--- | :--- | :--- |
| validators | Array | The list of addresses of the nodes who validated the block. |

### Example

```text
ain.getValidators(675).then(console.log);> ["0x04aac78e17374fd075d1f11bfe95ef7d8e4ed812","0xd46e8dd67c5d32be8058bb8eb970870f07244567","0x4e65fda2159562a496f9f3522f89122a3088497a"]
```



