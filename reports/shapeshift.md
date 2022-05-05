# Token Info 
https://etherscan.io/token/0xc770eefad204b5180df6a14ee197d99d808ee52d 
## Protocol
https://shapeshift.com
https://docs.shapeshift.com/

## Repo
https://github.com/shapeshift/fox-token

## Audit 
https://github.com/shapeshift/fox-token/blob/master/ShapeShift%20Fox%20Token%20-%20BlockchainLabs%20Audit%20Report.pdf


# Checklist 
## Market conditions
- [x] **Token must be listed and have pricing data via coingeko**
- [x] **Total MarketCap > $50 million**
- [ ] **Average daily on-chain liquidity over 30 days > $10,000,000**

## General considerations

- [ ] **The contract has a security review.** Avoid interacting with contracts that lack a security review. Check the length of the assessment (aka “level of effort”), the reputation of the security firm, and the number and severity of the findings.
- [ ] **You have contacted the developers.** You may need to alert their team to an incident. Look for appropriate contacts on [blockchain-security-contacts](https://github.com/crytic/blockchain-security-contacts).
- [ ] **They have a security mailing list for critical announcements.** Their team should advise users (like you!) when critical issues are found or when upgrades occur.

## Contract composition

- [ ] **The contract avoids unneeded complexity.** The token should be a simple contract; a token with complex code requires a higher standard of review. Use Slither’s [human-summary printer](https://github.com/crytic/slither/wiki/Printer-documentation#human-summary) to identify complex code.
- [ ] **The contract uses SafeMath.** Contracts that do not use SafeMath require a higher standard of review. Inspect the contract by hand for SafeMath usage.
- [ ] **The contract has only a few non–token-related functions.** Non–token-related functions increase the likelihood of an issue in the contract. Use Slither’s [contract-summary printer](https://github.com/crytic/slither/wiki/Printer-documentation#contract-summary) to broadly review the code used in the contract.
- [ ] **The token only has one address.** Tokens with multiple entry points for balance updates can break internal bookkeeping based on the address (e.g. `balances[token_address][msg.sender]` might not reflect the actual balance).

## Owner privileges

- [ ] **The token is not upgradeable.** Upgradeable contracts might change their rules over time. Use Slither’s [human-summary printer](https://github.com/crytic/slither/wiki/Printer-documentation#contract-summary) to determine if the contract is upgradeable.
- [ ] **The owner has limited minting capabilities.** Malicious or compromised owners can abuse minting capabilities. Use Slither’s [human-summary printer](https://github.com/crytic/slither/wiki/Printer-documentation#contract-summary) to review minting capabilities, and consider manually reviewing the code.
- [ ] **The token is not pausable.** Malicious or compromised owners can trap contracts relying on pausable tokens. Identify pauseable code by hand.
- [ ] **The owner cannot blacklist the contract.** Malicious or compromised owners can trap contracts relying on tokens with a blacklist. Identify blacklisting features by hand.
- [ ] **The team behind the token is known and can be held responsible for abuse.** Contracts with anonymous development teams, or that reside in legal shelters should require a higher standard of review.

## ERC-20 tokens 

### Suggested ERC-20 conformity checks

Slither includes a utility, [slither-check-erc](https://github.com/crytic/slither/wiki/ERC-Conformance), that reviews the conformance of a token to many related ERC standards. Use slither-check-erc to review that:

- [ ] **Transfer and transferFrom return a boolean.** Several tokens do not return a boolean on these functions. As a result, their calls in the contract might fail. 
- [ ] **The name, decimals, and symbol functions are present if used.** These functions are optional in the ERC20 standard and might not be present.
- [ ] **Decimals returns a uint8.** Several tokens incorrectly return a uint256. If this is the case, ensure the value returned is below 255.
- [ ] **The token mitigates the known [ERC20 race condition](https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729).** The ERC20 standard has a known ERC20 race condition that must be mitigated to prevent attackers from stealing tokens.

Slither includes a utility, [slither-prop](https://github.com/crytic/slither/wiki/Property-generation), that generates unit tests and security properties that can discover many common ERC flaws. Use slither-prop to review that:

- [ ] **The contract passes all unit tests and security properties from slither-prop.** Run the generated unit tests, then check the properties with [Echidna](https://github.com/crytic/echidna) and [Manticore](https://manticore.readthedocs.io/en/latest/verifier.html).

### Risks in ERC-20 extensions
Contracts might have different behaviors from their original ERC specification, manually review that:

- [ ] **The token is not an ERC777 token and has no external function call in transfer and transferFrom.** External calls in the transfer functions can lead to reentrancies.
- [ ] **Transfer and transferFrom should not take a fee.** Deflationary tokens can lead to unexpected behavior.
- [ ] **Potential interest earned from the token is taken into account.** Some tokens distribute interest to token holders. This interest might be trapped in the contract if not taken into account.

### Token scarcity

Reviews for issues of token scarcity requires manual review. Check for these conditions:

- [ ] **No user owns most of the supply.** If a few users own most of the tokens, they can influence operations based on the token's repartition.
- [ ] **The total supply is sufficient.** Tokens with a low total supply can be easily manipulated.
- [ ] **The tokens are located in more than a few exchanges.** If all the tokens are in one exchange, a compromise of the exchange can compromise the contract relying on the token.
- [ ] **Users understand the associated risks of large funds or flash loans.** Contracts relying on the token balance must carefully take in consideration attackers with large funds or attacks through flash loans.
- [ ] **The token does not allow flash minting**. Flash minting can lead to substantial swings in the balance and the total supply, which neccessitate strict and comprehensive overflow checks in the operation of the token. 




### Output from checks

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

