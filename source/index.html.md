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

[JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC) is a remote procedure call protocol encoded in JSON. You can use this API to access data in Zilliqa nodes. The JSON-RPC API server runs on port 4201 on a Zilliqa lookup node. All API calls are POST requests made to port 4201 of the machine running the zilliqa node.

All requests follow the standard json-rpc format and include 4 variables in the data object:
```
id: (eg "1")
jsonrpc: "" (eg "2.0")
method: "" (eg "GetBalance")
params: "" (eg ["1"])
```
Code examples using curl can be viewed in the dark area to the right.

# JSON-RPC API

## GetBalance

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetBalance",
    "params": ["c5a829596fb06a59e2b1ddb6589811c759025d52"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "balance": "99930",
    "nonce": 1
  }
}
```

Get the balance and nonce of a given address.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | address to fetch balance and nonce of
method | "GetBalance"
jsonrpc | "2.0"
id | 1


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
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "header": {
      "blockNum": "1",
      "difficulty": 20,
      "leaderPubKey": "0x020273D5EF4691D8EB3DFAB0ACCB213ADE94482B49972841E0F85A3BC49BC982BD",
      "minerPubKey": "0x03F9BD182E4FC260E04630C2F5F2EDD2883A50772535EDCA6D001A4548730B8D07",
      "nonce": "1530868960",
      "prevhash": "6babe1baa82cf5625c33970b8c7dc0f6ae8f5d0f21575efdf2733e3ecef34c78",
      "timestamp": "1530868880252432"
    },
    "signature": "BBD6719CC3E2904FDB0270766A95CC2BFBEE0B1D6055E741167D7E138A30C313025700D9B07F79B504CF6729D4D56E2FB1008843935BE74E8BCDAB4B7B2EAF75"
  }
}
```

Get details of a Directory Service block by block number.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | Block number to fetch details of
method | "GetDsBlock"
jsonrpc | "2.0"
id | 1


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
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "body": {
      "HeaderSign": "88145A9EE6EAF8CD4C7DC05E8AE559E09E68E990A9D35C51C97895E3ECA252B6338DF929033CA3B68669D3757EA1EA71565B942B6E4D93F9C509BE7D6B1A92B8",
      "MicroBlockEmpty": [
        1
      ],
      "MicroBlockHashes": [
        "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855"
      ]
    },
    "header": {
      "BlockNum": "100",
      "DSBlockNum": "3",
      "GasLimit": "100",
      "GasUsed": "1",
      "MinerPubKey": "0x035D872C9F1F2E4113806E34C2114988BC72229015D7EAE4E25CBF27F8ED9A51D7",
      "NumMicroBlocks": 1,
      "NumTxns": 0,
      "StateHash": "0000000000000000000000000000000000000000000000000000000000000000",
      "Timestamp": "1530871942103501",
      "TxnHash": "5df6e0e2761359d30a8275058e299fcc0381534545f55cf43e41983f5d4c9456",
      "prevBlockHash": "b6bace0e25f41be5219775db06f8eb4ef2f28b5f041c121128fb050c96c29d22",
      "type": 1,
      "version": 0
    }
  }
}
```

Get details of a Transaction block by block number.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | Block number to fetch details of
method | "GetTxBlock"
jsonrpc | "2.0"
id | 1


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
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "header": {
      "blockNum": "206",
      "difficulty": 20,
      "leaderPubKey": "0x036020EA88FF75732CC11A4CA60BAB9F44152D751B01761D679E3E4104B931AAA4",
      "minerPubKey": "0x02EB7B0B281AC6AEC919E9D1DB24FDE6D34C847AD636C7971A8A669C8433494C0E",
      "nonce": "1531327584",
      "prevhash": "23d514e64f4f1c7f878eacc239fd7d3e78c1860bcb89ca3e2798ba80b5f62cfb",
      "timestamp": "1531327643176242"
    },
    "signature": "3500578665026049D607CBA2C5BA7C06A412A1F7610E46C0310E158C82E76FCDEB13B47473ECE31CB2D434336B65421F42F7EDB2D2009AB582D5BF14085D7702"
  }
}
```

Get details of the most recent Directory Service block.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | empty string
method | "GetLatestDsBlock"
jsonrpc | "2.0"
id | 1


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
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "body": {
      "HeaderSign": "10D566A9FFEBF3029DEE6BEACE8CCE8891475978828F7FE3EEC593E5D6A7D363EE8B5D683B7E086C7CE67904C0F7CFBB6B06773A7E16D694D8AC68DCEE018B47",
      "MicroBlockEmpty": null,
      "MicroBlockHashes": null
    },
    "header": {
      "BlockNum": "10268",
      "DSBlockNum": "206",
      "GasLimit": "0",
      "GasUsed": "0",
      "MinerPubKey": "0x02EB7B0B281AC6AEC919E9D1DB24FDE6D34C847AD636C7971A8A669C8433494C0E",
      "NumMicroBlocks": 0,
      "NumTxns": 0,
      "StateHash": "0000000000000000000000000000000000000000000000000000000000000000",
      "Timestamp": "1531328919047014",
      "TxnHash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
      "prevBlockHash": "833cc52f7daf62abc4542fbaaae5994ba063e3a74f08bb164a464c2b14e24edc",
      "type": 1,
      "version": 0
    }
  }
}
```

Get details of the most recent Transaction block.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | empty string
method | "GetLatestTxBlock"
jsonrpc | "2.0"
id | 1


## GetTransaction

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTransaction",
    "params": ["43104643E5F35455B71F3CFCB471CE4A4C8B96E00F8E8B77733075662E5FC905"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "ID": "43104643e5f35455b71f3cfcb471ce4a4c8b96e00f8e8b77733075662e5fc905",
    "amount": "0",
    "nonce": "3",
    "senderPubKey": "0x02DFB1F0B14A1C81EE2D31F43B223FF88207FFCB193F1D01BA38C01DF1DBF0F1FF",
    "signature": "0x6F52EC8D6B5EC50CB83C57584E3DD33593FE15E7E4AFDCF4D2053586C0D2E4A43ED44A4E87BB6E726E097A02D888320983902578D621BE20804364F008A66DAC",
    "toAddr": "50e9247a39e87a734355a203666ff7415c8a0802",
    "version": "0"
  }
}
```

Get details of a Transaction by its hash.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | hash of the transaction to retrieve
method | "GetTransaction"
jsonrpc | "2.0"
id | 1


## CreateTransaction

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "CreateTransaction",
    "params": [{
      "version": 0,
      "nonce": 5,
      "to": "c5a829596fb06a59e2b1ddb6589811c759025d52",
      "amount": 83,
      "pubKey": "026ad7a7cb2aa230af177ca0ea3c4112a902d296bf7a5f25f5ae4b3df72321f4d0",
      "gasPrice": 1,
      "gasLimit": 1,
      "code": "",
      "data": "",
      "signature": "508b838641a6d0f9a7114c5b359a3a6119072e213b06b0f3331f4a33a8c80cde09d3aa7f64c3d767024ab56abbcb2ebd553085d214133c0383d4007828bde0c4"
    }]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "a5e238bca907c28d015e50acc76788f8bad79882bf40459215722c414a7b940b"
}
```

Create a new Transaction. See [zilliqajs.util.createTransactionJson()](https://github.com/Zilliqa/Zilliqa-JavaScript-Library/#createtransactionjson) in javascript for an example of how to construct the transaction object.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | object containing the following properties:
version | the current version
nonce | counter equal to the number of transactions sent by the transaction sender including this one. It's value is (current account nonce + 1)
to | destination account address. Incase of new contract account, set as 0000000000000000000000000000000000000000
amount | transaction amount to be transferred to the destination address
pubKey | object
gasPrice | amount that the sender is willing to pay per unit of gas for computations incurred in transaction processing (default 1)
gasLimit | the maximum amount of gas that should be used while processing this transaction (1 - regular transaction, 10 - invoke method, 50 - deploy contract)
code | (optional) string specifying the contract code. Present only when creating a new contract account
data | (optional) stringified JSON object specifying initialization parameters. Present when creating or calling a contract account
signature | an EC-Schnorr signature of the entire object (see )
method | "CreateTransaction"
jsonrpc | "2.0"
id | 1


## GetSmartContracts

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContracts",
    "params": ["c5a829596fb06a59e2b1ddb6589811c759025d52"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": [
    {
      "address": "50e9247a39e87a734355a203666ff7415c8a0802",
      "state": [
        {
          "type": "String",
          "value": "\"TESTING\"",
          "vname": "welcome_msg"
        },
        {
          "type": "Uint128",
          "value": "0",
          "vname": "_balance"
        }
      ]
    }
  ]
}
```

Get the list of smart contracts created by an address.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | address that deployed the smart contracts
method | "GetSmartContracts"
jsonrpc | "2.0"
id | 1


## GetSmartContractState

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractState",
    "params": ["50e9247a39e87a734355a203666ff7415c8a0802"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": [
    {
      "type": "String",
      "value": "\"TESTING\"",
      "vname": "welcome_msg"
    },
    {
      "type": "Uint128",
      "value": "0",
      "vname": "_balance"
    }
  ]
}
```

Get the state variables (mutable) of a smart contract address.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | address of the smart contract
method | "GetSmartContractState"
jsonrpc | "2.0"
id | 1


## GetSmartContractCode

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractCode",
    "params": ["50e9247a39e87a734355a203666ff7415c8a0802"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc":"2.0",
  "result": {
    "code": "(* HelloWorld contract *)\n\n\n(***************************************************)\n(*               Associated library                *)\n(***************************************************)\nlibrary HelloWorld\n\nlet one_msg = \n  fun (msg : Message) => \n  let nil_msg = Nil {Message} in\n  Cons {Message} msg nil_msg\n\nlet not_owner_code = Int32 1\nlet set_hello_code = Int32 2\n\n(***************************************************)\n(*             The contract definition             *)\n(***************************************************)\n\ncontract HelloWorld\n(owner: Address)\n\nfield welcome_msg : String = \"\"\n\ntransition setHello (msg : String)\n  is_owner = builtin eq owner _sender;\n  match is_owner with\n  | False =>\n    msg = {_tag : \"Main\"; _recipient : _sender; _amount : Uint128 0; code : not_owner_code};\n    msgs = one_msg msg;\n    send msgs\n  | True =>\n    welcome_msg := msg;\n    msg = {_tag : \"Main\"; _recipient : _sender; _amount : Uint128 0; code : set_hello_code};\n    msgs = one_msg msg;\n    send msgs\n  end\nend\n\n\ntransition getHello ()\n    r <- welcome_msg;\n    msg = {_tag : \"Main\"; _recipient : _sender; _amount : Uint128 0; msg : r};\n    msgs = one_msg msg;\n    send msgs\nend"
  }
}
```

Get the Scilla code of a smart contract address.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | address of the smart contract
method | "GetSmartContractCode"
jsonrpc | "2.0"
id | 1


## GetSmartContractInit

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractInit",
    "params": ["50e9247a39e87a734355a203666ff7415c8a0802"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": [
    {
      "type": "Address",
      "value": "0xc5a829596fb06a59e2b1ddb6589811c759025d52",
      "vname": "owner"
    }
  ]
}
```

Get the initialization parameters (immutable) of a given smart contract address.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | address of the smart contract
method | "GetSmartContractInit"
jsonrpc | "2.0"
id | 1


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
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "CurrentDSEpoch": "0",
    "CurrentMiniEpoch": "1",
    "DSBlockRate": 0,
    "NumDSBlocks": "1",
    "NumPeers": 0,
    "NumTransactions": "0",
    "NumTxBlocks": "1",
    "NumTxnsDSEpoch": "0",
    "NumTxnsTxEpoch": 0,
    "ShardingStructure": {
      "Error": "No shards yet"
    },
    "TransactionRate": 0,
    "TxBlockRate": 0
  }
}
```

Get statistics about the specified zilliqa node.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | empty string
method | "GetBlockchainInfo"
jsonrpc | "2.0"
id | 1


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

Get the network ID of the specified zilliqa node.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | empty string
method | "GetNetworkId"
jsonrpc | "2.0"
id | 1


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

Get the most recent transactions (upto 100) accepted by the specified zilliqa node.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | empty string
method | "GetRecentTransactions"
jsonrpc | "2.0"
id | 1


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

Get a paginated list of Directory Service blocks. Pass in page number as parameter. Returns a `maxPages` variable that specifies the max number of pages. 1 - latest blocks, maxPages - oldest blocks.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | int page number of listing (1 - latest blocks)
method | "DSBlockListing"
jsonrpc | "2.0"
id | 1


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
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "data": [
      {
        "BlockNum": 10372,
        "Hash": "39B5EB8B27F11B984C67CB4B0A0F3D69508ACDE3D37CCAC3423D19321C8841B8"
      },
      {
        "BlockNum": 10371,
        "Hash": "D674075909123DC098BF1B40C1BCFD1C760B2E6683557ACA436F7FB55F34F30F"
      },
      {
        "BlockNum": 10370,
        "Hash": "EB342667A123EBCD4209062040B25D26D264CDD2B9D76DC7952A5E2BC7C10B60"
      },
      {
        "BlockNum": 10369,
        "Hash": "2E2568D1E1A683ACDA7784DB1943C5CF41234501AE2DF6292D343956DA9E730E"
      },
      {
        "BlockNum": 10368,
        "Hash": "85A377D576EA6F9E4B5A2B8F84BB199060F45278F632F7B3A90FF847C0FD4952"
      },
      {
        "BlockNum": 10367,
        "Hash": "786E5E3B8575BAF417811D93A3173DA2EE084C8230E403ACB435C2EFD1409E27"
      },
      {
        "BlockNum": 10366,
        "Hash": "76276ACF59262ECC6C2D7BB04BCCFDB2B939284F923A9A54551EAB53106E542E"
      },
      {
        "BlockNum": 10365,
        "Hash": "9305905F36F17EE2F3E11B43E22AB654FF0E25C9CB867100235345EFEFD9B642"
      },
      {
        "BlockNum": 10364,
        "Hash": "41A0EFD2FC1705EC8E91C82E58BB7C238A8D8E3EA16A3D2486459C2C01172972"
      },
      {
        "BlockNum": 10363,
        "Hash": "E0C27AFA17B9F3EB84FBF6B0E2EC874DE1578ADF9C0258C23289AB1FAB0090D0"
      }
    ],
    "maxPages": 1038
  }
}
```

Get a paginated list of Transaction blocks. Pass in page number as parameter. Returns a `maxPages` variable that specifies the max number of pages. 1 - latest blocks, maxPages - oldest blocks.

### HTTP Request

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | int page number of listing (1 - latest blocks)
method | "TxBlockListing"
jsonrpc | "2.0"
id | 1

