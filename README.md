pragma solidity ^0.8.0;

contract SimpleToken {

    // Mapping to store token balances for each address
    mapping(address => uint256) public balances;

    // Total supply of tokens
    uint256 public totalSupply;

    // Constructor to set initial total supply
    constructor(uint256 initialSupply) {
        totalSupply = initialSupply;
        balances[msg.sender] = initialSupply; // Allocate initial supply to deployer
    }

    // Function to transfer tokens from one address to another 
    function transfer(address recipient, uint256 amount) public returns (bool) {
        require(balances[msg.sender] >= amount, "Insufficient balance");
        balances[msg.sender] -= amount;
        balances[recipient] += amount;
        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

    // Event to log token transfers
    event Transfer(address indexed from, address indexed to, uint256 value);
}
