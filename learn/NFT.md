---
label: kycNFTs
order: 10
icon: image
---
---
This page explains the design of our initial proofs; kycNFTs: 

!!!info kycNFT
kycNFT is a non-transferable NFT, proof of a linked compliant account in the web3 space.  
!!!

=== kycNFTs are the web3 version of the Twitter tick:

web2:      @VitalikButerin :icon-verified: 

web3:      [!badge variant="dark" size="2xL" text="Medium" text="vitalik.eth :icon-check-circle-fill:"]

- kycNFTs are unique, [personalizable](/learn/NFT/NFT_art.md) and the members own them.
===


[!badge  corners="square" size="L" variant="danger" text="Medium" text="No PII on-chain"] - kycNFTs do not contain personally identifiable information. [Read more](/concepts/nft/nft_metadata.md)

kycNFT (membership status) minting is FREE on every chain; requires [kycDAO membership](learn/membership.md). 

---

### Background: 

!!!info NFT
NFT stands for **Non-fungible token**. It is a unique asset that stored on the blockchain.
!!!

NFTs as a concept are prolific, and they exist on almost every blockchain. For this reason, kycDAO uses a particular type of NFTs to represent a user's verification.

Unlike most standard NFTs, kycNFTs represent identity verifications, which only make sense when associated with a specific account or address, therefore, our NFTs designed to be `non-transferable`.

--- 
!!!info SBT 
SBT stands for **Soulbound token**. It is a `non-transferable` asset stored on the blockchain.
!!! 

The concept of an NFT, which is bound to an account, has been discussed at length on various blockchains and has been referred to by several names:

- **Soulbound tokens** (SBTs)
- **Account/Address bound tokens** (ABTs)
- **Non-transferable NFTs** (NTNFTs)

kycDAO supports multiple different blockchain types, and each blockchain has its own implementation or standard (and sometimes multiple!); we've attempted to use the most popular standard on each blockchain and tried to ensure the smart contract interface is as similar as possible.

For a more detailed explanation of the smart contracts kycDAO uses, please see [!button variant="info" icon="log" text="Smart contracts"](buidl)





## Why did kycDAO choose to use soulbound NFTs?

As the concept of a decentralized identity is such a common subject discussed in web3, solutions for how to implement it have also brought up some great discussions.

Another commonly recognized alternative for sharing information related to identity is [verifiable credentials](https://www.w3.org/TR/vc-data-model/) or VCs.

We've written a blog post summarizing our thoughts on the benefits and disadvantages of [NFTs vs. VCs](https://blog.kycdao.xyz/nft_vs_vc/).