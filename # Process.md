# Process

docker pull trailofbits/eth-security-toolbox
docker run -it -v /Users/bookland/porter/v1-core:/share trailofbits/eth-security-toolbox
cd /share
pip3 install slither-analyzer --upgrade

slither-check-erc 0xdac17f958d2ee523a2206206994597c13d831ec7 TetherToken

- slither [target] --print human-summary
- slither [target] --print contract-summary
- slither-prop 


https://ethereum.org/ka/developers/tutorials/token-integration-checklist/