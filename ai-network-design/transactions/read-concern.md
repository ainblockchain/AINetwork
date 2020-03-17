# Read Concern

Transactions may specify read concern to indicate recommended block confirmation for the value to be valid. Even 0 confirmation can be used if the reverted operation does not cause significant flaws. For example, if the user clicked ‘like’ operation, it might be a good idea to update UI for the like count right after the interaction has happened if the broadcasted event can be accepted most of the time. In the worst case scenario, the like count shown in the UI may not be included in the block, but normally, this is not the end of the world.  


![](../../.gitbook/assets/read-concern-fig1.png)

Fig 1. a/e/g is not included in the block state as it is recommended to be read after 1 block confirmation. read\_concern 0 does not guarantee this value will be in the block, but it still can be useful to the application which requires an immediate response.   


If multiple transactions try to modify the same path, only the last one is valid. For example, if tx1 is {a/b: 1} and tx2 is {a/b: 2}, the last value 2 is the one that is valid. This applies to the read\_concern as well. If tx1 is {a/b: 1, read\_concern: 1} and tx2 is {a/b: 2, read\_concern: 2}, a/b path is not recommended to be read until 2 block confirmations.  


