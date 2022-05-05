# Token Contract 
https://etherscan.io/token/0xc770eefad204b5180df6a14ee197d99d808ee52d 
# Protocol
https://shapeshift.com
https://docs.shapeshift.com/

# Repo
https://github.com/shapeshift/fox-token

# Audit 
https://github.com/shapeshift/fox-token/blob/master/ShapeShift%20Fox%20Token%20-%20BlockchainLabs%20Audit%20Report.pdf


## Check FOX

### Check functions
[✓] totalSupply() is present
        [✓] totalSupply() -> (uint256) (correct return type)
        [✓] totalSupply() is view
[✓] balanceOf(address) is present
        [✓] balanceOf(address) -> (uint256) (correct return type)
        [✓] balanceOf(address) is view
[✓] transfer(address,uint256) is present
        [✓] transfer(address,uint256) -> (bool) (correct return type)
        [✓] Transfer(address,address,uint256) is emitted
[✓] transferFrom(address,address,uint256) is present
        [✓] transferFrom(address,address,uint256) -> (bool) (correct return type)
        [✓] Transfer(address,address,uint256) is emitted
[✓] approve(address,uint256) is present
        [✓] approve(address,uint256) -> (bool) (correct return type)
        [✓] Approval(address,address,uint256) is emitted
[✓] allowance(address,address) is present
        [✓] allowance(address,address) -> (uint256) (correct return type)
        [✓] allowance(address,address) is view
[✓] name() is present
        [✓] name() -> (string) (correct return type)
        [✓] name() is view
[✓] symbol() is present
        [✓] symbol() -> (string) (correct return type)
        [✓] symbol() is view
[✓] decimals() is present
        [✓] decimals() -> (uint8) (correct return type)
        [✓] decimals() is view

### Check events
[✓] Transfer(address,address,uint256) is present
        [✓] parameter 0 is indexed
        [✓] parameter 1 is indexed
[✓] Approval(address,address,uint256) is present
        [✓] parameter 0 is indexed
        [✓] parameter 1 is indexed


        [✓] FOX has increaseAllowance(address,uint256)

### Human-summary 

Number of lines: 371 (+ 0 in dependencies, + 0 in tests)
Number of assembly lines: 0
Number of contracts: 8 (+ 0 in dependencies, + 0 tests) 

Number of optimization issues: 10
Number of informational issues: 9
Number of low issues: 1
Number of medium issues: 0
Number of high issues: 0

ERCs: ERC20

+----------+-------------+-------+--------------------+--------------+----------+
|   Name   | # functions |  ERCS |     ERC20 info     | Complex code | Features |
+----------+-------------+-------+--------------------+--------------+----------+
| SafeMath |      5      |       |                    |      No      |          |
|  Roles   |      3      |       |                    |      No      |          |
|   FOX    |      30     | ERC20 |     ∞ Minting      |      No      |          |
|          |             |       | Approve Race Cond. |              |          |
|          |             |       |                    |              |          |
+----------+-------------+-------+--------------------+--------------+----------+


### Contract Summary

+ Contract IERC20
  - From IERC20
    - allowance(address,address) (external)
    - approve(address,uint256) (external)
    - balanceOf(address) (external)
    - totalSupply() (external)
    - transfer(address,uint256) (external)
    - transferFrom(address,address,uint256) (external)

+ Contract SafeMath (Most derived contract)
  - From SafeMath
    - add(uint256,uint256) (internal)
    - div(uint256,uint256) (internal)
    - mod(uint256,uint256) (internal)
    - mul(uint256,uint256) (internal)
    - sub(uint256,uint256) (internal)

+ Contract Roles (Most derived contract)
  - From Roles
    - add(Roles.Role,address) (internal)
    - has(Roles.Role,address) (internal)
    - remove(Roles.Role,address) (internal)

+ Contract ERC20
  - From ERC20
    - _burn(address,uint256) (internal)
    - _burnFrom(address,uint256) (internal)
    - _mint(address,uint256) (internal)
    - _transfer(address,address,uint256) (internal)
    - allowance(address,address) (public)
    - approve(address,uint256) (public)
    - balanceOf(address) (public)
    - decreaseAllowance(address,uint256) (public)
    - increaseAllowance(address,uint256) (public)
    - totalSupply() (public)
    - transfer(address,uint256) (public)
    - transferFrom(address,address,uint256) (public)

+ Contract MinterRole
  - From MinterRole
    - _addMinter(address) (internal)
    - _removeMinter(address) (internal)
    - addMinter(address) (public)
    - constructor() (internal)
    - isMinter(address) (public)
    - renounceMinter() (public)

+ Contract ERC20Mintable
  - From MinterRole
    - _addMinter(address) (internal)
    - _removeMinter(address) (internal)
    - addMinter(address) (public)
    - constructor() (internal)
    - isMinter(address) (public)
    - renounceMinter() (public)
  - From ERC20
    - _burn(address,uint256) (internal)
    - _burnFrom(address,uint256) (internal)
    - _mint(address,uint256) (internal)
    - _transfer(address,address,uint256) (internal)
    - allowance(address,address) (public)
    - approve(address,uint256) (public)
    - balanceOf(address) (public)
    - decreaseAllowance(address,uint256) (public)
    - increaseAllowance(address,uint256) (public)
    - totalSupply() (public)
    - transfer(address,uint256) (public)
    - transferFrom(address,address,uint256) (public)
  - From ERC20Mintable
    - mint(address,uint256) (public)

+ Contract ERC20Capped
  - From ERC20Mintable
    - mint(address,uint256) (public)
  - From MinterRole
    - _addMinter(address) (internal)
    - _removeMinter(address) (internal)
    - addMinter(address) (public)
    - constructor() (internal)
    - isMinter(address) (public)
    - renounceMinter() (public)
  - From ERC20
    - _burn(address,uint256) (internal)
    - _burnFrom(address,uint256) (internal)
    - _transfer(address,address,uint256) (internal)
    - allowance(address,address) (public)
    - approve(address,uint256) (public)
    - balanceOf(address) (public)
    - decreaseAllowance(address,uint256) (public)
    - increaseAllowance(address,uint256) (public)
    - totalSupply() (public)
    - transfer(address,uint256) (public)
    - transferFrom(address,address,uint256) (public)
  - From ERC20Capped
    - _mint(address,uint256) (internal)
    - cap() (public)
    - constructor(uint256) (public)

+ Contract FOX (Most derived contract)
  - From ERC20Capped
    - _mint(address,uint256) (internal)
    - cap() (public)
    - constructor(uint256) (public)
  - From ERC20Mintable
    - mint(address,uint256) (public)
  - From MinterRole
    - _addMinter(address) (internal)
    - _removeMinter(address) (internal)
    - addMinter(address) (public)
    - isMinter(address) (public)
    - renounceMinter() (public)
  - From ERC20
    - _burn(address,uint256) (internal)
    - _burnFrom(address,uint256) (internal)
    - _transfer(address,address,uint256) (internal)
    - allowance(address,address) (public)
    - approve(address,uint256) (public)
    - balanceOf(address) (public)
    - decreaseAllowance(address,uint256) (public)
    - increaseAllowance(address,uint256) (public)
    - totalSupply() (public)
    - transfer(address,uint256) (public)
    - transferFrom(address,address,uint256) (public)
  - From FOX
    - constructor() (public)

