# require, assert and revert

Functions in Solidity:

require: imports and uses external libraries, contracts, or functions.
assert: verifies a condition is true at a specific point in the contract's execution, and reverts if the condition is false.
revert: undoes all changes made by a function call and restores the state of the contract to its previous state.
Examples:

require("path/to/contract.sol");
assert(balance > 0);
revert();
Summary:

require imports external libraries or contracts.
assert verifies conditions and prevents incorrect behavior.
revert undoes changes made by a function call and restores the state of the contract.

## Description

In Solidity, the require, assert, and revert functions are used to ensure the integrity of a smart contract. The require function is used to import external libraries or contracts, allowing you to use their functions and variables within your own contract. The assert function is used to verify that a condition is true at a specific point in the contract's execution, and if the condition is false, the contract will revert and the transaction will be rolled back. The revert function can be used independently to undo all changes made by a function call and restore the state of the contract to what it was before the call.

## Getting Started

### Executing program

*To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.
Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., MyContract.sol). Copy and paste the following code into the file:

```
contract MyContract {
    // Mapping to store the balance of each user
    mapping (address => uint) public balances;

    // Event to emit when a user's balance is updated
    event BalanceUpdated(address indexed user, uint newBalance);

    // Function to deposit funds
    function deposit(uint amount) public {
        // Require that the amount is greater than 0
        require(amount > 0, "Amount must be greater than 0");

        // Get the current balance of the user
        uint currentBalance = balances[msg.sender];

        // Update the balance by adding the deposited amount
        balances[msg.sender] = currentBalance + amount;

        // Emit the BalanceUpdated event
        emit BalanceUpdated(msg.sender, balances[msg.sender]);
    }

    // Function to withdraw funds
    function withdraw(uint amount) public {
        // Require that the user has sufficient balance
        require(balances[msg.sender] >= amount, "Insufficient balance");

        // Get the current balance of the user
        uint currentBalance = balances[msg.sender];

        // Update the balance by subtracting the withdrawn amount
        balances[msg.sender] = currentBalance - amount;

        // Emit the BalanceUpdated event
        emit BalanceUpdated(msg.sender, balances[msg.sender]);
    }

    // Function to check if a user's balance is greater than 0
    function checkBalance() public {
        // Assert that the user's balance is greater than 0
        assert(balances[msg.sender] > 0);

        // If the assertion fails, revert with an error message
        revert("User's balance is 0 or less");
    }
}
```

## Help

Common Issues in Smart Contract Development
```
Missing require statements: Ensure to add require statements for external libraries/contracts.
assert failures: Use require instead of assert for runtime checks.
revert not undoing changes: Call revert at the correct point in the function.
Unhandled exceptions: Use try-catch blocks and revert to undo changes.
Conflicting function names: Use unique function names.
Missing or incorrect ABI encoding: Correctly encode ABI when calling functions.
Incorrect gas calculations: Use tools like Truffle's compile command and specify required gas amount.
Unintended reentrancy: Use payable and transfer functions carefully.
Out-of-gas errors: Test thoroughly and use gas-efficient coding practices.
Debugging issues: Use Solidity debuggers like Truffle's or Remix's.
```
## Authors

Datu Benladin Embag Jr, 
8202138@ntc.edu.ph



## License

This project is licensed under the MIT License - see the LICENSE.md file for details
