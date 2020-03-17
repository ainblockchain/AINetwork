# Blockchain Database

Ethereum is a global singleton state machine, transactions trigger a change of state or cause a contract to execute in the EVM. The contract execution part is the heavy part which requires both virtual machine and storage structure. The smart contract transaction can be divided into three functionalities: changing state, defining rules for changing state, and defining actions when changing state. While Ethereum handles all three functionalities through blockchain transactions, AIN network aims to provide this functionality through states, rules, and triggers.

Transactions in AI Network trigger a change of state or defines the rules for changing state. The difference is it does not contain the code and the node does not need extra storage or memory for running the code on-chain. Rules are a small amount of the expression to dictate which transactions are valid and accepted for the specified subset of the state. In this regard, rules provide integrity to data written to the blockchain, ensuring invalid transactions are not allowed. Finally, triggers are off-chain workers which may generate additional transactions in response to transactions that have already been processed by the blockchain.

AI Network's state manipulation module is often refer to as _blockchain database_ as it's very similar to traditional NOSQL database in the ways they read and write data.

