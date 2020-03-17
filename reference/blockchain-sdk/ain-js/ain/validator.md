# Validator

## depositConsensusStake

```text
ain.depositConsensusStake(transactionInput)
```

### Parameters

A transactionInput object with the following properties:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">Amount to stake for participating in the consensus protocol.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Address of the account that is staking. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        account argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.depositConsensusStake({ value: 1000 })
.then(function(res){ ... });
```

## getConsensusStakeAmount

```text
ain.getConsensusStakeAmount([account])
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| account | String \| undefined | \[Optional\] Address of the account to get the staked amount of. Uses the `ain.defaultAccount` property, if not specified. If defaultAccount is not set, sender must specify the account argument. |

### Returns

`Promise` returns `Number`

| Name | Type | Description |
| :--- | :--- | :--- |
| stake | Number | Amount of AIN currency that the account is currently staking. |

### Example

```text
ain.getConsensusStakeAmount('0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01')
.then(console.log);

> 1234.5
```

## withdrawConsensusStake

```text
ain.withdrawConsensusStake(transactionInput)
```

### Parameters

A transactionInput object with the following properties:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">[Optional] Amount of AIN currency to withdraw from the account&apos;s
        current consensus stake. If unspecified, the entire deposit will be withdrawn.</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">Number | undefined</td>
      <td style="text-align:left">
        <p>[Optional] If unspecified, the transaction will be regarded as a nonced
          transaction, and the field will be filled in with the current nonce of
          the transaction creator.
          <br />If nonce is set to -1, the transaction is not strictly ordered, in which
          case the ordering of transaction will be based on the timestamp at the
          time of creating the transaction.</p>
        <p>If nonce is set to a number &gt; -1, the transaction will be executed
          only after all the transactions with nonces up to number - 1 are processed.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Address of the account that is staking. Uses the <code>ain.defaultAccount</code> property,
        if not specified. If defaultAccount is not set, sender must specify the
        account argument.</td>
    </tr>
    <tr>
      <td style="text-align:left">parent_tx_hash</td>
      <td style="text-align:left">String | undefined</td>
      <td style="text-align:left">[Optional] Hash of parent transaction for nested transaction. <code>null</code>when
        it doesn&apos;t have a parent transaction.</td>
    </tr>
  </tbody>
</table>### Returns

`Promise` returns an object with 'result' and 'txHash' fields, or 'code' and 'error\_message'. A result is true if the transaction was executed properly. txHash is the string hash of the transaction sent. 

### Example

```text
ain.withdrawConsensusStake({ value: 99 })
.then(function(res){ ... });
```

