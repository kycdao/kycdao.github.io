---
label: Andorid SDK
icon: device-mobile
---

## Getting started
[Android sdk](https://www.example.com)
## Download
Gradle:
```
dependencies {
  ...
  implementation 'com.github.kycdao.sdk:android:1.0.0'
}
```
## How to use
Check the [sample application](https://www.example.com)

**WalletSession**

The WalletSession interface provides the connection between the wallet and the KycDaoSession.
You can either use the default implementation, which uses [WalletConnect v1](https://docs.walletconnect.com) to the connection.
Or you can also create your own class if you don't need to connect, for example because you are using this SDK from a wallet.
+++ Own implementation

```
class MyWalletSession : WalletSession {
    override fun getWalletAddress(): String {
        return walletAddress   //0x2a93b577696b80bff9af29f6561d83a4998ae09e
    }
    override fun getChainId(): String {
        return chainId   //80001
    }
    override fun personalSign(message: String): String {
        val signatureHex = eth_personal_sign(message)
         return signatureHex   //0x38a9e0b6cbe...
    }
    override fun sendMintingTransaction(mintingProperties: MintingProperties): String {
        val txHash = mint_transaction(mintingProperties)
        return txHash   //0x4327025aeac99...
    }
}

val walletSession = MyWalletSession()
```

+++ WalletConnect 

```
WalletConnectManager.subscribeSession { walletSession ->
    // The connection is established
}

// Open the wallet on this device for the connection
WalletConnectManager.connectWallet()

// Or show a QR code to connect with another device
val qrCodeUri = WalletConnectManager.getUri()
showQRcode(qrCodeUri)
```

+++

**Configure KycSession**

Initialize the KycDaoSession with the Walletsession that you created before.
With this interface you can guide the user through the KycDao process and show any screen you want.
```
 val kycSession = KycSessionManager.createSession(walletSession)
```

**KycDao methods**

[Under Construction]


**Sample**

After each step, you can ask what the next step is that you need to take. Based on this, you can display a screen to the user and then call the appropriate method to execute the next step.
```
    val state = kycSession.getState()

    when (state) {
        State.LOGIN_REQUIRED -> kycSession.login()
        State.USER_INFORMATION_REQUIRED -> kycSession.updateUser(email = "", residency = "US", legalEntity = false)
        State.WAIT_EMAIL_CONFIRMED -> kycSession.pollEmailConfirmed()
        State.IDENTITY_VERIFICATION -> kycSession.identityVerification()
        State.POLL_IDENTITY_VERIFICATION_RESULT -> kycSession.pollIdentityVerificationRequest()
        State.NFT_IMAGE_SELECTION -> {
            val nftImages = kycSession.getNftImageList()
            // select one NFT image
            kycSession.authorizeMinting(selectedNftImage)
        }
        State.WAITING_FOR_MINTING_AUTHORISATION -> kycSession.checkAuthorizeMinting()
        State.CALCULATE_FEE -> kycSession.calculateFee()
        State.MINTING -> kycSession.minting()
        State.CHECK_MINTING -> kycSession.checkMinting()
        State.POST_MINT_TOKEN_ID -> kycSession.sendMintToken()
        State.COMPLETED -> // Done
    }

```