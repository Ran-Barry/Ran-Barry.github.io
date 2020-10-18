---
title: solidity简单语法
date: 2020-09-08 16:15:57
tags:
---


1Ether = 10^3 Finney = 10^6 Szabo = 10^18 Wei

<!--more-->

## fallback

* 没有定义fallback function,在收到ether时，会触发exception并且退回ether。
* contract想收ether必须定义fallback function，且要加上payable modifier来宣告function可以收取。

代码举例

```sol
pragma solidity ^0.4.25;

contract FallbackExample{
    event LogFallback(string message);
    event LogBalance(uint alance);
    
    function() public payable{
        emit LogFallback("Fallback");
        emit LogBalance(address(this).balance);
    }
}
```

## address type

### 格式

```sol
<address>.send(uint256 amount)
```

* 对address送出amount Wei
* 本function会forward 2300 gas 作为呼叫的 gas
  * 因为 send 将会出发address中的fallback function
* 当send失败，将回传 false 。否则回传 true 。

### 格式

```sol
<address>.transfer(uint256 amount)

* 对address送出 amount Wei
* 本 function 会 forward 2300 gas 作为呼叫的 gas
  * 因为 transfer 将会出发 address 中的 fallback function
* 当执行失败，将 throw exception 。

### Transfer V.S. Send

* Transfer 保证了转移 Ether 的正确性，因为失败的实侯会让整个transaction 收到 throw 而终止
* Send 在执行失败只会回传 false, 因此在使用 Send 时，应该每次都检查他的回传值。比如搭配 require()

代码举例

```sol
pragma solidity ^0.4.25;

contract Address{
    function() public payable {}
    function Balance() public view returns (uint256){
        return address(this).balance;
    }
    function Transfer(uint256 amount) public returns (bool){
        msg.sender.transfer(amount * 1 ether);
        return true;
    }
    function SendWithoutCheck(uint256 amount) public returns (bool){
        msg.sender.send(amount * 1 ether);
        return true;
    }
    function SendWithCheck(uint256 amount) public returns (bool){
        require(msg.sender.send(amount * 1 ether),"Send failed");
        return true;
    }
}
```

## Mapping

### 格式

mapping (T1 => T2) var;

* 提供 Key -> Value 的资料结构
* T1 可以是除了 mapping 以外的所有 type，因为实际存储的时候，T1 原本的数据并不会被存储下来，只会留下 keccake256(T1) 作为 index。
* T2 可以是任何 type

代码实例

```sol
pragma solidity ^0.4.25;

contract Donation {
    mapping(address => uint) public ledger;
    mapping(address => bool) public donors;
    address[] public donorList;
    
    function isDonor(address pAddr) internal view returns(bool){
        return donors[pAddr];
    }
    
    function donate() public payable{
        if(msg.value >= 1 ether){
            if(!isDonor(msg.sender)){
                donors[msg.sender] = true;
                donorList.push(msg.sender);
            }
            
            ledger[msg.sender] += msg.value;
        } else {
            revert("< 1 ether");
        }
    }
}
```

## struct

格式

```sol
struct Name{
    T var;
    ...
}
```

代码示例

```sol
pragma solidity ^0.4.25;

contract Class{
    struct Student{
        string name;
        uint score;
        bool active;
    }
    mapping(uint => Student) students;
    
    modifier ActiveStudent(uint id){
        require(students[id].active,"Student is inactive");
        _;
    }
    
    function register(uint id,string name) public{
        students[id] = Student({name:name,score:0,active:true});
    }
    
    function modifyScore(uint id,uint score) public ActiveStudent(id){
        students[id].score = score;
    }
    
    function getStudent(uint id) public ActiveStudent(id) view returns (string,uint){
        return (students[id].name,students[id].score);
    }
}
```

## 实况捐赠合约实例

```sol
pragma solidity ^0.4.25;

contract Donation{
    
    struct DonorInfo{
        address[] donors;
        mapping (address => uint) ledger;
    }
    mapping (address => DonorInfo) DonationHistory;
    
    event LogDonate(address streamer,address donor, string nickname,uint value,string message);
    
    function donate(address _streamer,string _nickname,string _message) public payable{
        require(msg.value > 0);
        
        _streamer.transfer(msg.value);
        
        if(DonationHistory[_streamer].ledger[msg.sender] == 0)
        {
            DonationHistory[_streamer].donors.push(msg.sender);
        }
        
        DonationHistory[_streamer].ledger[msg.sender] += msg.value;
        
        
        emit LogDonate(_streamer,msg.sender,_nickname,msg.value,_message);
    }
    
    function getDonorList() public view returns(address[]){
        return DonationHistory[msg.sender].donors;
    }
    
    event LogListDonorInfo(address streamer,address user,uint value);
    
    function listDonorInfo() public{
        for(uint i = 0;i < DonationHistory[msg.sender].donors.length;i++){
            address user = DonationHistory[msg.sender].donors[i];
            emit LogListDonorInfo(msg.sender,user,DonationHistory[msg.sender].ledger[user]);
        }
    }
}
```

## Abstract

代码实例

```sol
pragma solidity ^0.4.25;

contract Ownable{
    address private owner;
    construcotr() internal {
        owner = msg.sender;
    }
    modifier onlyOwner(){
        require(isOwner());
        _;
    }
    
    function isOwner() public view returns (bool){
        return owner == msg.sender;
    }
}

contract Main is Ownable{
    string public name = "";
    function modifyName(string _name) public onlyOwner{
        name = _name;
    }
}
```

## Interface

* 只能定义function
* 不能继承其他contracts & interfaces
* 不能定义 constructor、变数、struct、enum

代码实例

```sol
pragma solidity ^0.4.25;

interface Animal {
    function run(uint speed) external returns (uint);
}

contract Cat is Animal{
    function run(uint speed) public returns (uint distance){
        return speed * speed;
    }
}

contract Dog is Animal{
    function run(uint speed) public returns(uint distance){
        return speed * 10;
    }
}
```

## library

格式：library lib{}

* 希望能只被部署一次且在一个指定的位置，但能被多个地方所使用
* 没有state variables
* 不能继承他人，也不能被继承
* 无法接受Ether

代码实例

```sol
pragma solidity ^0.4.25;

library Set{
    struct Data{
        mapping(int => bool) data;
    }
    function Insert(Data storage d,int key) public returns (bool){
        if(d.data[key])
            return false;//Key exists
        d.data[key] = true;
        return true;
    }
    function Remove(Data storage d,int key) public returns (bool){
        if(!d.data[key])
            return false;//Key does not exists
        d.data[key] = false;
        return true;
    }
    function Contain(Data storage d,int key) public view returns (bool) {
        return d.data[key];
    }
}

contract Main{
    Set.Data set;
    function insert(int key) public returns (bool) {
        return Set.Insert(set,key);
    }
    function remove(int key) public returns (bool) {
        return Set.Remove(set,key);
    }
    function contain(int key) public view returns (bool) {
        return Set.Contain(set,key);
    }
}
```

## SafeMath

代码实例

```sol
pragma solidity ^0.4.25;

library SafeMath{
    function mul(uint256 a,uint256 b) internal pure returns (uint256) {
        uint256 c = a * b;
        require( c / a == b);
        return c;
    }
    function div(uint256 a,uint256 b) internal pure returns (uint256) {
        require(b > 0); // solidity only automatically asserts when dividing by 0
        uint256 c = a / b;
        return c;
    }
    function sub(uint256 a,uint256 b) internal pure returns (uint256) {
        require(b <= a); // underflow
        uint256 c = a - b;
        return c;
    }
    function add(uint256 a,uint256 b) internal pure returns (uint256) {
        uint256 c = a + b;
        require(c >= a); // overflow
        return c;
    }
    function mod(uint256 a,uint256 b) internal pure returns (uint256) {
        require(b != 0);
        return a % b;
    }
}
contract Main{
    function test() public pure returns (uint256){
        uint256 a = 300;
        uint256 b = 10;
        return SafeMath.add(a,b);
    }
}
```

## Import & using

格式：import "a.sol";
格式：using lib for type;

代码实例

```sol
pragma solidity ^0.4.25;

import "browser/library & set.sol";

contract Main{
    using Set for Set.Data;
    
    Set.Data myset;
    
    function insert(int key) public returns (bool) {
        return mySet.Insert(key);
    }
    function remove(int key) public returns (bool) {
        return mySet.Remove(key);
    }
    function contain(int key) public view returns (bool) {
        return mySet.Contain(key);
    }
}
```

## IERC20 interface

代码实例

```sol
pragma solidity ^0.4.25;

interface IERC20 {
    // suo'you所有cun'zai所有存在的 Token 数量
    function totalSupply() external view returns (uint256);
    
    // 读取 tokenOwner 这个 address 所持有的 Token 数量
    function balanceOf(address tokenOwner) external view returns (uint256 balance);
    
    // 从 msg.sender 传 tokens 个 Token 给 to 这个 address
    function transfer(address to,uint256 tokens) external returns (bool success);
    
    // 得到 tokenOwner 授权给 spender 使用的 Token 剩余数量
    function allowance(address tokenOwner,address spender) external view returns (uint256 remaining);

    // msg.sender 授权给 spender 可使用自己的 tokens 个 Token
    function approve(address spender,uint256 tokens) external returns (bool success);

    // 将 tokens 个 Token 从 from 转到 to
    function transferFrom(address from,address to,uint256 tokens) external returns (bool success);

    event Transfer(
        address indexed from,
        address indexed to,
        uint256 tokens
    );

    event Approval(
        address indexed owner,
        address indexed spender,
        uint256 tokens
    );
}
```
