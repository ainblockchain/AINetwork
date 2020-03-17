# Rules and Owners

Rule configs are used to determine the validity of transactions before they are executed. Rule configs are also used to control which users are able to make certain types of transactions. Rule values are javascript boolean statements which will be invoked whenever a user tries to write data to the blockchain-database via a transaction. These statements will evaluate to either true or false depending on - the user, the current state of the blockchain database, and the current time - to name just a couple of examples. Common rule config use cases are:

* Enforcing the terms of an agreed contract between peers on the AI Network
* Ensuring automatic payment to relevant peers once the terms of a contract have been fulfilled and all relevant transactions to that contract have been added to the blockchain
* Determining who has permission to build and validate a block at any given height of the blockchain
* Enforcing punishments for validator peers who attempt to compromise the integrity of the blockchain

To control write permissions on rule configs, we use owner configs. Owner configs are also used to control the write permissions on the owner configs themselves.

