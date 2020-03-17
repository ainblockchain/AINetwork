# Structure

Below is the structure of a transaction on AIN blockchain. It largely contains 2 types of data: input from the creator and derived information.

Input from the transaction creator are:

* **nonce:** A numeric value added by the transaction creator to get a unique transaction hash. It  strictly numbers transactions to distinguish and order them. Negative nonce value means it's not a strictly ordered nonce, i.e.,  -1 means loosely ordered nonce and -2 means unordered nonce.
* **timestamp:** The unix time of transaction creation. Used only in transactions that are not strictly numbered with nonces.
* **operation:** Specifies actual state-updating request. operation can be either:
  * a single-operation with:
    * **type:** type of operation \("SET\_VALUE" \| "INC\_VALUE" \| "DEC\_VALUE" \| "SET\_RULE" \| "SET\_OWNER" \| "SET\_FUNC"\) ****
    * **ref:** path in the state tree to the value/rule/function hash
    * **value:** new value/rule/function hash to be set
  * a multi-operation with:
    * **type** = "SET"
    * **op\_list:** List of single operations.
      * \[ {type, ref, value}, {type, ref, value}, ..., {type, ref, value} \]
* **parent\_tx\_hash:** Identifier of parent transaction for nested transaction.

Derived data:

* **hash:** The hash of the transaction which uniquely identifies the transaction.
* **from:** Public key of the transaction creator.
* **signature:** The signature of the transaction that's used to validate the sender of the transaction. We use ECDSA and secp256k1 constants to define the elliptic curve.

When a transaction is received through a JSON RPC call, it will have 2 params. The first parameter will be the signature of the transaction by the {address}, and the second parameter will be the the transaction data object, which was used for signing. The transaction data object's properties include: nonce or timestamp, operation, and optionally, parent\_tx\_hash. A transaction's hash can be obtained by hashing the serialized the transaction object.

