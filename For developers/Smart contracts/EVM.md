---
label: EVMs
icon: dot
order: 100
---

Although Soulbound tokens have been a popular point of [discussion](https://github.com/ethereum/EIPs/issues/1238) in the Ethereum community, the adoption of a standard has yet to fully take off.

For this reason we've used the most well known NFT standard ([ERC721](https://eips.ethereum.org/EIPS/eip-721)) and modified it to prevent transfers. You can see the source code for our EVM contracts [here](https://github.com/kycdao/smart-contracts/tree/main/ethereum/kycdao-ntnft/contracts)

## Expiry and Revoking

The most important addition we've made to the ERC721 standard is an expiry date for the NFT and the ability to revoke NFTs, making them invalid. Both of these fields are tracked on-chain, rather than in token metadata, which allows other smart contracts to know whether a certain NFT is valid.

Other smart contracts can quickly check if a certain address has a valid KYC NFT using the following function:

```solidity
    /// @dev Check whether a given address has ANY token which is valid, 
    ///      i.e. is NOT revoked and has an expiry in the future
    /// @param _addr Address to check for tokens
    /// @return valid Whether the address has a valid token
    function hasValidToken(address _addr) external view returns (bool valid);
```
For further information about the specific NFT associated with an address, including metadata, we also support [`ERC721Enumerable`](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#ERC721Enumerable).

## Use of Proxy for Upgrades

We currently use a simple [UUPSProxy](https://eips.ethereum.org/EIPS/eip-1822) for our smart contracts, allowing us to upgrade the contract.

## Deterministic Address

When deploying our smart contracts we use a [CREATE2](https://eips.ethereum.org/EIPS/eip-1014) deployer, which ensures we have a deterministic address. This way the address of our contracts on all chains remains the same.

## Support for Gas Station Network

Our smart contracts support [OpenGSN](https://opengsn.org/), which allows organizations to pay for their users gas costs on their behalf. If you're interested in using this please [get in touch](/support).