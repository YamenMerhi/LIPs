---
lip: 10
title: ReceivedVaults
author: 
discussions-to: https://discord.gg/E2rJPP4
status: Draft
type: LSP
created: 2021-12-1
requires: LSP2
---

## Simple Summary
This standard describes a set of [ERC725Y](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-725.md) key values to store addresses of received vaults in a [ERC725Y](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-725.md) smart contract.

## Abstract
This key value standard describes keys to be added to an [ERC725Y](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-725.md) smart contract, that reference received vaults smart contracts. Two keys are proposed: `LSP10ReceivedVaults[]` to hold an array of addresses and `LSP10ReceivedVaultsMap` to hold a mapping of the index in the former array and an standards interface ID to be able to quickly tell different vaults standards apart without querying each other vaults smart contract directly. The key `LSP10ReceivedVaultsMap` also helps to prevent adding duplications to the array, when automatically added via smart contract (e.g. a [LSP1-UniversalReceiverDelegate](https://github.com/lukso-network/LIPs/blob/master/LSPs/LSP-1-UniversalReceiver.md)).

## Motivation
To be able to display received vaults in a profile we need to keep track of all received vaults contract addresses. This is important for [LSP3 UniversalProfile](https://github.com/lukso-network/LIPs/blob/master/LSPs/LSP-3-UniversalProfile.md), but also Assets smart contracts via [LSP5-ReceivedAssets](https://github.com/lukso-network/LIPs/blob/master/LSPs/LSP-5-ReceivedAssets.md) Standard.

## Specification

Every contract that supports to the ERC725Account SHOULD have the following keys:

### ERC725Y Keys


#### LSP10ReceivedAssets[]

References issued smart contract vaults.

```json
{
    "name": "LSP10Vaults[]",
    "key": "0x55482936e01da86729a45d2b87a6b1d3bc582bea0ec00e38bdb340e3af6f9f06",
    "keyType": "Array",
    "valueContent": "Address",
    "valueType": "address"
}
```


#### LSP10ReceivedVaultsMap

References issued smart contract vaults.

The `valueContent` MUST be constructed as follows: `bytes8(indexNumber) + bytes4(standardInterfaceId)`. 

```json
{
    "name": "LSP10VaultsMap:<address>",
    "key": "0x192448c3c0f88c7f00000000<address>",
    "keyType": "Mapping",
    "valueContent": "Mixed",
    "valueType": "bytes"
}
```

## Rationale

## Implementation

A implementation can be found in the [lukso-network/standards-scenarios](https://github.com/lukso-network/lsp-universalprofile-smart-contracts/tree/develop/contracts/LSP1UniversalReceiver/LSP1UniversalReceiverDelegateVault);
The below defines the JSON interface of the `LSP10ReceivedVaults`.

ERC725Y JSON Schema `LSP10ReceivedVaults`:
```json
[
    {
        "name": "LSP10VaultsMap:<address>",
        "key": "0x192448c3c0f88c7f00000000<address>",
        "keyType": "Mapping",
        "valueContent": "Mixed",
        "valueType": "bytes"
    },
    {
        "name": "LSP10Vaults[]",
        "key": "0x55482936e01da86729a45d2b87a6b1d3bc582bea0ec00e38bdb340e3af6f9f06",
        "keyType": "Array",
        "valueContent": "Address",
        "valueType": "address"
    }
]
```

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
