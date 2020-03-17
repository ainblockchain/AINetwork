# ain.wallet

## wallet

```text
ain.wallet
```

The AIN `Wallet` that can hold multiple accounts. An Account object consists of an address, a private\_key, and a public\_key.

### Example

```text
ain.wallet;
> Wallet {
   accounts: {
      "0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01": {
         address: "0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01",
         private_key: "...",
         public_key: "..."
      },
      "0xF2CD2AA0c7926743B1D4310b2BC984a0a453c3d4": {
         address: "0xF2CD2AA0c7926743B1D4310b2BC984a0a453c3d4",
         private_key: "...",
         public_key: "..."
      }
   },
   create: function(){},
   add: function(){},
   addFromHDWallet: function(){},
   setDefaultAccount: function(){},
   removeDefaultAccount: function(){},
   remove: function(){},
   clear: function(){},
   toV3Keystore: function(){},
   fromV3Keystore: function(){},
   sign: function(){},
   signTransaction: function(){},
   recover: function(){},
   defaultAccount: "0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01",
   length: 2,
}
```

## create

```text
ain.wallet.create(numberOfAccounts)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| numberOfAccounts | Number | The number of accounts to create. |

### Returns

Newly created `Account` object\(s\).

### Example

```text
ain.wallet.create(3)
.then(accounts => {
    // can access new accounts with accounts[i]
})
```

## add

```text
ain.wallet.add(account)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| account | String \| Object | A private key or an account object. |

### Returns

| Name | Type | Description |
| :--- | :--- | :--- |
| address | String | The address of the added account. |

### Example

```text
ain.wallet.add("0x348ce564d427a3311b6536bbcff9390d69395b06ed6c486954e971d960fe8709");
```

## addFromHDWallet

```text
ain.wallet.addFromHDWallet(seedPhrase, index = 0)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| seedPhrase | String | The seed phrase \(12 or 24 words\) of the wallet. |
| index | number | The index of the account you're trying to add. |

### Returns

| Name | Type | Description |
| :--- | :--- | :--- |
| address | String | The address of the added account. |

### Example

```text
ain.wallet.add("apple banana carrot ...", 1);
```

## remove

```text
ain.wallet.remove(account)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| account | String \| Object | A public key or an account object. |

### Example

```text
ain.wallet.remove("0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01");
```

## clear

Removes accounts added to the wallet and reset defaultAccount to null.

```text
ain.wallet.clear()
```

### Example

```text
ain.wallet.clear();
```

## defaultAccount

```text
ain.wallet.defaultAccount
```

### Returns

| Name | Type | Description |
| :--- | :--- | :--- |
| account | String | The public key of the default account. Default value is `undefined`. |

### Example

```text
console.log(ain.wallet.defaultAccount);

> "0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01"
```

## setDefaultAccount

```text
ain.wallet.setDefaultAccount(address)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| address | String | The address of the account to set as the defaultAccount. The account should already exist in `ain.wallet`. |

### Example

```text
ain.wallet.setDefaultAccount("0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01");
```

## removeDefaultAccount

```text
ain.wallet.removeDefaultAccount()
```

### Example

```text
ain.wallet.removeDefaultAccount();
```

## getBalance

```text
ain.wallet.getBalance([key])
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| key | String | \[Optional, defaults to `ain.wallet.defaultAccount`\] A private key to sign the data with, or an address if the account is loaded to the wallet. |

### Returns

Promise returns a number, which is the AIN balance of the address.

### Example

```text
const balance = await ain.wallet.getBalance("0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01");
```

## sign

```text
ain.wallet.sign(data[, key])
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| data | String | The data to sign. |
| key | String | \[Optional, defaults to `ain.wallet.defaultAccount`\] A private key to sign the data with, or an address if the account is loaded to the wallet. |

### Returns

| Name | Type | Description |
| :--- | :--- | :--- |
| signature | String | The signature of the data. |

### Example

```text
const signature = ain.wallet.sign("This is an important message.", "0x348ce564d427a3311b6536bbcff9390d69395b06ed6c486954e971d960fe8709");
```

## signTransaction

```text
ain.wallet.signTransaction(transaction)
```

### Parameters

transaction is an `Object` with following properties:

| Name | Type | Description |
| :--- | :--- | :--- |
| nonce | Number | Nonce of the transaction sender or the timestamp at which the transaction was created. It can be -1 if the transaction is loosely ordered. |
| timestamp | Number | The unix time at which the transaction was created. |
| operation | Operation \| UpdateOperation | The operation of the transaction. It it's a singular operation, it will have type, ref, value and optionally rule\_type fields. If it's a multi-operation, it will have type field set to "SET", and op\_list field with its value as a list of singular operations. |
| parent\_tx\_hash | String | Hash of parent transaction for nested transaction. `null`when it doesn't have a parent transaction. |

Optional parameter:

| Name | Type | Description |
| :--- | :--- | :--- |
| key | String | \[Optional, defaults to `ain.wallet.defaultAccount`\] A private key to sign the transaction with, or an address if the account is loaded to the wallet. |

### Returns

The signature of the transaction.

### Example

```text
const signature = ain.wallet.signTransaction(
  {
    nonce: 11,
    timestamp: 1569895376000,
    operation: {type: "SET_VALUE", ref: "afan/user/user123/balance", value: 100}
  },
  "0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01"
);
```

## recover

```text
ain.wallet.recover(signature)
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| signature | String | The signature. |

### Returns

| Name | Type | Description |
| :--- | :--- | :--- |
| address | String | The address used to sign. |

### Example

```text
const addr = ain.wallet.recover("0xSIGNATURE");
```

## transfer

```text
ain.wallet.transfer({to, value[, from, nonce]})
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| to | String | The address of the recipient of the transferred AIN. |
| value | Number | The amount of AIN that will be transferred. |
| from | String | \[Optional\] The address of the sender of AIN. The from account should be added to wallet in order to sign the transfer transaction. If the argument is not specified and the defaultAccount is set, the defaultAccount will be used. |
| nonce | Number | \[Optional, defaults to `current_nonce + 1`\] Nonce of the transaction sender or the timestamp at which the transaction was created. It can be -1 if the transaction is not strictly ordered. |

### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
const addr = ain.wallet.transfer("0xabcd...1234", 1000, "0xefgh...5678");
```

