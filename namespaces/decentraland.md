---
namespace: urn:decentraland
github-org: https://github.com/decentraland
contact-email: developers@decentraland.org
---

# Description

Decentraland is a virtual reality platform powered by the Ethereum blockchain. 

# Resolver structure

The structure of the resolver is defined by a hierarchy of content address resolvers.

```yml
urn:decentraland:{protocol}:(...)
```

The hierarchy is defined by the `{protocol}` component of the URN.

## The Ethereum resolvers

Decentraland works in Ethereum mainnet, ropsten and Matic. There are 4 registered roots for blockchain assets:

- Ethereum Mainnet: `urn:decentraland:ethereum:{contract-or-alias}:{tokenId}`
- Ethereum Ropsten: `urn:decentraland:ropsten:{contract-or-alias}:{tokenId}`
- Matic Mainnet: `urn:decentraland:matic:{contract-or-alias}:{tokenId}`
- Matic Mumbai: `urn:decentraland:matic:{contract-or-alias}:{tokenId}`

### Aliases

For each protocol, to make the URN friendlyer to read, we specify some aliases, the aliases are defined in this live file: https://contracts.decentraland.org/addresses.json which should be used every time a contract needs to be resolved.

#### Example: Ethereum Mainnet

- `urn:decentraland:ethereum:LAND` resolves to `0xf87e31492faf9a91b02ee0deaad50d51d56d5d4d`
- `urn:decentraland:ethereum:ESTATE` resolves to `0x959e104E1a4dB6317fA58F8295F586e1A978c297`

Using that information, `urn:decentraland:ethereum:LAND:4763953136893138488487244504044754960247` resolves to `urn:decentraland:ethereum:0xf87e31492faf9a91b02ee0deaad50d51d56d5d4d:4763953136893138488487244504044754960247` which can be interpreted as:

```yml
# to validate ownership in the blochckain of urn:decentraland:ethereum:LAND:4763953136893138488487244504044754960247
ethereum-chain: mainnet
contract: 0xf87e31492faf9a91b02ee0deaad50d51d56d5d4d (LAND)
token-id: 4763953136893138488487244504044754960247
```

### Content resolvers

(more to come)

## Custom resolvers

For some use cases, like default wearables (non-blockchain based assets) we will use custom resolvers.

Custom resolvers start with `x-` in the protocol, like custom HTTP headers. This is so to avoid conflicts with future protocols and to easily differentiate blockchain assets from non-blockchain assets.

E.g. `urn:decentraland:x-base-avatars:{collection}:{assetId}` -> `urn:decentraland:x-base-avatars:hats:top-hat-1`
