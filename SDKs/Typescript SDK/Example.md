---
label: Example
icon: code
order: -1
---

!!!
This is an example page showing how to integrate kycDAO. The example is a grant program site which requires KYC compliance for submitting proposals.
!!!

See the example website here: [grant.com]()

The code for this site is here: [example-repo]()

## Theoretical user interaction flow

1. user opens grant.xyz site
2. user connects their wallet 
    a.  site calls SDK to validate selected network
3. **site checks whether user has kycNFT**
    - if yes, thanks
4. if no, **user starts KYC process via integrated kycDAO**
    - grant site requests required information from user
    - start IdV [persona]
        - user provides required infromation to IdV provider
    - grant site waits for SDK to get result from IdV provider (via active backend polling)
    - NFT selection [_is out of scope for now_]
    - minting
        - request kycDAO backend to send minting authorization to kycNFT smart contract
        - ensure user has the correct network selected in their wallet
            - network select: intersection of the “allowed networks from the SDK configuration” and “allowed by the backend”
            - ⇒ [concrete algorithm for this](https://www.notion.so/EVM-SDK-769a3ca4a4ec468d9db54fc0e1319ca6)
        - prompt user to sign minting transaction via EIP-1193
        - wait for minting
5. site checks whether they have already submitted their grant proposal [mock]
    - if yes, thanks
6. if no, user submits proposal [mock]
7. proposal accepted/rejected by [grant.xyz](http://grant.xyx) team [mock]
