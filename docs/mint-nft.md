# How to mint NFT 
Ride the shockwave of the NFT explosion and create your own NFTs without learning to code smart contracts. Allow users to mint and sell NFTs that automatically pay out royalties with every transfer, tokenize in-game assets, and quickly implement cutting-edge NFT solutions for any product vertical.

## Supported blockchains 

Blockchain | Deploy NFT contract | Mint NFT
---------|----------|---------
 Algorand | - | ✓
 Binance Smart Chain | ✓ | ✓
 Celo | ✓ | ✓
 Ethereum | ✓ | ✓
 Flow | ✓ | ✓
 Kucoin | ✓ | ✓
 Klaytn | ✓ | ✓
 Harmony | ✓ | ✓
 Polygon | ✓ | ✓
 Solana* | - | ✓
 Tron | ✓ | ✓

**For Solana, NFTs are not deployed, only minted right away. Newly created NFT creates new address on the blockchain and owner of the NFT owns with it's private key the account of the NFT.*

## Mint NFT

[Minting NFT operation](https://docs.tatum.io/rest/smart-contracts/b3A6MzA3NjA4OTQ-mint-nft) can be used in 3 different ways.

1. First mode works just like other NFT endpoints. Every time the funds are transferred, the transaction must be signed with the corresponding private key.

2. Second mode works without private key or signature id. Mint NFT requests use built-in smart contract, private key and token id which are provided by Tatum.

You dont need to provide fromPrivateKey (or signatureId), contractAddress and tokenId fields to perform the mint NFT request.

3. Third mode enables you to mint on any custom NFT ERC-721 smart contract, on which specified minter address is approved as a minter. You don't specify private key or signatureId, only minter address, from which the NFT will be minted.

You can use addresses specified in the bellow table to be used as a minter.

Performed request without fromPrivateKey or signatureId fields will be populated with following attributes:

- `fromPrivateKey` - a built-in private key connected to the address from which will be NFT transaction fees paid.
- `tokenId` - a counter which starts from 0 and is increased for each NFT mint request by 1. The tokenId is provided per each chain and mainnet/testnet version of network.
- `contractAddress` - represents Tatum built in smart contract address of the minted NFT.

The blockchain fee of the performed transaction is paid from the address connected with built-in private key and is debitted in form of credits. The credits are debitted only if NFT mint requests are performed with paid API key plan.

We transform fee to the credits in accordance to the rates provided by the Tatum.

It means if you perform mint NFT request with following body:

```json
{
  "chain": "BSC",
  "to": "0xBC2eBA680EE50d685cc4Fe65f102AA70AfB27D3F",
  "url": "ipfs://QmXJJ6UF5WkF4WTJvsdhiA1etGwBLfpva7Vr9AudGMe3pj"
}
```
The fields contractAddress, fromPrivateKey and tokenId will be internally filled in following way:

```json
{
  "chain": "CELO",
  "to": "0xBC2eBA680EE50d685cc4Fe65f102AA70AfB27D3F",
  "url": "ipfs://QmXJJ6UF5WkF4WTJvsdhiA1etGwBLfpva7Vr9AudGMe3pj",
  "fromPrivateKey": "{tatumBuiltInPrivateKey}",
  "tokenId": "{tatumBuiltInTokenId + 1}",
  "contractAddress": "0x45871ED5F15203C0ce791eFE5f4B5044833aE10e"
}
```

Keep in mind that your credit amount will be debitted accordingly to the rate of the selected blockchain and cost of transaction fees.


We have prepared following smart contracts for minting without private key:

#### Testnet network
Blockchain | Address | Contract Address
---------|---------|---------
BSC |0xc16ae5e8c985b906935a0cadf4e24f0400531883| 0xF73075aa67561791352fbEe8278115487Fd90ab6
Celo | 0xBC2eBA680EE50d685cc4Fe65f102AA70AfB27D3F| 0x45871ED5F15203C0ce791eFE5f4B5044833aE10e
Ethereuem  | 0x53e8577C4347C365E4e0DA5B57A589cB6f2AB848| 0xAe7D8842D0295B1f24a8842cBd5eB83Ae2fd0946
Harmony | 0x8906f62d40293ddca77fdf6714c3f63265deddf0| 0x427ddbe3ad5e1e77e010c02e61e9bdef82dcaeea
Klaytn| 0x80d8bac9a6901698b3749fe336bbd1385c1f98f2| 0x45871ED5F15203C0ce791eFE5f4B5044833aE10e
Polygon| 0x542b9ac4945a3836fd12ad98acbc76a0c8b743f5| 0xCd2AdA00c48A27FAa5Cc67F9A1ed55B89dDf7F77

#### Mainnet network
Blockchain | Address | Contract Address
---------|---------|---------
BSC |0xcf9e127455d28e7362380aec1b92ddee8200b295| 0x0A46D855221AF8F2336f3810e3d6013F10100577
Celo | 0xcf9e127455d28e7362380aec1b92ddee8200b295| 0xC49c2d52B3B4D0e3E52D1C8E0e10B13c82982E9d
Ethereuem  | 0xcf9e127455d28e7362380aec1b92ddee8200b295| 0x789c00ed7ddd72a806dbac40df926df32fde3c2f
Harmony | 0xcf9e127455d28e7362380aec1b92ddee8200b295| 0xA0BbB8140e9298E613Da57DDd269586473Bc94Be
Klaytn| 0xcf9e127455d28e7362380aec1b92ddee8200b295| 0x7c4e274387a9bc81f9de7502921fd0550583d3bb
Polygon| 0xcf9e127455d28e7362380aec1b92ddee8200b295| 0x29768a03a62760EF462c1F0fFEC1C027B981B909


<!-- theme: danger -->
>No one should ever send it's own private keys to the internet because there is a strong possibility of stealing keys and loss of funds. In this method, it is possible to enter privateKey or signatureId. PrivateKey should be used only for quick development on testnet versions of blockchain when there is no risk of losing funds. In production, <a href="https://github.com/tatumio/tatum-kms" target="_blank">Tatum KMS</a> should be used for the highest security standards, and signatureId should be present in the request. Alternatively, using the Tatum client library for supported languages.
