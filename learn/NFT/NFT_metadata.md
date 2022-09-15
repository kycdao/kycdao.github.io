---
label: kycNFT metadata
icon: code-square
order: -8
---

The metadata schema used for each kycDAO NFT will always store all necessary fields for using our service, however to conform to the standards for each blockchain the exact schema will differ slightly.


**kycNFT** specific metadata concepts: 

Metadata   | Type | Description
:---   | :---: | :---
Validity | boolean  | Verification is `valid` or `non-valid`.
Tier | x | Represent the verification type(s).
Unique | x | Represents a Proof of Human factor
Custom | x | This is an owner extenable function. 

[!badge  corners="square" size="L" variant="danger" text="Medium" text="No PII on-chain"] - kycNFTs do not contain personal identifiable information.

---
  
For technical details go to [:icon-log: Smartcontracts]()