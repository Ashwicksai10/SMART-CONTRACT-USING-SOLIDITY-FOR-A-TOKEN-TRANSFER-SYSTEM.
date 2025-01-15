pragma solidity ^0.8.0;

contract SimpleToken {

  
    mapping(address => uint256) public balances;

    uint256 public totalSupply;

    constructor(uint256 initialSupply) {
        totalSupply = initialSupply;
        balances[msg.sender] = initialSupply; // Allocate initial supply to deployer
    }

    
    function transfer(address recipient, uint256 amount) public returns (bool) {
        require(balances[msg.sender] >= amount, "Insufficient balance");
        balances[msg.sender] -= amount;
        balances[recipient] += amount;
        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

   
    event Transfer(address indexed from, address indexed to, uint256 value);
}
