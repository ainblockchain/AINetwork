# Nonce

Transactions signed by the same private key \(i.e., with the same address\) are submitted and handled in an order using nonce. Usually, nonce is a non-negative integer value, starting from 0, that stands for the number of transactions accepted to blocks so far. Whenever a transaction is submitted its nonce is check in the following way:

* If the nonce value is equal to \(the number of transactions with the same address in blocks\) + 1, it's accepted
* Otherwise, it's kept in pending mode with a predefined timeout value until the condition met.

We call this type of nonce s_trictly ordered nonce_. This is enough for typical human-generated transactions. For more use cases like machine-generated transactions, we support two more types: _loosely ordered nonce_ and _unordered nonce_.

Transactions with loosely ordered nonce are ordered using timestamp:

* If the timestamp is larger than the last timestamp, it's accepted
* Otherwise, it' rejected

Transactions with unordered nonce is always accepted unless a transaction with the same transaction hash is already in blocks.

Three different types of nonce can be compared as follows:

| Type | Nonce Field | When To Use | Good For | API Version |
| :--- | :--- | :--- | :--- | :--- |
| Strictly ordered | Non-negative integer | Single client | Human-generated txs | 1.0 |
| Loosely ordered | -1 | Multiple clients, transactions are aligned with time | Machine-generated txs with multiple clients | TBD |
| Unordered | -2 | Single or multiple clients, transactions are not aligned with each other. | Machine-generated txs with different generation time and submission time | 1.0 |



