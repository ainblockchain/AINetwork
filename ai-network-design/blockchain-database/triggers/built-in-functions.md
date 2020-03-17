# Built-in Functions

## Built-in Functions

To apply predefined system operations, built-in functions are defined. For example, account value transfer is implemented using transfer built-in function. Each built-in function consists of triggering conditions and a function. The triggering condition is given by a database path pattern and whenever a new value is written on the path patten, the function is called. If the function fails, the transaction triggered the function call also fails.

### Transfer

```text
{
  '/transfer/{from_addr}/{to_addr}/{transfer_id}/value': _transfer(value, context) {
    // Check (the balance of from_addr) >= value
    // Decrement the balance of from_addr by value
    // Increment the balance of to_addr by value
  }
}
```

### Deposit

```text
{
  '/deposit/{service_id}/{addr}/{deposit_id}/value': _deposit(value, context) {
    // Check (the balance of addr) >= value
    // Decrement the balance of addr by value
    // Increment the value of /deposit_accounts/$service_id/$addr by value
    // Set /deposit_accounts/$service_id/$addr/expire_at as
    // transaction's timestamp + service's deposit lockup time, which is
    // configured at /deposit_accounts/$service_id/config/lockup_duration
  }
}
```

### Withdraw

```text
{
  '/withdraw/{service_id}/{addr}/{withdraw_id}/value': _withdraw(value, context) {
    // Check the value at (/deposit_accounts/$service_id/$addr/value) >= value
    // Check (deposit_accounts/$service_id/$addr/expire_at) >= current time
    // Decrement the value of /deposit_accounts/$service_id/$addr by value
    // Increment the balance of addr by value
  }
}
```

