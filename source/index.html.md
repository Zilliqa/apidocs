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

[JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC) is a remote procedure call protocol encoded in JSON. You can use this API to access data in Zilliqa nodes. The JSON-RPC API server runs on port 4201 on a Zilliqa lookup node. All API calls are POST requests made to port 4201 of the machine running the Zilliqa node.

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
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "body":{
            "HeaderSign":"AFD7E0A37D6BDC62B5B2C8D4318A8921C917532D5F285FAE9F78FB1DA819771474A1CB130BFBD1B867333A2E66E12B2A7242D720702B56F6544574BD8AABCD91",
            "MicroBlockEmpty":[1,1,1,1],
            "MicroBlockHashes":[
                "c7deb25b595bb978b48d1219cb19415585b664b180046fd2adde242827f2c805",
                "3d01bbd8658bd07543be34f699102262a0113628e8b869eee4d62c6a687b20d7",
                "99116f739cd1d58a15f20dae32f8c836042b15e946034230d7df6160e9b29b0d",
                "dd8cd4bffcdd34708d18bb49c4da4fcb65b2e39ce7558139543684d623a3b01a"
            ]
        },
        "header":{
            "BlockNum":"100",
            "DSBlockNum":"3",
            "GasLimit":"200000",
            "GasUsed":"0",
            "MinerPubKey":"0x02271D3B7B7052C0A0A000A21B08E8AB34F4ED6FC8E7DF7CE32CAE84709102C639",
            "NumMicroBlocks":4,
            "NumTxns":0,
            "PrevBlockHash":"af52c80ef9f91d24a614fb18695cc99475c03930d65a55c4146b52c64206ec28",
            "Rewards":"0",
            "StateHash":"e81b45cbd0e2f3a09b69ba3b5adeecacc06841ea75f9001cf5d391b469f3c4ce",
            "Timestamp":"1542364977362827",
            "TxnHash":"2f6fe4ae2c67516aeb9214b4befd4d1e29c0023b74b4f2c043fe114353cb2ffe",
            "Type":1,
            "Version":0
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
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "body":{
            "HeaderSign":"A4FCCC5AD9EDBE365B082EE3AB2350396F1159000611A4833C60132373CBE8359D84CF675DCBB9941A650B8252AE355234153A04E9E1050C89391D97A012DDE7",
            "MicroBlockEmpty":[1,1],
            "MicroBlockHashes":[
                "0bab8255044b971724af7fb4dd61b9f26267170d9cffc1f02344e1ac9dd95243",
                "e807e00ed230a0f2e55b34a2771e4f5e3805f5b690d3891bb6b3c77cd2042b32"
            ]
        },
        "header":{
            "BlockNum":"4054",
            "DSBlockNum":"82",
            "GasLimit":"100000",
            "GasUsed":"0",
            "MinerPubKey":"0x0347ADF217C1EA8AE0506EA0125DF5BBA544896C46DF768A493555857961CE1715",
            "NumMicroBlocks":2,
            "NumTxns":0,
            "PrevBlockHash":"67b4c69df286ccf59e553d6fb15935895e71bf6c402dfc9cf89f422878140877",
            "Rewards":"0",
            "StateHash":"2d31fb48605005bb31dcff8b63b4c8bc76aaded7006c8b5f7121305f1382feee",
            "Timestamp":"1542430362519960",
            "TxnHash":"7f55d7f6f8f8a00e2dc2aa09ec0366fcd64510bdd452a7eb2fa0d706d11271ab",
            "Type":1,
            "Version":0
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
    "params": ["2d1eea871d8845472e98dbe9b7a7d788fbcce226f52e4216612592167b89042c"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "ID":"2d1eea871d8845472e98dbe9b7a7d788fbcce226f52e4216612592167b89042c",
        "amount":"10000",
        "gasLimit":"10",
        "gasPrice":"1",
        "nonce":"13",
        "receipt":{
            "cumulative_gas":"1",
            "success":true
        },
        "senderPubKey":"0x0205273E54F262F8717A687250591DCFB5755B8CE4E3BD340C7ABEFD0DE1276574",
        "signature":"0x29AD673848DCD7F5168F205F7A9FCD1E8109408E6C4D7D03E4E869317B9067E636B216A32314DD37176C35D51F9D4C24E0E519BA80E66206457C83C9029A490D",
        "toAddr":"8ad0357ebb5515f694de597eda6f3f6bdbad0fd9",
        "version":"1"
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
      "version": 1,
      "nonce": 13,
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

`POST http://localhost:4201/`

### Data Parameters

Parameter | Description
--------- | -------------
params | object containing the following properties:
version | the current version
nonce | counter equal to the number of transactions sent by the transaction sender including this one. It's value is (current account nonce + 1)
toAddr | destination account address. Incase of new contract account, set as 0000000000000000000000000000000000000000
amount | transaction amount to be transferred to the destination address
pubKey | object
gasPrice | amount that the sender is willing to pay per unit of gas for computations incurred in transaction processing (default 1)
gasLimit | the maximum amount of gas that should be used while processing this transaction (1 - regular transaction, 10 - invoke method, 50 - deploy contract)
code | (optional) string specifying the contract code. Present only when creating a new contract account
data | (optional) stringified JSON object specifying initialization parameters. Present when creating or calling a contract account
signature | an EC-Schnorr signature of the entire object
method | "CreateTransaction"
jsonrpc | "2.0"
id | 1


## GetSmartContracts

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContracts",
    "params": ["8254B2C9ACDF181D5D6796D63320FBB20D4EDD12"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":[
        {
            "address":"dd2f86fd33fddcb237447642963627d9d1297295",
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
            "address":"fa22b2c24ea3868de5c9bcb843c87104f0fd45dc",
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
    "params": ["dd2f86fd33fddcb237447642963627d9d1297295"]
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
    "params": ["dd2f86fd33fddcb237447642963627d9d1297295"]
}' -H "Content-Type: application/json" -X POST "https://api-scilla.zilliqa.com/"
```

> The above command returns JSON structured like this:

```json
{
    "id":"1",
    "jsonrpc":"2.0",
    "result":[
        {
            "type":"ByStr20",
            "value":"0x8254b2c9acdf181d5d6796d63320fbb20d4edd12",
            "vname":"owner"
        },
        {
            "type":"BNum",
            "value":"5169",
            "vname":"_creation_block"
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
    "id":"1",
    "jsonrpc":"2.0",
    "result":{
        "CurrentDSEpoch":"84",
        "CurrentMiniEpoch":"4167",
        "DSBlockRate":0.001240451642236594,
        "NumDSBlocks":"85",
        "NumPeers":20,
        "NumTransactions":"15",
        "NumTxBlocks":"4167",
        "NumTxnsDSEpoch":"0",
        "NumTxnsTxEpoch":0,
        "ShardingStructure":{
            "NumPeers":[10]
        },
        "TransactionRate":0,
        "TxBlockRate":0.060601745931509736
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

