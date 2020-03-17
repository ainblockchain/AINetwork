# Propagation

The AIN network uses a “flood routing” protocol to ensure that transactions are propagated quickly and efficiently through the network. When validating and propagating transactions, each node in the AIN network acts as a co-equal node in a P2P network. These co-equal nodes form a mesh network, ensuring that all  nodes in the network are connected to each other at all times. When a new node connects to the AIN network, the node will establish a connection to 11 other peers in the AIN network. Connected nodes are referred to as “neighbor nodes”. Each node in the AIN network is responsible for both receiving and propagating transactions to and from each of their neighbors.

Transaction propagation begins from the originating AIN Network node which either created the transaction  or received the transaction from an AIN network client. This originating node must validate the transaction in three steps:

* Check both local transaction pool and the blockchain to make sure the transaction is not a duplicate 
* Verify that the signature contained in the transaction matches the public key of the transaction sender
* Verify nonce to check the transaction is not breaking dependency to other transactions
* Verify that the output of the transaction is valid, as determined by the AIN Network blockchain Rules

If the transaction is deemed valid, the transaction is immediately executed as a write operation to the blockchain-database. the originating node propagates the transaction to its neighbors, who repeat this validation and propagation process until each node in the network has received the transaction.  


