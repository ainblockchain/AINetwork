# Predefined Structures

## Reserved Characters in Paths

In data paths, the following characters are reserved:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Characters</th>
      <th style="text-align:left">Purpose</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">/</td>
      <td style="text-align:left">Reserved for path separator</td>
      <td style="text-align:left">/apps/afan/users</td>
    </tr>
    <tr>
      <td style="text-align:left">.</td>
      <td style="text-align:left">Reserved for rule configs and owner configs</td>
      <td style="text-align:left">
        <p>{</p>
        <p>.write: false,</p>
        <p>...</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">*</td>
      <td style="text-align:left">Reserved for owner configs</td>
      <td style="text-align:left">
        <p>{</p>
        <p>&quot;apps&quot;: {
          <br />&quot;.owner&quot;: {
          <br />&quot;owners&quot;: {</p>
        <p>&quot;*&quot;: {</p>
        <p>...</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$</td>
      <td style="text-align:left">Reserved for path variables in rule configs</td>
      <td style="text-align:left">
        <p>{</p>
        <p>transfer: {</p>
        <p>$from: {</p>
        <p>$to: {</p>
        <p>$key: {</p>
        <p>value: {</p>
        <p>.write: ...</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">{, }</td>
      <td style="text-align:left">Reserved for variables in built-in function paths</td>
      <td style="text-align:left">/transfer/{from}/{to}/{key}/value</td>
    </tr>
    <tr>
      <td style="text-align:left">#, [, ], &lt;ASCII control characters 0-31 or 127&gt;</td>
      <td style="text-align:left">Reserved for other purposes in the future</td>
      <td style="text-align:left">-</td>
    </tr>
  </tbody>
</table>## Pre-defined Paths in Database

The following pre-defined paths are used in the blockchain database:

| Path | Purpose |
| :--- | :--- |
| /token/name | Token name |
| /token/symbol | Token symbol |
| /token/total\_supply | Token total supply |
| /accounts/$address/balance | Account balance |
| /accounts/$address/nonce | Account nonce |
| /transfer/$from/$to/$key/value | Transfer  |
| /deposit\_accounts/$service\_id/$address/$account\_id | Deposit accounts |
| /deposit/$service\_id/$address/$deposit\_id | Deposit |
| /withdraw/$service\_id/$address/$withdraw\_id | Withdraw |
| /consensus | Consensus |
| /apps | Applications |

Owner configs and rule configs are stored in separate places in the database.

