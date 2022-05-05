# Checklist
The following criteria and checks are used before a token is added to the Porter allow-list. 

## Overall Project/Market Conditions

- [ ] Token must be listed and have pricing data via coingeko
- [ ] Legitimacy of the project/ protocol
- [ ] Total MarketCap > $100 million
- [ ] Average daily on-chain liquidity over 30 days > $10,000,000

## Token Security 
- [ ] ERC20 spec is correctly followed (confrmed by slither-check-erc)
- [ ] Token is verified on Etherscan
- [ ] Administrative privileges over the protocol should not be owned by an EOA, any multisig must have known members.
- [ ] If token supply is not fixed, conditions under which supply can increase needs to be made aware of and low risk 
- [ ] No fee is taken on transfer
- [ ] Token is not upgradable
- [ ] The owner has limited minting capabilities
- [ ] The token is not pausable
- [ ] The owner can not disallow-list the contract
- [ ] Token ownership should be widely distributed with no address (whale) owning more than 30% 

### More details and inspiration
* https://docs.porter.finance/portal/resources/risks#mitigating-collateral-token-risk
* https://tribe.fei.money/t/tribe-turbo-launch-group/3959
* [Token Integration Checklist](https://ethereum.org/ka/developers/tutorials/token-integration-checklist/)
* [Token Integration Risks](https://blog.openzeppelin.com/workshop-recap-secure-development-workshop-1/)
