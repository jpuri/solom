## Scoping

A variable has initial default value whose byte-representation is all zeros.

Scoping in Solidity follows scoping rules of C99:

- variables are visible from the point right after their declaration until the end of smallest block `{}` that contains the declaration.
- variables that are parameters - function parameters, modifier parameters, catch parameters are visible inside the code block that follows
