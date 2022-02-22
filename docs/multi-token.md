---
tags: [erc1155] [multi]
---

# How to create ERC-1155 token

*This article describes how to create your own ERC-1155 token using a single TATUM API call.*

```json
POST 'https://api-eu1.tatum.io/v3/multitoken'
```

---

## ERC-1155

The ERC-1155 is a standardized smart contract with a predefined set of features. These tokens have common properties with both fungible and non-fungible tokens. Any single contract may include any combination of fungible, non-fungible, or semi-fungible tokens.

NFTs are typically made using ERC-721 smart contracts on Ethereum-compatible blockchains. While this type of contract gives them the unique properties that make them so desirable (scarcity, verifiable authenticity), it also has certain limitations.

ERC-721 tokens each have a unique ID. This makes batch operations very costly in terms of gas fees and makes shared ownership impossible.

According to ERC-1155, a single smart contract can include multiple  tokens. This opens up all sorts of possibilities for shared ownership, gaming applications, and a wide range of other use cases.

However, creating an ERC-1155 smart contract on an Ethereum-compatible blockchain is not easy at all. As a developer, you have to know a lot of things:
- Solidity - a new programming language for writing smart contracts
- How to use a compiler for Solidity
- How to develop using an IDE
- How to deploy the compiled smart contract

---

## TATUM unified API call

This method creates a new ERC1155 Smart Contract (Multi Tokens) on the blockchain. The smart contract is standardized and audited. Minting, burning and transfering tokens is possible, as well as minting multiple tokens at once.
Tatum now supports Multi Tokens on these blockchains:
- Ethereum
- Polygon (Matic)
- Celo
- Harmony.ONE
- Binance Smart Chain

Check the API call documentation for information about all parameters. 

The parameters `chainId` and `x-testnet-type` are worth noting:
- The `chainId` parameter is used to select a specific blockchain for deploying our prebuilt ERC1155 tokens.
- The `x-testnet-type` parameter is used to select which environment you want to call the API in. Valid for Ethereum invocations only.


**Request body example**
```json
{
  "uri": "example.com",
  "fromPrivateKey": "0x05e150c73f1920ec14caa1e0b6aa09940899678051a78542840c2668ce5080c2",
  "nonce": 0,
  "feeCurrency": "CELO"
}
```

**Response body example**

```json
{
  "txId": "c83f8818db43d9ba4accfe454aa44fc33123d47a4f89d47b314d6748eb0e9bc9",
  "failed": false
}
```

<!-- theme: warning -->
> #### Security
>
> Blockchain transactions are signed using a private key via API, which is not a secure way of signing transactions. Your private keys and mnemonics should never leave your security perimeter. To correctly and securely sign a transaction, you can use the [Tatum CLI](https://github.com/tatumio/tatum-cli); a specific language library like [Tatum JS](https://github.com/tatumio/tatum-js); local [middleware API](https://github.com/tatumio/tatum-middleware); or our complex key management system, [Tatum KMS](https://github.com/tatumio/tatum-kms).

---

<!-- theme: info -->

> #### Learn more
>
>If you want to learn more about ERC-1155, [this standard](https://eips.ethereum.org/EIPS/eip-1155) might be useful, as well as [this explanation](https://academy.bit2me.com/en/what-is-token-erc-1155/).