---
label: NFT metadata
icon: code
order: -100
---

The metadata schema used for each kycDAO NFT will always store all necessary fields for using our service, however to conform to the standards for each blockchain the exact schema will differ slightly.

## Ethereum (or EVM based chains)

The majority of metadata for EVM based chains will be stored off-chain, to reduce gas costs.

Using the [ERC-721]() function `tokenURI` will return an IPFS URI to a JSON document with the metadata.

Here's an example of the JSON metadata stored in IPFS:

```JSON
{
    "description": "An example of a non-transferable KYCDAO NFT",
    "image": "ipfs://QmRCe3McAC4i9Tc6A…cJLCAaM1uv5U8ZSxYUMexSp",
    "name": "KYCDAO NFT"
}
```

## NEAR

For NEAR we follow the NEAR NFT metadata standard [NEP-177](https://github.com/near/NEPs/blob/master/neps/nep-0177.md), with some extensions in the `extra` field.

```rust
type TokenMetadata = {
  title: string|null, // ex. "Arch Nemesis: Mail Carrier" or "Parcel #5055"
  description: string|null, // free-form description
  media: string|null, // URL to associated media, preferably to decentralized, content-addressed storage
  media_hash: string|null, // Base64-encoded sha256 hash of content referenced by the `media` field. Required if `media` is included.
  issued_at: number|null, // When token was issued or minted, Unix epoch in milliseconds
  expires_at: number|null, // When token expires, Unix epoch in milliseconds
  extra: string|null, // anything extra the NFT wants to store on-chain. Can be stringified JSON.
  reference: string|null, // URL to an off-chain JSON file with more info.
  reference_hash: string|null // Base64-encoded sha256 hash of JSON from reference field. Required if `reference` is included.
}
```

## Solana

On Solana we follow [Metaplex's NFT metadata standard](https://docs.metaplex.com/programs/token-metadata/changelog/v1.0)

Here is an example of the JSON metadata stored off-chain referred to in the `uri` field:

```JSON
{
  "name": "kycDAO NFT",
  "symbol": "KYCDAO",
  "description": "A non-transferable NFT from kycDAO",
  "image": "https://www.arweave.net/abcd5678?ext=png",
  "external_url": "https://kycdao.xyz",
  "collection": {
     "name": "kycDAO NFT",
     "family": "KYC"
  }
}
```

## Aptos
