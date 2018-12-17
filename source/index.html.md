---
title: Zilliqa JSON-RPC API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/Zilliqa/Zilliqa-Javascript-Library'>Javascript SDK</a>
  - <a href='http://scilla.readthedocs.io/'>Scilla Docs</a>

includes:

search: true
---

# Introduction

[JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC) is a remote procedure call protocol encoded in JSON. You can use this API to access data in Zilliqa nodes.
The JSON-RPC API server runs on:

+ `http://localhost:4201/` when running Zilliqa locally.
+ `https://api.zilliqa.com/` when running on Zilliqa _Maoshanwang_ testnet.
+ `https://api-scilla.zilliqa.com/` when running on the small-scale testnet for developers.

All API calls are POST requests made to machine running the Zilliqa lookup node.

All requests follow the standard JSON-RPC format and include 4 variables in the data object:

+ `id: (e.g. "1")`
+ `jsonrpc: (e.g. "2.0")`
+ `method: (e.g. "GetBalance")`
+ `params: (e.g. ["1"])`

Code examples using curl can be viewed in the dark area to the right.

# Blockchain-related methods

## GetNetworkId

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNetworkId",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "TestNet"
}
```

Get the network ID from the specified lookup node.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetNetworkId"
params | ""

## GetBlockchainInfo

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetBlockchainInfo",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "CurrentDSEpoch":"26",
        "CurrentMiniEpoch":"1250",
        "DSBlockRate":1.9217623126238637e-08,
        "NumDSBlocks":"27",
        "NumPeers":40,
        "NumTransactions":"16038",
        "NumTxBlocks":"1250",
        "NumTxnsDSEpoch":"8970",
        "NumTxnsTxEpoch":0,
        "ShardingStructure":{
            "NumPeers":[10,10,10]
        },
        "TransactionRate":0,
        "TxBlockRate":8.0917876984482132e-07
    }
}
```

Get the current network statistics from the specified lookup node.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetBlockchainInfo"
params | ""

## GetShardingStructure

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetShardingStructure",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "NumPeers":[10,10,10]
    }
}
```

Get the current sharding structure of the network from the specified lookup node.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetShardingStructure"
params | ""

## GetDsBlock

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetDsBlock",
    "params": ["1"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "header":{
            "BlockNum":"1",
            "Difficulty":3,
            "DifficultyDS":5,
            "GasPrice":"100",
            "LeaderPubKey":"0x0208EA17FE78DE1D4A17B921B7ADB2B3FEE4C795FC5FD54BEA80FCE926F09F79F3",
            "PoWWinners":[
                "0x0307BA09F607D36C6D3B2AC7541592DB8674A889690A14B816FACF67B4F9221CEC",
                "0x0342081E95907022E1E5A525F2D7CE51EB5AF56B7EB13C29C6EC194FB93DF2E752"
            ],
            "PrevHash":"ba127538d2c63eec121629011ae8173210589689dca54d1e11904dd82c68e9da",
            "Timestamp":"1544755380363821"
        },
        "signature":"E2EC67C64323D73D8CCBCC79FEEE04826702751D599995B997AFF7452A7CB7D11CEA8DC5275E9CEAAF7C623F2FEEE132A5F2EF5B9EB63D8C4C5CDD97D64B6CC3"
    }
}
```

Get the details of a specified Directory Service block number.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetDsBlock"
params | A specified DS block number.

## GetLatestDsBlock

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetLatestDsBlock",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "header":{
            "BlockNum":"26",
            "Difficulty":3,
            "DifficultyDS":16,
            "GasPrice":"100",
            "LeaderPubKey":"0x020C11D6B9CA45B56EC80705F1070D9928CFA4BA99212BEF934307C228ECC309FC",
            "PoWWinners":[
                "0x02CB5328E79387F337EC671ECFF0CF2501CCD4DDFCA3565640F94792DE0A7EA0F9",
                "0x0320D26B67A1C701377AA391F2572B66D72F5D0E1A23C44E5B1DA7BF2D53C653E1"
            ],
            "PrevHash":"449a67f3cb160f598ac279f95e6583868a2052c846123558866f56dd6d70cd6c",
            "Timestamp":"1544776175498144"
        },
        "signature":"D096A9F6FB4DAFCFE7112D1C9684CAC2338CDBF0FC17E2B9DF814751BEA8E1F84A889DBC0CEBF903BFD06B1E0C0165F29347EED51B86A613F3C5A18F1CA11EEA"
    }
}
```

Get the details of the most recent Directory Service block.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetLatestDsBlock"
params | ""

## GetNumDSBlocks

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumDSBlocks",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":"27"
}
```

Get the number of Directory Service blocks in the network so far.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetNumDSBlocks"
params | ""

## GetDSBlockRate

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetDSBlockRate",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":1.9217623126238637e-08
}
```

Get the current Directory Service blockrate per second.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetDSBlockRate"
params | ""

## DSBlockListing

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "DSBlockListing",
    "params": [1]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "data": [
      {
        "BlockNum": 208,
        "Hash": "D5D8D80034EA93409B0F2DA493533EAA4B5BE5301E705C82A30FB521000CCBD3"
      },
      {
        "BlockNum": 207,
        "Hash": "4FB82808E837F4A2E7C9818CAE4968861F4CF66CB835509EE02ADD08D82F77A8"
      },
      {
        "BlockNum": 206,
        "Hash": "1E21DFFD46147A14C3A2155D588BEF969133A7315E015814D67C38685715A116"
      },
      {
        "BlockNum": 205,
        "Hash": "23D514E64F4F1C7F878EACC239FD7D3E78C1860BCB89CA3E2798BA80B5F62CFB"
      },
      {
        "BlockNum": 204,
        "Hash": "01230FFBC0DA3EBD4DE7C3B4C8438CDD8215171F773731DCA06937754A943868"
      },
      {
        "BlockNum": 203,
        "Hash": "AFFF5FCAABD67639CAD1954836818093AD323F7874D2C7A0850B8ACB2A130100"
      },
      {
        "BlockNum": 202,
        "Hash": "1499C28EF49D534741A988007715376DF437120994DD5999BF15A9168C5414E9"
      },
      {
        "BlockNum": 201,
        "Hash": "A3C62538289B094FBAC4641172E8EA46EE7440733DF497465EB68FB1D26E82E6"
      },
      {
        "BlockNum": 200,
        "Hash": "A200CB54AE5B1D2BB6E8A7E4B3BF930E8DA1081188F6F96DD59FD6D483FEB3E6"
      },
      {
        "BlockNum": 199,
        "Hash": "A4DC7549D3D2A7EA24AA373FDDEB0A5DF06BB8B77C7918015DFB489587BD1C07"
      }
    ],
    "maxPages": 21
  }
}
```

Get a paginated list of Directory Service blocks. Pass in page number as parameter. Returns a `maxPages` variable that specifies the max number of pages. `1` being latest block.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "DSBlockListing"
params | Page number (of type `Int`) of the listings (`1` being the latest block).

## GetTxBlock

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTxBlock",
    "params": ["100"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "body":{
            "HeaderSign":"88DE8A7BE752A8399ACDEEFF71E0E5515E04AEEC6C27EBB2CBC51B4686D019C70E6D01DA3B60AD8660DD871AA58E4118E866EB02A293BE3AA03407B247663D0B",
            "MicroBlockInfos":[[],[[]],[[],[[]]],[[],[[]],[[],[[]]]]]},
            "header":{
                "BlockNum":"100",
                "DSBlockNum":"3",
                "GasLimit":"200000",
                "GasUsed":"0",
                "MbInfoHash":"ef2226b10220289ae75d616c62e64e799d98f429af1d230c2f4d3f4e0998597f",
                "MinerPubKey":"0x0389465277028C9382F3314ED01BACF9CA6DAAC02A48B85756A513C66346F06963",
                "NumMicroBlocks":4,
                "NumTxns":0,
                "PrevBlockHash":"294f14853b92b8f9ed5ac4a708ec928e2aebf4f39afd38f7e0bb7f7728728f9c",
                "Rewards":"0",
                "StateDeltaHash":"0000000000000000000000000000000000000000000000000000000000000000",
                "StateRootHash":"b44f0b4557f5efb5bc4db798540481b102ba6c239acbe403e42dd0b820b32ba9",
                "Timestamp":"1545026406814544",
                "Type":1,
                "Version":0
            }
    }
}
```

Get the details of a specified Transaction block number.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetTxBlock"
params | A specified Transaction block number.

## GetLatestTxBlock

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetLatestTxBlock",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "body":{
            "HeaderSign":"5AA9C0DEEF08985379A5F0981C7DD5982D03629B0C55AE7EE5FA13F276FAF94B38A3A94332E8CC0DFEB2D6952E0280B52A46B8FBA7D5D15D0E49936BA80B06A7",
            "MicroBlockInfos":[[],[[]],[[],[[]]],[[],[[]],[[],[[]]]]]
        },
        "header":{
            "BlockNum":"960",
            "DSBlockNum":"20",
            "GasLimit":"200000",
            "GasUsed":"0",
            "MbInfoHash":"37e4f0a90c6bcbc0132d839ba2ce19ccdb42916eda3a2899caeea08550d531d0",
            "MinerPubKey":"0x03F8CCD04CCFFB273AC3B9E5D7260AFFFE3024C03200B653AF99FCCBFBF2AA269A",
            "NumMicroBlocks":4,
            "NumTxns":0,
            "PrevBlockHash":"80ad8dc0494a04e5f5a182306893645ad18bb5b05ee2e8397dfb2f151f004703",
            "Rewards":"0",
            "StateDeltaHash":"0000000000000000000000000000000000000000000000000000000000000000",
            "StateRootHash":"24b9de6c00ae81db99079aa22e17ab72b1d9f9f6aab34b744931e9a2b3544c61",
            "Timestamp":"1545040322833958",
            "Type":1,
            "Version":0
        }
    }
}
```

Get the details of the most recent Transaction block.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetLatestTxBlock"
params | ""

## GetNumTxBlocks

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumTxBlocks",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":"1000"
}
```

Get the number of Transaction blocks in the network so far.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetNumTxBlocks"
params | ""

## GetTxBlockRate

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTxBlockRate",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":6.5499873692751224e-07
}
```

Get the current Transaction blockrate per second.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetTxBlockRate"
params | ""

## TxBlockListing

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "TxBlockListing",
    "params": [1]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "data":[
            {
                "BlockNum":1016,
                "Hash":"BBA0C358B0A578CFD5230E501B76A0D8C3E27D5E82524D8B3028B4D8D68AFD3A"
            },
            {
                "BlockNum":1015,
                "Hash":"F90074A2A50973C80DB358DEF8F6D39157ADAEF1C1634E88B66FD55230212FA7"
            },
            {
                "BlockNum":1014,
                "Hash":"C71C95A4AD784251F3BDBC157CAF87B941F0866A40C5AA2409B724AE55CC25BC"
            },
            {
                "BlockNum":1013,
                "Hash":"9A432A3BD743A1B31B839F1C0E61C4B1D7C3A983D767B8DB9833D7B9537BCCD7"
            },
            {
                "BlockNum":1012,
                "Hash":"141772BB18777685F55D2E8BEB1682357C0D4CD0E28680B8993C2D6B1CE685AE"
            },
            {
                "BlockNum":1011,
                "Hash":"092209AD966FFC928180C3A14F1CD4DBC1D065F167441FC2D31B471C612AE77D"
            },
            {
                "BlockNum":1010,
                "Hash":"7A1A580FEFD45947A4F5DDA1D75CAB96B8DCE15D9E6644DF3BF072F45C52D0F3"
            },
            {
                "BlockNum":1009,
                "Hash":"BDB10D71FF35EB607DC45FF283FD477568903D295B80F9380FCB39D11BE55336"
            },
            {
                "BlockNum":1008,
                "Hash":"E64E2E716D89410B06DF5E32846C4743A755836A35EF449C7955602DF4E60DD0"
            },
            {
                "BlockNum":1007,
                "Hash":"1FD23789E64D1645B7D03058AFCFEB7118A92578A59DA6604568B9B5987F9458"
            }
        ],
        "maxPages":102
    }
}
```

Get a paginated list of Transaction blocks. Pass in page number as parameter. Returns a `maxPages` variable that specifies the max number of pages. `1` being latest block.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "TxBlockListing"
params | Page number (of type `Int`) of the listings (`1` being the latest block).

## GetNumTransactions

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumTransactions",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":"19"
}
```

Get the number of Transactions in the network so far.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetNumTransactions"
params | ""

## GetTransactionRate

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTransactionRate",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":0
}
```

Get the current Transaction rate of the network.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetTransactionRate"
params | ""

## GetCurrentMiniEpoch

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetCurrentMiniEpoch",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":"1068"
}
```

Get the number of Transaction epochs in the network so far.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetCurrentMiniEpoch"
params | ""

## GetCurrentDSEpoch

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetCurrentDSEpoch",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":"22"
}
```

Get the number of DS epochs in the network so far.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetCurrentDSEpoch"
params | ""

## GetPrevDifficulty

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetPrevDifficulty",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":3
}
```

Get the minimum shard difficulty of the previous block.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetPrevDifficulty"
params | ""

## GetPrevDSDifficulty

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetPrevDSDifficulty",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":16
}
```

Get the minimum shard difficulty of the previous block.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetPrevDSDifficulty"
params | ""

# Transaction-related methods

## CreateTransaction

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "CreateTransaction",
    "params": [{
      "version": 1,
      "nonce": 1,
      "toAddr": "8AD0357EBB5515F694DE597EDA6F3F6BDBAD0FD9",
      "amount": "10000",
      "pubKey": "0205273e54f262f8717a687250591dcfb5755b8ce4e3bd340c7abefd0de1276574",
      "gasPrice": "1",
      "gasLimit": "10",
      "code": "",
      "data": "",
      "signature": "29ad673848dcd7f5168f205f7a9fcd1e8109408e6c4d7d03e4e869317b9067e636b216a32314dd37176c35d51f9d4c24e0e519ba80e66206457c83c9029a490d"
    }]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "Info":"Non-contract txn, sent to shard",
        "TranID":"2d1eea871d8845472e98dbe9b7a7d788fbcce226f52e4216612592167b89042c"
    }
}
```

Create a new Transaction. See [Quick Start](https://github.com/Zilliqa/Zilliqa-JavaScript-Library#quick-start) in javascript for an example of how to construct a transaction object.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "CreateTransaction"
params | An object containing the following properties:
------ | -----------------------------------------------
version | The current version of Zilliqa.
nonce | Counter equal to the number of transactions sent by the sender's account, including this one. It's value is = `current account nonce + 1`.
toAddr | Recipient's account address. For deploying new contracts, set this as `0000000000000000000000000000000000000000`.
amount | Transaction amount to be transferred to the destination address
pubKey | Public key of the sender.
gasPrice | An amount that the sender is willing to pay per unit of gas for computations incurred in transaction processing.
gasLimit | The maximum amount of gas that should be used while processing this transaction (For regular transaction, please use `1`. For smart contract transactions, please check out the [gas documentation](https://drive.google.com/file/d/1c0EJXELVe_MxhULPuJgwGvxFGenG7fmK/view?usp=sharing)).
code | **(optional)** String specifying the contract code. Present only when deploying a new contract.
data | **(optional)** Stringified JSON object specifying parameters to be passed to a contract for execution. Present when creating or calling a smart contract.
signature | an EC-Schnorr signature of the entire object

## GetTransaction

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTransaction",
    "params": ["AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "ID":"aaf3089596437a7c6984fa2627b6f38b5f5b80faeaac6993c2e82c6a8ee2615e",
        "amount":"0",
        "gasLimit":"50000",
        "gasPrice":"100",
        "nonce":"4",
        "receipt":{
            "cumulative_gas":"50",
            "success":false
        },
        "senderPubKey":"0x0237AECBF98D57A10DABB66A710B10844765A355645223AA2A2F77AA484228C03A","signature":"0xE44E0DDC6A968233C177FB27D6E326C69EB79A23DDEBBC5A70183039D34CCA39665B2C0526F164F9ADBB1810C8BE028EA17D5357F6BC4A7BCE676B6A96B8987B",
        "toAddr":"0000000000000000000000000000000000000000",
        "version":"0"
    }
}
```

Get details of a Transaction by its hash.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetTransaction"
params | Hash of the transaction to retrieve.

## GetRecentTransactions

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetRecentTransactions",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "TxnHashes": [
      "0e73effb72ddf7a164c69b559970f82e0ae846187a9223af7ced2a741c03f347",
      "43104643e5f35455b71f3cfcb471ce4a4c8b96e00f8e8b77733075662e5fc905",
      "271ac49c852f14fc286409811838840cde3febbeef96eb10cabf1b67fc5cd248",
      "c60ba6f3d374362e140edbfc0110304236d22bbac1a2e31fe62350a0305ed72d",
      "1b551314c9d0f911607e5fccf1115f858c246a12b505375c4a1df44183cac695",
      "36c932b0dc96618021ca778686572b8772a89ffdbbbe672b6df47dfb6dd6daa0",
      "c2f9cf7ae47b996c4fa9c137a8bfa905dce07f6a822f9b869159906a879e2e0e",
      "016b844b473d3a1296e6898036f8edfb1a722811ac8f476adad9320576764453",
      "dbb67c0c77e710e94ce16e91884dedbc127ccec5ec66068471a2da1ff8e4fded",
      "eb594f17752029887245acc3e6a534e565f8873778ab6513aba649b23c2a8e44",
      "6a6097826d05e5f71bec37bddaa8a40a5e35980b5839f84d3a99078ed6b029e4",
      "2ed27839f061e3e7fc0d4c33e7e24c5a706ddf33c805189845cc1101903398a7",
      "d517cd27523d6d51e6c7eedb0f8637ba7cdd1b5814b7ab5dfa7ab9e3f2314a38",
      "675daa74a79797b4d3c94e27149591b8cba5d97ccaa27a9962d560ef845dc42b",
      "6947ea29f71187d12a1968d25a221d62d113f5361ed9ae8378ece85014b77e80",
      "27a016dec19d3a126b75cf466f48d57548279ebb031917ed0d6727c473560bb5",
      "9532127876bd7761ec1ac40c62e1d23160cb0da42777591195091c8b5fd5367f",
      "4e946891a97c2aa6eed67ac7ab4738658db8cef13e7f66f0c2aa1572d7a30b7e",
      "962da9dd3b7e394b6ed79fb7b278c13202c34d4f2e167bb7bdd6f5b85ad802ae",
      "ace1376174f12adda4dcaa2ed01a48cf9e8c02419bdeab4477cd6d60f7239223",
    ],
    "number": 20
  }
}
```

Get the most recent transactions (up to `100`) accepted by the specified zilliqa node.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetRecentTransactions"
params | ""

## GetNumTxnsTxEpoch

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumTxnsTxEpoch",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":0
}
```

Get the number of transactions in this Transaction epoch.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetNumTxnsTxEpoch"
params | ""

## GetNumTxnsDSEpoch

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumTxnsDSEpoch",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":"0"
}
```

Get the number of transactions in this Directory Service epoch.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetNumTxnsDSEpoch"
params | ""

## GetMinimumGasPrice

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetMinimumGasPrice",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":"100"
}
```

Get the minimum gas price of the last DS epoch.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetMinimumGasPrice"
params | ""

# Contract-related methods

## GetSmartContractCode

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractCode",
    "params": ["fe001824823b12b58708bf24edd94d8b5e1cfcf7"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "code":"scilla_version 0\n\n    (* HelloWorld contract *)\n    \n    import ListUtils\n    \n    (***************************************************)\n    (*               Associated library                *)\n    (***************************************************)\n    library HelloWorld\n    \n    let one_msg = \n      fun (msg : Message) => \n      let nil_msg = Nil {Message} in\n      Cons {Message} msg nil_msg\n    \n    let not_owner_code = Int32 1\n    let set_hello_code = Int32 2\n    \n    (***************************************************)\n    (*             The contract definition             *)\n    (***************************************************)\n    \n    contract HelloWorld\n    (owner: ByStr20)\n    \n    field welcome_msg : String = \"\"\n    \n    transition setHello (msg : String)\n      is_owner = builtin eq owner _sender;\n      match is_owner with\n      | False =>\n        msg = {_tag : \"Main\"; _recipient : _sender; _amount : Uint128 0; code : not_owner_code};\n        msgs = one_msg msg;\n        send msgs\n      | True =>\n        welcome_msg := msg;\n        msg = {_tag : \"Main\"; _recipient : _sender; _amount : Uint128 0; code : set_hello_code};\n        msgs = one_msg msg;\n        send msgs\n      end\n    end\n    \n    \n    transition getHello ()\n        r <- welcome_msg;\n        e = {_eventname: \"getHello()\"; msg: r};\n        event e\n    end"
    }
}
```

Get the Scilla code of a smart contract address.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetSmartContractCode"
params | A smart contract address.

## GetSmartContractInit

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractInit",
    "params": ["fe001824823b12b58708bf24edd94d8b5e1cfcf7"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":[
        {
            "type":"Uint32",
            "value":"0",
            "vname":"_scilla_version"
        },
        {
            "type":"ByStr20",
            "value":"0x1eefc4f453539e5ee732b49eb4792b268c2f3908",
            "vname":"owner"
        },
        {
            "type":"BNum",
            "value":"1583",
            "vname":"_creation_block"
        }
    ]
}
```

Get the initialization parameters (immutable) of a given smart contract address.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetSmartContractInit"
params | A smart contract address.

## GetSmartContractState

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractState",
    "params": ["fe001824823b12b58708bf24edd94d8b5e1cfcf7"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":[
        {
            "type":"String",
            "value":"Hello World",
            "vname":"welcome_msg"
        },
        {
            "type":"Uint128",
            "value":"0",
            "vname":"_balance"
        }
    ]
}
```

Get the state variables (mutable) of a smart contract address.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetSmartContractState"
params | A smart contract address.

## GetSmartContracts

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContracts",
    "params": ["1eefc4f453539e5ee732b49eb4792b268c2f3908"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":[
        {
            "address":"6b3070b0abf4371b2b3b26e23f11f4c073b636e5",
            "state":[
                {
                    "type":"String",
                    "value":"Hello World",
                    "vname":"welcome_msg"
                },
                {
                    "type":"Uint128",
                    "value":"0",
                    "vname":"_balance"
                }
            ]
        },
        {
            "address":"13cf0f8c1ea003779df0b7fa08a97903bc760e80",
            "state":[
                {
                    "type":"String",
                    "value":"Hello World",
                    "vname":"welcome_msg"
                },
                {
                    "type":"Uint128",
                    "value":"0",
                    "vname":"_balance"
                }
            ]
        }
    ]
}
```

Get the list of smart contracts created by an address.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetSmartContracts"
params | A account address.

## GetContractAddressFromTransactionID

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetContractAddressFromTransactionID",
    "params": ["AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":"c458f39c106582c1a49bac6bc76ec603e2ae0497"
}
```

Get a smart contract address from a transaction ID.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetContractAddressFromTransactionID"
params | A Transaction ID.

# Account-related methods

## GetBalance

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetBalance",
    "params": ["1eefc4f453539e5ee732b49eb4792b268c2f3908"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "balance":"18446744073637511711",
        "nonce":16
    }
}
```

Get the balance of an account address.

### HTTP Request

+ **_Maoshanwang_ Testnet:** `POST "https://api.zilliqa.com/"`
+ **Scilla Testnet:** `POST "https://api-scilla.zilliqa.com/"`
+ **Local:** `POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
id | 1
jsonrpc | "2.0"
method | "GetBalance"
params | ""
