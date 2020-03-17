# Block Structure

Structure of a block:

* Block
  * **header**
    * **number:** The number of this block that is incremented by 1 as a new block is created. The genesis block has a block number of 0.
    * **last\_hash:** The hash of the previous block in the blockchain.
    * **last\_votes\_hash**: The hash of the last\_votes \(propose, &gt; 2/3 pre-votes and pre-commits\) from validators that were used to reach consensus on the previous block.
    * **transactions\_hash**: The hash of the list of transactions that are included in the block.
    * **timestamp:** The unix timestamp for when the block was collated.
    * **size:** The size of the block.
    * **proposer:** The node who created and proposed the block.
    * **validators:** List of validators who participated in the consensus process for this block.
    * **reward:** TBD.
  * **hash:** The hash of the block's header.
  * **last\_votes:** List of validators' voting transactions \(propose, pre-votes and pre-commits\) that contributed to reaching consensus on the previous block. In order for a block to be added to the blockchain, it needs more than 2/3 of the signed pre-commit transactions from validators where each vote is weighted in proportion to the voter's stake.
  * **transactions:** List of transactions included in the block.
    * \[{hash, signature, transaction data}, ...\]



