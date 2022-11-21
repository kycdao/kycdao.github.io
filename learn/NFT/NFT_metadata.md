---
label: kycNFT metadata
icon: code-square
order: 10
---

The metadata schema used for each kycDAO NFT will always store all necessary fields. The exact schema can differ slightly to conform to each supported blockchain.


**kycNFT** specific metadata primitives: 

Metadata   | Type | Description
:---   | :---: | :---
Validity | boolean  | is `valid` / `non-valid` calculated from `verified` + `expiry`
Verified | boolean  | Linked verification status maintained by kycDAO
Expiry | date  | Membership is valid until
Tier |  | Represent the verification type(s)
Custom |  | Future extension function

[!badge  corners="square" size="L" variant="danger" text="Medium" text="No PII on-chain"] - kycNFTs do not contain personal identifiable information.

---
  
For technical details go to [:icon-log: Smartcontracts]()