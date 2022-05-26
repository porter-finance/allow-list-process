# Ribbon Checklist

## Links
https://www.coingecko.com/en/coins/ribbon-finance

https://etherscan.io/token/0x6123B0049F904d730dB3C36a31167D9d4121fA6B

https://github.com/ribbon-finance/governance/blob/main/contracts/RibbonToken.sol

# Notes
The ribbon token has three ownership roles, ADMIN_ROLE, MINTER_ROLE, and TRANSFER_ROLE.
At the time of writing - the [Ribbon Multisig](https://gnosis-safe.io/app/eth:0xDAEada3d210D2f45874724BeEa03C7d4BBD41674) has the MINTER_ROLE and the ADMIN_ROLE. This means they can mint more tokens at will, or pause transfers of the Ribbon Tokens. 

<img width="812" alt="CleanShot 2022-05-26 at 11 49 31@2x" src="https://user-images.githubusercontent.com/15036618/170535734-87c81120-0bcf-43f8-924b-8cd1e1c38b2c.png">


# Main Risks 
* Ribbon 4:6 multisig can pause transfers of RBN tokens, preventing bondholders from being able to redeem or convert. 
* Ribbon 4:6 multisig can mint new RBN tokens at will


## Market conditions
- [X] **Token must be listed and have pricing data via coingeko**
- [X] **Total MarketCap > $50 million**
- [X] **Average daily on-chain liquidity over 30 days > $10,000,000**

## General considerations

- [X] **The contract has a security review.** Avoid interacting with contracts that lack a security review. Check the length of the assessment (aka “level of effort”), the reputation of the security firm, and the number and severity of the findings.
- [X] **You have contacted the developers.** You may need to alert their team to an incident. Look for appropriate contacts on [blockchain-security-contacts](https://github.com/crytic/blockchain-security-contacts).
- [X] **They have a security mailing list for critical announcements.** Their team should advise users (like you!) when critical issues are found or when upgrades occur.

## Contract composition

- [X] **The contract avoids unneeded complexity.** The token should be a simple contract; a token with complex code requires a higher standard of review. Use Slither’s [human-summary printer](https://github.com/crytic/slither/wiki/Printer-documentation#human-summary) to identify complex code.
- [X] **The contract uses SafeMath.** Contracts that do not use SafeMath require a higher standard of review. Inspect the contract by hand for SafeMath usage.
- [X] **The contract has only a few non–token-related functions.** Non–token-related functions increase the likelihood of an issue in the contract. Use Slither’s [contract-summary printer](https://github.com/crytic/slither/wiki/Printer-documentation#contract-summary) to broadly review the code used in the contract.
- [X] **The token only has one address.** Tokens with multiple entry points for balance updates can break internal bookkeeping based on the address (e.g. `balances[token_address][msg.sender]` might not reflect the actual balance).

## Owner privileges

- [X] **The token is not upgradeable.** Upgradeable contracts might change their rules over time. Use Slither’s [human-summary printer](https://github.com/crytic/slither/wiki/Printer-documentation#contract-summary) to determine if the contract is upgradeable.
- [ ] **The owner has limited minting capabilities.** Malicious or compromised owners can abuse minting capabilities. Use Slither’s [human-summary printer](https://github.com/crytic/slither/wiki/Printer-documentation#contract-summary) to review minting capabilities, and consider manually reviewing the code.
- [ ] **The token is not pausable.** Malicious or compromised owners can trap contracts relying on pausable tokens. Identify pauseable code by hand.
- [X] **The owner cannot blacklist the contract.** Malicious or compromised owners can trap contracts relying on tokens with a blacklist. Identify blacklisting features by hand.
- [X] **The team behind the token is known and can be held responsible for abuse.** Contracts with anonymous development teams, or that reside in legal shelters should require a higher standard of review.

## ERC-20 tokens 

### Suggested ERC-20 conformity checks

Slither includes a utility, [slither-check-erc](https://github.com/crytic/slither/wiki/ERC-Conformance), that reviews the conformance of a token to many related ERC standards. Use slither-check-erc to review that:

- [X] **Transfer and transferFrom return a boolean.** Several tokens do not return a boolean on these functions. As a result, their calls in the contract might fail. 
- [X] **The name, decimals, and symbol functions are present if used.** These functions are optional in the ERC20 standard and might not be present.
- [X] **Decimals returns a uint8.** Several tokens incorrectly return a uint256. If this is the case, ensure the value returned is below 255.
- [X] **The token mitigates the known [ERC20 race condition](https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729).** The ERC20 standard has a known ERC20 race condition that must be mitigated to prevent attackers from stealing tokens.

Slither includes a utility, [slither-prop](https://github.com/crytic/slither/wiki/Property-generation), that generates unit tests and security properties that can discover many common ERC flaws. Use slither-prop to review that:

- [X] **The contract passes all unit tests and security properties from slither-prop.** Run the generated unit tests, then check the properties with [Echidna](https://github.com/crytic/echidna) and [Manticore](https://manticore.readthedocs.io/en/latest/verifier.html).

### Risks in ERC-20 extensions
Contracts might have different behaviors from their original ERC specification, manually review that:

- [X] **The token is not an ERC777 token and has no external function call in transfer and transferFrom.** External calls in the transfer functions can lead to reentrancies.
- [X] **Transfer and transferFrom should not take a fee.** Deflationary tokens can lead to unexpected behavior.
- [X] **Potential interest earned from the token is taken into account.** Some tokens distribute interest to token holders. This interest might be trapped in the contract if not taken into account.

### Token scarcity

Reviews for issues of token scarcity requires manual review. Check for these conditions:

- [X] **No user owns most of the supply.** If a few users own most of the tokens, they can influence operations based on the token's repartition.
- [X] **The total supply is sufficient.** Tokens with a low total supply can be easily manipulated.
- [X] **The tokens are located in more than a few exchanges.** If all the tokens are in one exchange, a compromise of the exchange can compromise the contract relying on the token.
- [X] **The token does not allow flash minting**. Flash minting can lead to substantial swings in the balance and the total supply, which neccessitate strict and comprehensive overflow checks in the operation of the token. 

#### References
* https://docs.porter.finance/portal/resources/risks#collateral-token-risk
* [Token Integration Risks](https://blog.openzeppelin.com/workshop-recap-secure-development-workshop-1/)
* [Token Integration Checklist](https://ethereum.org/ka/developers/tutorials/token-integration-checklist/)
* https://github.com/crytic/building-secure-contracts/blob/master/development-guidelines/token_integration.md
* https://tribe.fei.money/t/tribe-turbo-launch-group/3959
