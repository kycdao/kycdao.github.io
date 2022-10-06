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
    override fun getAvailableWallets(): List<String> {
        return addresses   //[0x2a93b57769..., 0x2b234a943...]
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
//Connect to a wallet
WalletConnectManager.connectWallet { createdSession ->
    //On connection successfully established
    myWalletSession = createdSession
}

// Or show a QR code to connect with another device
val qrCodeUri = WalletConnectManager.getUri()
showQRcode(qrCodeUri)
```
+++
**Configure KycSession**

Initialize the KycDaoSession with the WalletSession that you created before. You will also have to provide a wallet address, that you want to associate with the kycSession. 
With this interface you can guide the user through the KycDao process, while implementing your own logic in between.
```
 myKycSession = kycManager.createSession(choosenWallet, walletSession)
```
**KycManager**

Interacting with the KycSession happens not directly but through a manager class. Before calling any function of this class, make sure to first have a KycSession avalaible. This can be guranteed by first calling the prior mentioned createSession() method.

***Available Functions:***
# createSession


suspend fun createSession(walletAddress: [String](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html), walletSession: WalletSession): KycSession

Creates a kycSession that will be used by the KycManager.
Must be called first to ensure that KycManager has access to a session.

#### Return

The created kycSession

## Parameters

| | |
|---|---|
| walletAddress | The wallet address which will be linked to the kycSession |
| walletSession | An implementation of the WalletSession interface used to access the wallet of the user |

# login


suspend fun login(signature: [String](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html)): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-boolean/index.html)

Logs in the user, based on their signature

#### Return

Returns whether the login was successful or not

## Parameters

| | |
|---|---|
| signature | Personal signed signature created by WalletSession.personalSign() |

# savePersonalInfo

suspend fun savePersonalInfo(personalDataResult: [PersonalDataResult])

Save the personal information of the user and sends confirmation email if email is not yet confirmed.

By calling this function the disclaimer is also accepted. The function finishes when the email is confirmed.

## Parameters

| | |
|---|---|
| personalDataResult | The personal information to be saved wrapped in a PersonalDataResult class |

# selectAndPrepareForNFTMinting


suspend fun selectAndPrepareForNFTMinting(activity: [ComponentActivity](https://developer.android.com/reference/kotlin/androidx/activity/ComponentActivity.html)): [String](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html)?

Launches the predefined NftSelector activity on which a selection must be made, and returns with the id of the selectedImage.

Returns after the minting of the selectedNft has been authorized.

#### Return

Id of the selected NFT image

## Parameters
| | |
|---|---|
| activity | Activity that launches the new NftSelectorActivity |

# mint

suspend fun mint(performTransaction: suspend (MintingProperties) -&gt; MintingTransactionResult?)

Performs a minting operation

Finsihes after minting has finished and a receipt is found for it.

## Parameters

| | |
|---|---|
| performTransaction | Lambda function which contains the actual minting call, using the WalletSession interface |

# startPersonaIdentification


fun startPersonaIdentification(activity: [ComponentActivity](https://developer.android.com/reference/kotlin/androidx/activity/ComponentActivity.html))

Starts the persona identification process.

## Parameters

| | |
|---|---|
| activity | The activity that starts the new activity containing the persona process |

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