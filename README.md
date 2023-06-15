// SPDX-License-Identifier: UNLICENSED

pragma solidity ^0.8.0;

contract MyToken {
    string public constant name = "web3easy";
    string public constant symbol = "W3E";
    uint8 public constant decimals = 18;
    uint256 public constant MAX_SUPPLY = 1000 * (10 ** uint256(decimals));
    
    mapping(address => uint256) private balances;
    uint256 private tokenTotalSupply;
    
    event Transfer(address indexed from, address indexed to, uint256 value);
    
    constructor() {
        balances[msg.sender] = MAX_SUPPLY;
        tokenTotalSupply = MAX_SUPPLY;
        emit Transfer(address(0), msg.sender, MAX_SUPPLY);
    }
    
    function balanceOf(address _owner) public view returns (uint256) {
        return balances[_owner];
    }
    
    function transfer(address _to, uint256 _value) public returns (bool) {
        require(_to != address(0), "Invalid address");
        require(_value <= balances[msg.sender], "Insufficient balance");
        
        balances[msg.sender] -= _value;
        balances[_to] += _value;
        
        emit Transfer(msg.sender, _to, _value);
        return true;
    }
    
    function TotaltokenSupply() public view returns (uint256) {
        return tokenTotalSupply;
    }
}
