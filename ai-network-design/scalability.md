# Scalability

An application in AI Network may generate millions of transactions and many of them are not directly related to other applications. If full nodes maintain one giant tree, it can grow very large. AI Network blockchain solves scalability issue by partitioning the global state tree into several sub-tree states.  


There are three areas of scaling: data scaling, computation scaling, and state scaling. While the most of EVM based blockchains have to deal with all three areas and suffers from sharding them, AI Network blockchain can be only concerned with the state sharding because blockchain’s responsibility is limited to state management only. In AI Network blockchain, data and computation are managed off-chain, and computation is triggered by the state change. The state is a tree structure, which can be easily partitioned.

### **Sharding**

A shard in AIN blockchain maintains a subset of the global state tree. Each of the multiple shards is processed on a separate small blockchain instance, thus greatly increasing a blockchain’s total throughput.

Each shard validates a small part of the transaction history. It is known that POW consensus algorithm can’t be used in conjunction with sharding. This is because the computation power required to attack a shard is significantly less than the computing power required to attack the entire blockchain. Thus proof of stake \(PoS\) consensus algorithms are used for each shard, and only designated nodes who is authorized to commit their stakes are allowed to participate in block validation. 

The state tree is partitioned into relevant subtree and transactions for the subtree are recorded in a child block. Once the child blocks are branched out from the parent blocks, the small headers of child blocks have to be recorded on the main chain.

### **Branch and report**

For forking shard chains from the parent chain, a child first records branch transaction into the parent chain. Branch transaction includes the subtree path it wants to be in charge and the rules for reporting block headers as the new chain grows. After the branch transaction included in the parent chain, validators in the child chain are responsible for processing transactions regarding data for subtree state. The branch transaction creates a new genesis block for the child chain which includes the consensus rule for managing the new branch. When the proposer of the child chain broadcast the new block, the proposer generates report transaction for recording the header of the block into the parent chain. The child block can generate one report transaction per block while the parent block can include multiple report transactions from different shards.  
  
****

![](https://lh6.googleusercontent.com/KNpcqWlVnCL7ngxddoyiqyHUWQIjLlCMEkTbvLHybnfoaiYRe0ZcJQejk40hfqKIbXJ1aBVfVJgfzfbwJjzQ0nl8zbk7eBN4aVM_Wcuc1M4Po_B9a2Ctb1cMyfbh6EWv7zL39kg6)

**Fig 1. The diagram shows how the child state is branched from the root chain. After the branch, the child paths are managed by the child chain and only the header hash is recorded in the root state.**  


![](https://lh4.googleusercontent.com/lXPGuT8kcXDEXpJqzKfuC2hfztITU3y6mFm5cBwDR8bXyXM4E1QG0J7JmZcgA_s9MxdoQ36_6kSd-1dBJKPLCp--VNlQfOIuPwLfxzFMbZJAME00im9_qwC8hT-VHM3l3JJQm1dg)

**Fig 2. The diagram shows how multiple children can report to the parent block. The branch can be recursive. For example, child 1-1 is a child of child 1 which is the child of the root.**  


