## Errors and the Revert Statement

Errors in Solidity provide a convenient and gas efficient way to explainto the user cause of operation failing. They can be defined inside or outside of the contract.

Instance of `error` can only be created using `revert` statement. Using them with `revert statement` causes all the changes in the current call to be reverted and passes the error data back to the caller. Errors are inherited.

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

/// Insufficient balance for transfer. Needed `required` but only
/// `available` available.
/// @param available balance available.
/// @param required requested amount to transfer.
error InsufficientBalance(uint256 available, uint256 required);

contract TestToken {
    mapping(address => uint) balance;
    function transfer(address to, uint256 amount) public {
        if (amount > balance[msg.sender])
            revert InsufficientBalance({
                available: balance[msg.sender],
                required: amount
            });
        balance[msg.sender] -= amount;
        balance[to] += amount;
    }
    // ...
}
```

Data size of `error` is very less and error is not saved on-chain. `require` and `assert` also internally use `Error` and `revert` mechanism.
