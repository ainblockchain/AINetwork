# Operations

Blockchain state can be accessed using state access operations. There are two types of operations, _read operation_ and _write operation_, and they are again classified into two categories: _simple operation_ and _composite operation_. Simple operations are those that have only one access reference point \(i.e., data path in the blockchain database\), while composite operations have multiple access reference points.

## Read Operations

There is no permission required for read operations.

### Simple Operations

| Target | Operator | Parameters | Action |
| :--- | :--- | :--- | :--- |
| value | GET\_VALUE | ref | Get the value on the path reference |
| rule | GET\_RULE | ref | Get the rule config on the path reference |
| owner | GET\_OWNER | ref | Get the owner config on the path reference |
| function | GET\_FUNC | ref | Get a triggering function hash on the path reference |
| rule | EVAL\_RULE | ref, address, value, timestamp | Evaluate the rule config on the path reference |
| owner | EVAL\_OWNER | ref, address | Evaluate the owner config on the path reference |

### Composite Operations

| Target | Operator | Parameters | Action | Rule requirements |
| :--- | :--- | :--- | :--- | :--- |
| value, rule, owner, or function | GET | op\_list \(list of get operations\)  | Get multiple path-value, path-rule, path-owner, or path-function pairs | Write permission on **all** the paths |

## Write Operations

Each write operation has permission requirements depending on its type and path reference.

### Simple Operations

| Target | Operator | Parameters | Action | Required Permission |
| :--- | :--- | :--- | :--- | :--- |
| value | SET\_VALUE | ref, value | Set the value on the path reference | Value write permission on the path |
| value | INC\_VALUE | ref, value | Increment the value on the path reference by delta | Value write permission on the path |
| value | DEC\_VALUE | ref, value | Decrement the value on the path reference by delta | Value write permission on the path |
| rule | SET\_RULE | ref, rule | Set the rule on the path reference | Rule write permission on the path |
| owner | SET\_OWNER | ref, owner | Set the owner on the path reference | Owner write permission on the path |
| function | SET\_FUNC | ref, funcHash | Set a triggering function on the path reference | Function write permission on the path |

### Composite Operations

There are two composite write operations, SET and BATCH:

| Target | Operator | Parameters | Action | Rule requirements |
| :--- | :--- | :--- | :--- | :--- |
| value, rule, owner, or function  | SET | op\_list \(an array of operations\) | Set multiple path-value, path-rule, path-owner, or path-function pairs | Write permission on **all** the paths |
| value, rule, owner, or function | BATCH | tx\_list \(an array of transactions\) | Handle each transaction independently | Write permission on the paths of each transaction |

The SET and BATCH operations can be compared as follows:

| Comparison | SET Operation | BATCH Operation |
| :--- | :--- | :--- |
| structure | Has multiple operations in op\_list | Has multiple transactions in tx\_list |
| atomicity | The whole operation fails if one of the operation in op\_list fails | The transactions in tx\_list are executed independently, i.e., failure of one transaction does not affect other transactions |
| order | Broadcasted in a bundle and executed in the given order | Broadcasted in a bundle and executed in the given order |



