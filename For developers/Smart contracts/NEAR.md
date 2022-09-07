---
label: NEAR
icon: dot
order: 99
---

There has been [discussion](https://github.com/near/NEPs/pull/359) for a NEAR non-transferable NFT, however there is currently no established NEP.

Our NEAR smart contracts closely follow the [NEP171](https://nomicon.io/Standards/Tokens/NonFungibleToken/Core) standard for NFTs. We have removed any functions related to transfers or approvals.

In the hopes that our implementation for non-transferable NFTs (NTNFTs) will some day become a NEAR standard, we have added it to the `near-sdk-rs` repository. See our branch [here](https://github.com/kycdao/near-sdk-rs/tree/ntnft/near-contract-standards/src/ntnft) for details.

For details of our specific KYC additions for NTNFTs (including metadata specifics) see our code [here](https://github.com/kycdao/smart-contracts/tree/main/near/kycdao-ntnft)