## Scan API Reference

List of APIs:

- [queryDataBase](#queryDataBase)

#### queryDataBase

Uri: /scan/queryDataBase

Request method: GET

Returns the ABEY Chain real time data, include Lightning Block、Block Time、Snail Block、Transaction Count、Address Count、Committee.

##### Parameters

Parameter：

none

##### Returns

`lightningBlocks` - Lightning Block.

`snailBlocks` - Snail Block.

`totalTxs` - Transaction Count.

`totalAddress` - Address Count.

`committee` - Committee.

`blockTime` - Block Time.

##### Example
```js
// Request
curl --location --request GET 'https://scanapi.abeychain.com/scan/queryDataBase'

// Result
{
    "code": 200,
    "message": "success",
    "data": {
        "lightningBlocks": 8027675,
        "totalTxs": 33230820,
        "totalAddress": 163163,
        "snailBlocks": 67272,
        "committee": 322,
        "blockTime": "5.1"
    }
}
```

