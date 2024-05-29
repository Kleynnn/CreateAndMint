# Create and Mint Token
The cappedToken contract is an Ethereum smart contract written in Solidity that implements a capped ERC-20 token. It allows for the creation of tokens with a maximum supply, where the contract owner has the ability to mint new tokens and any token holder can burn their tokens.

## Getting Started
To get started with using this contract, you'll need basic knowledge of Ethereum smart contracts and the Solidity programming language. You'll also need access to an Ethereum development environment, such as Remix or Hardhat, for deploying and interacting with the contract.

### Executing program

To run this program, you can use Remix IDE to perform the required steps. Make sure to save all the codes for it to run smoothly.

```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Capped.sol";

contract cappedToken is ERC20Capped {
    address public owner;

    constructor(uint256 initialSupply, uint256 cap) ERC20("_cappedToken", "CTK") ERC20Capped(cap) {
        owner = msg.sender;
        _mint(owner, initialSupply);
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can perform this action");
        _;
    }

    function mintToken(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    function burnToken(uint256 amount) public {
        _burn(msg.sender, amount);
    }

    function transferToken(address to, uint256 amount) public returns (bool) {
        _transfer(msg.sender, to, amount);
        return true;
    }
}
```

Deploy the cappedToken contract to the Ethereum blockchain using an Ethereum development environment like Remix or Hardhat.

During deployment, provide the initial supply and cap parameters to set the initial token supply and the maximum supply cap.

Once deployed, you can interact with the contract through its functions.
As the contract owner, you can mint new tokens using the mint function by providing the recipient address and the amount of tokens to mint.
Any token holder can burn their tokens using the burn function by specifying the amount of tokens to burn.

The contract owner has exclusive access to certain functions, such as minting new tokens.
The onlyOwner modifier restricts these functions to be called only by the owner's address, ensuring ownership control.

## Authors

Kleyn 

## License

This project is licensed under the MIT License - see the LICENSE.md file for details
