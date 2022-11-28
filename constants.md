## Constants and Immutable State Variables

State variables in a contract can be declared as `constant` or `immutable`. In these cases value can not be modified after the contract has been constructed. The compiler does not reserve a storage slot for these variables, every occurence is replaced by the respective value.

Compared to regular state variables, the gas costs of constant and immutable variables are much lower.

Example:

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.4;

uint constant X = 32**22 + 8;

contract C {
    string constant TEXT = "abc";
    bytes32 constant MY_HASH = keccak256("abc");
    uint immutable decimals;
    uint immutable maxBalance;
    address immutable owner = msg.sender;

    constructor(uint decimals_, address ref) {
        decimals = decimals_;
        // Assignments to immutables can even access the environment.
        maxBalance = ref.balance;
    }

    function isBalanceTooHigh(address other) public view returns (bool) {
        return other.balance > maxBalance;
    }
}
```

### Constant

For `constant` variables the value has to be fixed at compile time. It is also possible to define `constant` variables at file level. Only `strings` and `value types` can be used as constants.

For a constant variable the expression assigned to it is copied to all the places where it is accessed and also re-evaluated each time.

### Immutable

`immutable` variables can be assigned once at construction time. They are bit less restrictive than those declared as `constant`. Immutable variables can be assigned any arbitrary value in the constructor of the contract or at the point of their declaration. They can be assigned only once.
