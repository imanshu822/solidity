# MyToken Solidity Contract

## Overview

The MyToken contract is a basic implementation of an ERC-20-like token in Solidity. It demonstrates fundamental token operations such as minting (token creation) and burning (token destruction), along with balance management. This contract is suitable for educational purposes and provides a foundational understanding of token management on the Ethereum blockchain.

### Key Features

- **Token Name:** META
- **Token Symbol:** MTA
- **Total Supply:** Tracks the total supply of META tokens in circulation.
- **Balance Management:** Utilizes a mapping to manage token balances for each address.
- **Minting:** Allows for the creation of new tokens, increasing both total supply and the balance of a specified address.
- **Burning:** Enables the destruction of tokens, decreasing both total supply and the balance of a specified address, ensuring that sufficient tokens exist for burning.

## Getting Started

To deploy and interact with the MyToken contract, follow these steps:

### Prerequisites

- Access to an Ethereum development environment (e.g., Remix IDE).
- Basic understanding of Solidity and Ethereum smart contracts.


### Deployment

1. **Open Remix IDE:**
   - Visit [Remix](https://remix.ethereum.org/).

2. **Create a New File:**
   - Click on the "+" icon to create a new file and save it as `MyToken.sol`.

3. **Copy and Paste Code:**
   - Copy the Solidity code provided in `MyToken.sol` from this repository.

4. **Compile the Contract:**
   - Switch to the "Solidity Compiler" tab in Remix.
   - Ensure the compiler version is set to `0.8.18` or another compatible version.
   - Click on "Compile MyToken.sol" to compile the contract.

5. **Deploy the Contract:**
   - Navigate to the "Deploy & Run Transactions" tab.
   - Select the `MyToken` contract from the dropdown menu.
   - Click on "Deploy" to deploy the contract to the Ethereum network.

### Interacting with the Contract

Once deployed, you can interact with the contract using Remix or any other Ethereum development tool:

- **Mint Tokens:**
  - Call the `mint` function, specifying the recipient's address and the amount of tokens to mint.

- **Burn Tokens:**
  - Call the `burn` function, specifying the owner's address and the amount of tokens to burn. The contract ensures that the address has sufficient tokens to burn.

### Example Usage

```solidity
// Example of minting 100 META tokens to a specific address
MyToken myTokenContract = MyToken(<deployed_contract_address>);
myTokenContract.mint(<recipient_address>, 100);

// Example of burning 50 META tokens from a specific address
myTokenContract.burn(<owner_address>, 50);


### Code

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract MyToken {

    // Public variables
    string public tokenName = "META";
    string public tokenAbbrv = "MTA";
    uint public totalSupply = 0;

    // Mapping of address to token balances
    mapping(address => uint) public balances;

    // Mint function
    function mint(address _address, uint _value) public {
        totalSupply += _value;
        balances[_address] += _value;
    }

    // Burn function
    function burn(address _address, uint _value) public {
        require(balances[_address] >= _value, "Insufficient balance to burn");
        totalSupply -= _value;
        balances[_address] -= _value;
    }
}

