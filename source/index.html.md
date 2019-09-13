---
title: Zilliqa JSON-RPC API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript: node.js
  - java: java
  - ruby: ruby
  - python: python

toc_footers:
  - <a href='https://github.com/Zilliqa/Zilliqa-Javascript-Library'>Javascript SDK</a>
  - <a href='https://github.com/FireStack-Lab/LaksaJ'>Java SDK</a>
  - <a href='https://github.com/FireStack-Lab/LaksaRuby'>Ruby SDK</a>
  - <a href='https://github.com/deepgully/pyzil'>Python SDK</a>
  - <a href='http://scilla.readthedocs.io/'>Scilla Documentation</a>

includes:

search: true
---

# Introduction

[JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC) is a remote procedure call protocol encoded in JSON. You can use this API to access data from the Zilliqa nodes.
The JSON-RPC API server runs on:

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

All API calls are POST requests.

All requests follow the standard JSON-RPC format and include 4 variables in the data object:

| Data object | Example             |
| ----------- | :------------------ |
| `id`        | e.g. `"1"`          |
| `jsonrpc`   | e.g. `"2.0"`        |
| `method`    | e.g. `"GetBalance"` |
| `params`    | e.g. `["1"]`        |

# Blockchain-related methods

## GetNetworkId

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNetworkId",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const NetworkId = await zilliqa.network.GetNetworkId();
console.log(NetworkId);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<String> networkId = client.getNetworkId();
        System.out.println(new Gson().toJson(networkId));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetNetworkId
puts ret
```

```python
from pyzil.zilliqa import chain
from pyzil.zilliqa.api import ZilliqaAPI


# EITHER
chain.set_active_chain(chain.MainNet)
network_id = chain.active_chain.api.GetNetworkId()
print(network_id)

# OR
new_api = ZilliqaAPI(endpoint="https://api.zilliqa.com")
network_id = new_api.GetNetworkId()
print(network_id)

```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "1"
}
```

Returns the `CHAIN_ID` of the specified network. This is represented as a `String`. <br> See table below for the `CHAIN_ID` for different chains:

| Chain(s)              | `CHAIN_ID` |
| --------------------- | ---------- |
| **Zilliqa Mainnet**   | `1`        |
| **Developer testnet** | `333`      |

**NOTE:** `CHAIN_ID` from `2` to `9` are reserved for Zilliqa Core use.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description       |
| --------- | ------ | -------- | ----------------- |
| `id`      | string | Required | `"1"`             |
| `jsonrpc` | string | Required | `"2.0"`           |
| `method`  | string | Required | `"GetNetworkId"`  |
| `params`  | string | Required | Empty string `""` |

## GetBlockchainInfo

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetBlockchainInfo",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const blockChainInfo = await zilliqa.blockchain.getBlockChainInfo();
console.log(blockChainInfo.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<BlockchainInfo> blockchainInfo = client.getBlockchainInfo();
        System.out.println(new Gson().toJson(blockchainInfo));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetBlockchainInfo
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetBlockchainInfo())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "CurrentDSEpoch": "10",
    "CurrentMiniEpoch": "906",
    "DSBlockRate": 0.0001324694641012551,
    "NumDSBlocks": "11",
    "NumPeers": 2400,
    "NumTransactions": "1114482",
    "NumTxBlocks": "906",
    "NumTxnsDSEpoch": "15750",
    "NumTxnsTxEpoch": "5250",
    "ShardingStructure": {
      "NumPeers": [600, 600, 600]
    },
    "TransactionRate": 92.51249993656286,
    "TxBlockRate": 0.010826202125962327
  }
}
```

Returns the current network statistics for the specified network.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description           |
| --------- | ------ | -------- | --------------------- |
| `id`      | string | Required | `"1"`                 |
| `jsonrpc` | string | Required | `"2.0"`               |
| `method`  | string | Required | `"GetBlockchainInfo"` |
| `params`  | string | Required | Empty string `""`     |

## GetDsBlock

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetDsBlock",
    "params": ["1"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const dsBlock = await zilliqa.blockchain.getDSBlock("1");
console.log(dsBlock.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<DsBlock> dsBlock = client.getDsBlock("1");
        System.out.println(new Gson().toJson(dsBlock));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetDsBlock("1")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetDsBlock("1"))
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "header": {
      "BlockNum": "1",
      "Difficulty": 3,
      "DifficultyDS": 5,
      "GasPrice": "100",
      "LeaderPubKey": "0x0208EA17FE78DE1D4A17B921B7ADB2B3FEE4C795FC5FD54BEA80FCE926F09F79F3",
      "PoWWinners": [
        "0x0307BA09F607D36C6D3B2AC7541592DB8674A889690A14B816FACF67B4F9221CEC",
        "0x0342081E95907022E1E5A525F2D7CE51EB5AF56B7EB13C29C6EC194FB93DF2E752"
      ],
      "PrevHash": "ba127538d2c63eec121629011ae8173210589689dca54d1e11904dd82c68e9da",
      "Timestamp": "1544755380363821"
    },
    "signature": "E2EC67C64323D73D8CCBCC79FEEE04826702751D599995B997AFF7452A7CB7D11CEA8DC5275E9CEAAF7C623F2FEEE132A5F2EF5B9EB63D8C4C5CDD97D64B6CC3"
  }
}
```

Returns the details of a specified Directory Service block.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                         |
| --------- | ------ | -------- | --------------------------------------------------- |
| `id`      | string | Required | `"1"`                                               |
| `jsonrpc` | string | Required | `"2.0"`                                             |
| `method`  | string | Required | `"GetDsBlock"`                                      |
| `params`  | string | Required | Specifed DS block number to return. Example: `"40"` |

## GetLatestDsBlock

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetLatestDsBlock",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const dsBlock = await zilliqa.blockchain.getLatestDSBlock();
console.log(dsBlock.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<DsBlock> dsBlock = client.getLatestDsBlock();
        System.out.println(new Gson().toJson(dsBlock));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetLatestDsBlock
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetLatestDsBlock())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "header": {
      "BlockNum": "26",
      "Difficulty": 3,
      "DifficultyDS": 16,
      "GasPrice": "100",
      "LeaderPubKey": "0x020C11D6B9CA45B56EC80705F1070D9928CFA4BA99212BEF934307C228ECC309FC",
      "PoWWinners": [
        "0x02CB5328E79387F337EC671ECFF0CF2501CCD4DDFCA3565640F94792DE0A7EA0F9",
        "0x0320D26B67A1C701377AA391F2572B66D72F5D0E1A23C44E5B1DA7BF2D53C653E1"
      ],
      "PrevHash": "449a67f3cb160f598ac279f95e6583868a2052c846123558866f56dd6d70cd6c",
      "Timestamp": "1544776175498144"
    },
    "signature": "D096A9F6FB4DAFCFE7112D1C9684CAC2338CDBF0FC17E2B9DF814751BEA8E1F84A889DBC0CEBF903BFD06B1E0C0165F29347EED51B86A613F3C5A18F1CA11EEA"
  }
}
```

Returns the details of the most recent Directory Service block.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description          |
| --------- | ------ | -------- | -------------------- |
| `id`      | string | Required | `"1"`                |
| `jsonrpc` | string | Required | `"2.0"`              |
| `method`  | string | Required | `"GetLatestDsBlock"` |
| `params`  | string | Required | Empty string `""`    |

## GetNumDSBlocks

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumDSBlocks",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const numDsBlock = await zilliqa.blockchain.getNumDSBlocks();
console.log(numDsBlock.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<String> numDSBlocks = client.getNumDSBlocks();
        System.out.println(new Gson().toJson(numDSBlocks));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetNumDSBlocks
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumDSBlocks())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "27"
}
```

Returns the current number of validated Directory Service blocks in the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description        |
| --------- | ------ | -------- | ------------------ |
| `id`      | string | Required | `"1"`              |
| `jsonrpc` | string | Required | `"2.0"`            |
| `method`  | string | Required | `"GetNumDSBlocks"` |
| `params`  | string | Required | Empty string `""`  |

## GetDSBlockRate

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetDSBlockRate",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const dsBlockRate = await zilliqa.blockchain.getDSBlockRate();
console.log(dsBlockRate.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<Double> dsBlockRate = client.getDSBlockRate();
        System.out.println(new Gson().toJson(dsBlockRate));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetDSBlockRate
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetDSBlockRate())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 1.9217623126238637e-8
}
```

Returns the current Directory Service blockrate per second.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description        |
| --------- | ------ | -------- | ------------------ |
| `id`      | string | Required | `"1"`              |
| `jsonrpc` | string | Required | `"2.0"`            |
| `method`  | string | Required | `"GetDSBlockRate"` |
| `params`  | string | Required | Empty string `""`  |

## DSBlockListing

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "DSBlockListing",
    "params": [1]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const dsBlockListing = await zilliqa.blockchain.getDSBlockListing(1);
console.log(dsBlockListing.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<BlockList> blockListing = client.getDSBlockListing(1);
        System.out.println(new Gson().toJson(blockListing));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetDSBlockListing(1)
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetDSBlockListing(1))
```

> **Example response:**

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

Returns a paginated list of up to **10** Directory Service (DS) blocks and their block hashes for a specified page. The `maxPages` variable that specifies the maximum number of pages available is also returned.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                |
| --------- | ------ | -------- | ---------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                      |
| `jsonrpc` | string | Required | `"2.0"`                                                    |
| `method`  | string | Required | `"DSBlockListing"`                                         |
| `params`  | number | Required | Specifed page of DS blocks listing to return. Example: `1` |

## GetTxBlock

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTxBlock",
    "params": ["40"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const txBlock = await zilliqa.blockchain.getTxBlock("40");
console.log(txBlock.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<TxBlock> txBlock = client.getTxBlock("40");
        System.out.println(new Gson().toJson(txBlock));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetTxBlock("40")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTxBlock("40"))
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "body": {
      "BlockHash": "79fdf67632c9f793650955297c860d021c3241f2b448120747ee8fe502c03e54",
      "HeaderSign": "CB8290232ECE38030EAD865859A77616BD10738D79D6335F003427C6118C1CBFEC94D33183A73D5E8877361582748D2EEC895722066D390E79119B8E2DC3411D",
      "MicroBlockInfos": [
        {
          "MicroBlockHash": "97ab843bfd7a520f65c16667a8700ba11a886cc130254258e155d48be3ee3fb5",
          "MicroBlockShardId": 0,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        },
        {
          "MicroBlockHash": "120d3f2c76e1c55b6adb3e78aa3aa1c34e618fd3023069420dd1dcd79689cd50",
          "MicroBlockShardId": 1,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        },
        {
          "MicroBlockHash": "3fbae433e0e5c30ab89ec75cd32276dd49581941c7d0fc318503ca55693a9aed",
          "MicroBlockShardId": 2,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        }
      ]
    },
    "header": {
      "BlockNum": "40",
      "DSBlockNum": "1",
      "GasLimit": "1500000",
      "GasUsed": "0",
      "MbInfoHash": "dcb2c79d8fd7021634039e49578c1e7415f4a6aa9586043db3f488a34e6846ff",
      "MinerPubKey": "0x020035B739426374C5327A1224B986005297102E01C29656B8B086BF4B352C6CA9",
      "NumMicroBlocks": 3,
      "NumTxns": 0,
      "PrevBlockHash": "b87e9f526ffbaa653fcb9b2db731f53c65420f12ace6d88bd2753f816650bdb5",
      "Rewards": "0",
      "StateDeltaHash": "0000000000000000000000000000000000000000000000000000000000000000",
      "StateRootHash": "77ebb9cce52b0e1bc8ce1c0e5669e88f5018bd986d01339960ba07882b63ed79",
      "Timestamp": "1548930491181914",
      "Version": 1
    }
  }
}
```

Returns the details of a specified Transaction block.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                         |
| --------- | ------ | -------- | --------------------------------------------------- |
| `id`      | string | Required | `"1"`                                               |
| `jsonrpc` | string | Required | `"2.0"`                                             |
| `method`  | string | Required | `"GetTxBlock"`                                      |
| `params`  | string | Required | Specifed TX block number to return. Example: `"40"` |

## GetLatestTxBlock

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetLatestTxBlock",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const txBlock = await zilliqa.blockchain.getLatestTxBlock();
console.log(txBlock.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<TxBlock> txBlock = client.getLatestTxBlock();
        System.out.println(new Gson().toJson(txBlock));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetLatestTxBlock
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetLatestTxBlock())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "body": {
      "BlockHash": "794ded1feff2bed53432e5c77dbb30310d1003e5605bbbfad4e7dd08e7a1664b",
      "HeaderSign": "8BFA12F57C05F994650C56FF718D8EDD2AD9B00464091E76902CF2815F1FD5CFBD093BDD89FB2ABA6C4EAC4DAEAD8B8D0E74834758BA0160066C899D89EA2073",
      "MicroBlockInfos": [
        {
          "MicroBlockHash": "d7d2c88d699478946d3d25b3ca8effcf8b575da526a6741c3e87330f7144cf6d",
          "MicroBlockShardId": 0,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        },
        {
          "MicroBlockHash": "1f89fd6c178f1c5b8f5f0af8a2d3026af43e9ddcbe66ca760b07d00e3660f432",
          "MicroBlockShardId": 1,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        },
        {
          "MicroBlockHash": "0a68a175bd6a76a597fdcad1c1b7aed21ce3d55a3ccaa82cd3d72a8097ec0178",
          "MicroBlockShardId": 2,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        },
        {
          "MicroBlockHash": "ba899867e5cb2bc5bba0f186f24fb6a5cdd73718af740d37fd87128b0b89245e",
          "MicroBlockShardId": 3,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        }
      ]
    },
    "header": {
      "BlockNum": "157264",
      "DSBlockNum": "1573",
      "GasLimit": "2000000",
      "GasUsed": "0",
      "MbInfoHash": "4251b1b2f76235b637eee21fa197b411a08d1390ab06ff37d34deaf73e26f9e2",
      "MinerPubKey": "0x0211CDC4EE0AC1D3EFBD9597C970A32F9B618E530DE24D0E3EA93D90F66712EB80",
      "NumMicroBlocks": 4,
      "NumTxns": 0,
      "PrevBlockHash": "06f94e089213d9f89393f28d43320c4251e87ee9d393f4aa52cbf325f5f5eb15",
      "Rewards": "0",
      "StateDeltaHash": "0000000000000000000000000000000000000000000000000000000000000000",
      "StateRootHash": "61da8b03cd7d2729056ed8407a2bccffecffb4854ea304085a3ad5516901dfd7",
      "Timestamp": "1562059080341128",
      "Version": 1
    }
  }
}
```

Returns the details of the most recent Transaction block.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description          |
| --------- | ------ | -------- | -------------------- |
| `id`      | string | Required | `"1"`                |
| `jsonrpc` | string | Required | `"2.0"`              |
| `method`  | string | Required | `"GetLatestTxBlock"` |
| `params`  | string | Required | Empty string `""`    |

## GetNumTxBlocks

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumTxBlocks",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const numTxBlock = await zilliqa.blockchain.getNumTxBlocks();
console.log(numTxBlock.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<String> numTxBlocks = client.getNumTxBlocks();
        System.out.println(new Gson().toJson(numTxBlocks));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetNumTxBlocks
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumTxBlocks())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "1000"
}
```

Returns the current number of Transaction blocks in the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description        |
| --------- | ------ | -------- | ------------------ |
| `id`      | string | Required | `"1"`              |
| `jsonrpc` | string | Required | `"2.0"`            |
| `method`  | string | Required | `"GetNumTxBlocks"` |
| `params`  | string | Required | Empty string `""`  |

## GetTxBlockRate

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTxBlockRate",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const txBlockRate = await zilliqa.blockchain.getTxBlockRate();
console.log(txBlockRate.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<Double> txBlockRate = client.getTxBlockRate();
        System.out.println(new Gson().toJson(txBlockRate));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetTxBlockRate
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTxBlockRate())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 6.5499873692751224e-7
}
```

Returns the current Transaction blockrate per second for the network.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description        |
| --------- | ------ | -------- | ------------------ |
| `id`      | string | Required | `"1"`              |
| `jsonrpc` | string | Required | `"2.0"`            |
| `method`  | string | Required | `"GetTxBlockRate"` |
| `params`  | string | Required | Empty string `""`  |

## TxBlockListing

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "TxBlockListing",
    "params": [1]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const txBlockListing = await zilliqa.blockchain.getTxBlockListing(1);
console.log(txBlockListing.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<BlockList> blockListing = client.getTxBlockListing(1);
        System.out.println(new Gson().toJson(blockListing));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetTxBlockListing(1)
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTxBlockListing(1))
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "data": [
      {
        "BlockNum": 1016,
        "Hash": "BBA0C358B0A578CFD5230E501B76A0D8C3E27D5E82524D8B3028B4D8D68AFD3A"
      },
      {
        "BlockNum": 1015,
        "Hash": "F90074A2A50973C80DB358DEF8F6D39157ADAEF1C1634E88B66FD55230212FA7"
      },
      {
        "BlockNum": 1014,
        "Hash": "C71C95A4AD784251F3BDBC157CAF87B941F0866A40C5AA2409B724AE55CC25BC"
      },
      {
        "BlockNum": 1013,
        "Hash": "9A432A3BD743A1B31B839F1C0E61C4B1D7C3A983D767B8DB9833D7B9537BCCD7"
      },
      {
        "BlockNum": 1012,
        "Hash": "141772BB18777685F55D2E8BEB1682357C0D4CD0E28680B8993C2D6B1CE685AE"
      },
      {
        "BlockNum": 1011,
        "Hash": "092209AD966FFC928180C3A14F1CD4DBC1D065F167441FC2D31B471C612AE77D"
      },
      {
        "BlockNum": 1010,
        "Hash": "7A1A580FEFD45947A4F5DDA1D75CAB96B8DCE15D9E6644DF3BF072F45C52D0F3"
      },
      {
        "BlockNum": 1009,
        "Hash": "BDB10D71FF35EB607DC45FF283FD477568903D295B80F9380FCB39D11BE55336"
      },
      {
        "BlockNum": 1008,
        "Hash": "E64E2E716D89410B06DF5E32846C4743A755836A35EF449C7955602DF4E60DD0"
      },
      {
        "BlockNum": 1007,
        "Hash": "1FD23789E64D1645B7D03058AFCFEB7118A92578A59DA6604568B9B5987F9458"
      }
    ],
    "maxPages": 102
  }
}
```

Returns a paginated list of up to **10** Transaction blocks and their block hashes for a specified page. The `maxPages` variable that specifies the maximum number of pages available is also returned.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                |
| --------- | ------ | -------- | ---------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                      |
| `jsonrpc` | string | Required | `"2.0"`                                                    |
| `method`  | string | Required | `"TxBlockListing"`                                         |
| `params`  | number | Required | Specifed page of TX blocks listing to return. Example: `1` |

## GetNumTransactions

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumTransactions",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const numTransactions = await zilliqa.blockchain.getNumTransactions();
console.log(numTransactions.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<String> numTransactions = client.getNumTransactions();
        System.out.println(new Gson().toJson(numTransactions));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetNumTransactions
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumTransactions())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "19"
}
```

Returns the current number of validated Transactions in the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description            |
| --------- | ------ | -------- | ---------------------- |
| `id`      | string | Required | `"1"`                  |
| `jsonrpc` | string | Required | `"2.0"`                |
| `method`  | string | Required | `"GetNumTransactions"` |
| `params`  | string | Required | Empty string `""`      |

## GetTransactionRate

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTransactionRate",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const transactionRate = await zilliqa.blockchain.getTransactionRate();
console.log(transactionRate.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<Integer> transactionRate = client.getTransactionRate();
        System.out.println(new Gson().toJson(transactionRate));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetTransactionRate
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTransactionRate())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 0
}
```

Returns the current Transaction rate per second **(TPS)** of the network. <br> This is represented as an `Number`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description            |
| --------- | ------ | -------- | ---------------------- |
| `id`      | string | Required | `"1"`                  |
| `jsonrpc` | string | Required | `"2.0"`                |
| `method`  | string | Required | `"GetTransactionRate"` |
| `params`  | string | Required | Empty string `""`      |

## GetCurrentMiniEpoch

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetCurrentMiniEpoch",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const currentMiniEpoch = await zilliqa.blockchain.getCurrentMiniEpoch();
console.log(currentMiniEpoch.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<String> currentMiniEpoch = client.getCurrentMiniEpoch();
        System.out.println(new Gson().toJson(currentMiniEpoch));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetCurrentMiniEpoch
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetCurrentMiniEpoch())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "1068"
}
```

Returns the current TX block number of the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description             |
| --------- | ------ | -------- | ----------------------- |
| `id`      | string | Required | `"1"`                   |
| `jsonrpc` | string | Required | `"2.0"`                 |
| `method`  | string | Required | `"GetCurrentMiniEpoch"` |
| `params`  | string | Required | Empty string `""`       |

## GetCurrentDSEpoch

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetCurrentDSEpoch",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const currentDSEpoch = await zilliqa.blockchain.getCurrentDSEpoch();
console.log(currentDSEpoch.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<String> currentDSEpoch = client.getCurrentDSEpoch();
        System.out.println(new Gson().toJson(currentDSEpoch));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetCurrentDSEpoch
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetCurrentDSEpoch())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "22"
}
```

Returns the current number of DS blocks in the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description           |
| --------- | ------ | -------- | --------------------- |
| `id`      | string | Required | `"1"`                 |
| `jsonrpc` | string | Required | `"2.0"`               |
| `method`  | string | Required | `"GetCurrentDSEpoch"` |
| `params`  | string | Required | Empty string `""`     |

## GetPrevDifficulty

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetPrevDifficulty",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const prevDifficulty = await zilliqa.blockchain.getPrevDifficulty();
console.log(prevDifficulty.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<Integer> prevDifficulty = client.getPrevDifficulty();
        System.out.println(new Gson().toJson(prevDifficulty));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetPrevDifficulty
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetPrevDifficulty())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 3
}
```

Returns the minimum shard difficulty of the previous block. <br> This is represented as an `Number`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description           |
| --------- | ------ | -------- | --------------------- |
| `id`      | string | Required | `"1"`                 |
| `jsonrpc` | string | Required | `"2.0"`               |
| `method`  | string | Required | `"GetPrevDifficulty"` |
| `params`  | string | Required | Empty string `""`     |

## GetPrevDSDifficulty

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetPrevDSDifficulty",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const prevDSDifficulty = await zilliqa.blockchain.getPrevDSDifficulty();
console.log(prevDSDifficulty.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com/");
        Rep<Integer> prevDSDifficulty = client.getPrevDSDifficulty();
        System.out.println(new Gson().toJson(prevDSDifficulty));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetPrevDSDifficulty
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetPrevDSDifficulty())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 16
}
```

Returns the minimum DS difficulty of the previous block. <br> This is represented as an `Number`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description             |
| --------- | ------ | -------- | ----------------------- |
| `id`      | string | Required | `"1"`                   |
| `jsonrpc` | string | Required | `"2.0"`                 |
| `method`  | string | Required | `"GetPrevDSDifficulty"` |
| `params`  | string | Required | Empty string `""`       |

## GetTotalCoinSupply

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTotalCoinSupply",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const totalCoinSupply = await zilliqa.network.GetTotalCoinSupply();
console.log(totalCoinSupply);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<String> totalCoinSupply = client.getTotalCoinSupply();
        System.out.println(new Gson().toJson(totalCoinSupply));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetTotalCoinSupply
puts ret
```

```python
from pyzil.zilliqa import chain
from pyzil.zilliqa.api import ZilliqaAPI


# EITHER
chain.set_active_chain(chain.MainNet)
total_coin_supply = chain.active_chain.api.GetTotalCoinSupply()
print(total_coin_supply)

# OR
new_api = ZilliqaAPI(endpoint="https://api.zilliqa.com")
total_coin_supply = new_api.GetTotalCoinSupply()
print(total_coin_supply)

```

> **Example response:**

```json
{"id":"1","jsonrpc":"2.0","result":"12600527397.260273972000"}
```

Returns the total supply (ZIL) of coins in the network. This is represented as a `String`.



### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description            |
| --------- | ------ | -------- | -----------------      |
| `id`      | string | Required | `"1"`                  |
| `jsonrpc` | string | Required | `"2.0"`                |
| `method`  | string | Required | `"GetTotalCoinSupply"` |
| `params`  | string | Required | Empty string `""`      |


# Transaction-related methods

## CreateTransaction

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "CreateTransaction",
    "params": [{
      "version": 65537,
      "nonce": 1,
      "toAddr": "0x4BAF5faDA8e5Db92C3d3242618c5B47133AE003C",
      "amount": "1000000000000",
      "pubKey": "0205273e54f262f8717a687250591dcfb5755b8ce4e3bd340c7abefd0de1276574",
      "gasPrice": "1000000000",
      "gasLimit": "1",
      "code": "",
      "data": "",
      "signature": "29ad673848dcd7f5168f205f7a9fcd1e8109408e6c4d7d03e4e869317b9067e636b216a32314dd37176c35d51f9d4c24e0e519ba80e66206457c83c9029a490d",
      "priority": false
    }]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
let tx = zilliqa.transactions.new({
  version: 65537,
  toAddr: "0x4BAF5faDA8e5Db92C3d3242618c5B47133AE003C",
  amount: units.toQa("1", units.Units.Zil),
  gasPrice: units.toQa("1000", units.Units.Li),
  gasLimit: Long.fromNumber(1)
});

// Send a transaction to the network
tx = await zilliqa.blockchain.createTransaction(tx);
console.log(tx.id);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        Wallet wallet = new Wallet();
        wallet.setProvider(new HttpProvider("https://dev-api.zilliqa.com"));
        wallet.addByPrivateKey("e19d05c5452598e24caad4a0d85a49146f7be089515c905ae6a19e8a578a6930");
        Transaction transaction = Transaction.builder()
                .version(String.valueOf(pack(1, 8)))
                .toAddr("4baf5fada8e5db92c3d3242618c5b47133ae003c".toLowerCase())
                .senderPubKey("0246e7178dc8253201101e18fd6f6eb9972451d121fc57aa2a06dd5c111e58dc6a")
                .amount("1000000000000")
                .gasPrice("1000000000")
                .gasLimit("1")
                .code("")
                .data("")
                .provider(new HttpProvider("https://api.zilliqa.com"))
                .build();
        transaction = wallet.sign(transaction);

        // Send a transaction to the network
        HttpProvider.CreateTxResult result = TransactionFactory.createTransaction(transaction);
        System.out.println(result);
    }
}
```

```ruby
payload = {
    version: 65537,
    toAddr: '4baf5fada8e5db92c3d3242618c5b47133ae003c',
    amount: '1000000000000',
    gasPrice: '1000000000',
    gasLimit: 1,
})

provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.CreateTransaction(payload)
puts ret
```

```python
from pyzil.account import Account
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)

account = Account(private_key="0xe19d05c5452598e24caad4a0d85a49146f7be089515c905ae6a19e8a578a6930")

payload = {
    "to_addr": "0x4BAF5faDA8e5Db92C3d3242618c5B47133AE003C",
    "amount": "1000000000000",
    "nonce": account.get_nonce() + 1,
    "gas_price": "1000000000",
    "gas_limit": 1,
    "code": "",
    "data": "",
    "priority": False,
}

params = chain.active_chain.build_transaction_params(account.zil_key, **payload)
txn_info = chain.active_chain.api.CreateTransaction(params)
print(txn_info)
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "Info": "Non-contract txn, sent to shard",
    "TranID": "2d1eea871d8845472e98dbe9b7a7d788fbcce226f52e4216612592167b89042c"
  }
}
```

Create a new Transaction object and send it to the network to be process. <br> See [Quick Start](https://github.com/Zilliqa/Zilliqa-JavaScript-Library#quick-start) in Javascript-SDK for an example of how to construct a Transaction object.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                              |
| --------- | ------ | -------- | -------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                    |
| `jsonrpc` | string | Required | `"2.0"`                                                  |
| `method`  | string | Required | `"CreateTransaction"`                                    |
| `params`  | N/A    | Required | See table below for the Transaction parameters required: |

### TRANSACTION PARAMETERS

| Parameter   | Type    | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ----------- | ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `version`   | number  | Required | The decimal conversion of the bitwise concatenation of `CHAIN_ID` and `MSG_VERSION` parameters. <br><br> **-** For mainnet, it is `65537`. <br> **-** For Developer testnet, it is `21823489`.                                                                                                                                                                                                                                             |
| `nonce`     | number  | Required | A transaction counter in each account. This prevents replay attacks where a transaction sending eg. 20 coins from A to B can be replayed by B over and over to continually drain A's balance. <br><br> It's value should be `Current account nonce + 1`.                                                                                                                                                                                   |
| `toAddr`    | string  | Required | Recipient's account address. This is represented as a `String`. <br><br> **NOTE:** This address has to be checksummed for every 6th bit, but the "0x" prefix is optional. <br><br> For deploying new contracts, set this to `"0000000000000000000000000000000000000000"`.                                                                                                                                                                  |
| `amount`    | string  | Required | Transaction amount to be sent to the recipent's address. This is measured in the smallest price unit **Qa** (or 10^-12 **Zil**) in Zilliqa.                                                                                                                                                                                                                                                                                                |
| `pubKey`    | string  | Required | Sender's public key of 33 bytes.                                                                                                                                                                                                                                                                                                                                                                                                           |
| `gasPrice`  | string  | Required | An amount that a sender is willing to pay per unit of gas for processing this transaction. This is measured in the smallest price unit **Qa** (or 10^-12 **Zil**) in Zilliqa.                                                                                                                                                                                                                                                              |
| `gasLimit`  | string  | Required | The amount of gas units that is needed to be process this transaction. <br><br> **-** For **regular transaction**, please use `"1"`. <br> **-** For **smart contract transaction**, please consult the [gas documentation](https://drive.google.com/file/d/1c0EJXELVe_MxhULPuJgwGvxFGenG7fmK/view?usp=sharing).                                                                                                                            |
| `code`      | string  | Optional | The smart contract source code. This is present only when deploying a new contract.                                                                                                                                                                                                                                                                                                                                                        |
| `data`      | string  | Optional | `String`-ified JSON object specifying the transition parameters to be passed to a specified smart contract. <br><br> - When creating a contract, this JSON object contains the **init** parameters. <br> - When calling a contract, this JSON object contains the **msg** parameters. <br><br> _For more information on the Scilla interpreter, please visit the [documentation](https://scilla.readthedocs.io/en/latest/interface.html)._ |
| `signature` | string  | Required | An **EC-Schnorr** signature of 64 bytes of the entire Transaction object as stipulated above.                                                                                                                                                                                                                                                                                                                                              |
| `priority`  | boolean | Optional | A flag for this transaction to be processed by the DS committee. <br><br> This is required for only for [Category III transactions](https://blog.zilliqa.com/provisioning-sharding-for-smart-contracts-a-design-for-zilliqa-cd8d012ee735), but it can be used for other transaction categories too.                                                                                                                                        |

## GetTransaction

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTransaction",
    "params": ["655107c300e86ee6e819af1cbfce097db1510e8cd971d99f32ce2772dcad42f2"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const txn = await zilliqa.blockchain.getTransaction(
  "655107c300e86ee6e819af1cbfce097db1510e8cd971d99f32ce2772dcad42f2"
);
console.log(txn.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<Transaction> transaction = client.getTransaction("655107c300e86ee6e819af1cbfce097db1510e8cd971d99f32ce2772dcad42f2");
        System.out.println(new Gson().toJson(transaction));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetTransaction("655107c300e86ee6e819af1cbfce097db1510e8cd971d99f32ce2772dcad42f2")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTransaction("655107c300e86ee6e819af1cbfce097db1510e8cd971d99f32ce2772dcad42f2"))
```

> **Example response:**


```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "ID": "655107c300e86ee6e819af1cbfce097db1510e8cd971d99f32ce2772dcad42f2",
    "amount": "0",
    "gasLimit": "10000",
    "gasPrice": "1000000000",
    "nonce": "20",
    "receipt": {
      "cumulative_gas": "1662",
      "epoch_num": "134",
      "success": true
    },
    "senderPubKey": "0x03EBCBAEEDD5F98F428BCEBC83E609E5F98136470708A57D61B71BF0B332200EEA",
    "signature": "0x6DEA9FE535AB3557963CA47323B150979CB7C3990515389AF18AFFDD1049ECF3C5AEB5107A64636A946E75219B9482AFE9C7E1D8E5C59D55A1A28A24C0B877B6",
    "toAddr": "0000000000000000000000000000000000000000",
    "version": "131073"
  }
}
```

*Note: If the transaction had an data field or code field, it will be displayed*

```json
{
    "id": "1",
    "jsonrpc": "2.0",
    "result": {
        "ID": "ebd9da6a0a3855c910813dad3d6796cf90f12bf5152dcb5ddda664ef2a632ad9",
        "amount": "0",
        "data": "{\"_tag\":\"t3\",\"params\":[]}",
        "gasLimit": "100000",
        "gasPrice": "10000000000",
        "nonce": "118",
        "receipt": {
            "cumulative_gas": "176",
            "epoch_num": "229640",
            "success": true
        },
        "senderPubKey": "0x021D8698472A58B11176125D1B2B05981849DB83B6A91D019F7686A4F9702CA598",
        "signature": "0xD642287BB7DB3C2B48B162D88EB90D6B48C3EFC2309FAF04B59E1422BEE27F15AC5ED7CCA21D5F791073E59DEE6EAA2A9134CEDBC1467BAA6C0E471BC5F4ECA4",
        "toAddr": "4c876493f196d2660ba98f2989982a4d1e7282ab",
        "version": "65537"
    }
}
```

Returns the details of a specified Transaction.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                              |
| --------- | ------ | -------- | -------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                    |
| `jsonrpc` | string | Required | `"2.0"`                                                  |
| `method`  | string | Required | `"GetTransaction"`                                       |
| `params`  | string | Required | Transaction hash of 32 bytes of a specified transaction. |


## GetRecentTransactions

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetRecentTransactions",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const recentTransactions = await zilliqa.blockchain.getRecentTransactions();
console.log(recentTransactions.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<TransactionList> transactionList = client.getRecentTransactions();
        System.out.println(new Gson().toJson(transactionList));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetRecentTransactions
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetRecentTransactions())
```

> **Example response:**

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
      "ace1376174f12adda4dcaa2ed01a48cf9e8c02419bdeab4477cd6d60f7239223"
    ],
    "number": 100
  }
}
```

Returns the most recent **100** transactions that are validated by the Zilliqa network.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description               |
| --------- | ------ | -------- | ------------------------- |
| `id`      | string | Required | `"1"`                     |
| `jsonrpc` | string | Required | `"2.0"`                   |
| `method`  | string | Required | `"GetRecentTransactions"` |
| `params`  | string | Required | Empty string `""`         |

## GetTransactionsForTxBlock

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTransactionsForTxBlock",
    "params": ["2"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const txns = await zilliqa.blockchain.getTransactionsForTxBlock("2");
console.log(txns.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<List<List<String>>> transactionList = client.getTransactionsForTxBlock("2");
        System.out.println(new Gson().toJson(transactionList));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetTransactionsForTxBlock("2")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTransactionsForTxBlock("2"))
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": [
    [
      "2398362e23635582ed58f83dbcff7af2d8ccb017f6ff2bb49d343e7b8bb8bd68",
      "3f337358c07c4e984714da804985f23eca9a9dd14aa8ba1ddd89583cf5110bf0",
      "35823ae3377b91792fa34fa5577fa267385374e08da51555f63a537942d5adb6",
      "04e5f20de988a4afea17408c87a8d4f73d14082f13df552cce849e4ddd4cfffc"
    ],
    [
      "5830a93aafe6571099aa38e99218c4495a2af73d481a28aba8a34c45768d0fb9",
      "9250ce07210b75ef8ec5fcf42f3b5afa4cd4b60414b338be0caddcfb316293cf",
      "60fe6307f27e084bfb84ff5b6cafcbb05e1bc450d1b67d9102d57066d931ba7f",
      "92562be5d4fd4b39ea44f22e010636163b6500561ddab58aca0a90ac7c11f04c"
    ],
    [
      "9cfe6d32b31cf31267bc46b2a99f0b243266f4842d140dab5b3ee31369ae9926",
      "3526b2b8f226fff6643c60deea71129dcd98c320521c8e96715e2f02c651a081",
      "477a9c79acaa9aa2060b9d21f2e01760a31499b32723e0e2e1cb2cb8c4e4be7e",
      "a1fa8ec4253c8ad125b81f8ee952f4e12abc445c80f56d85e18a9246541b7f37",
      "251ce0e4a60be05363cad225b61f48ae4dd017230b0b3c58c7257239ec51aa09",
      "452471a31af62ecd48cadc1536a4fef3b7ac243dd1023d8f9a12b1448f096c69",
      "a5b1c0354433304ca6a3d3bc95eb41bae856b8aea5eb6d7ea28fff19e4b1033b"
    ],
    [
      "adba475e9ae7419a91107987c93838ac72c305937c5683aecee2d98024002eca",
      "0f0cf6f5e4ba6ed7302db5b00f958b305e33d28e5a5a7297f87f51307b59aa82",
      "d05be491318e6bbadb4705d436daf0c46762de1e14bf8d4794ff34782584f027",
      "2157babdc5c65e7b4ca5e774782119d811d54d4dcc9b64a176120f1ac3c73c1c",
      "dafc9b289def10232da12efcc6fa37a142982c832357628e830e616e9663501e"
    ]
  ]
}
```

Returns the validated transactions included within a specfied final transaction block as an array of length _i_, where _i_ is the number of shards plus the DS committee. The transactions are grouped based on the group that processed the transaction. The first element of the array refers to the first shard. The last element of the array at index, _i_, refers to the transactions processed by the DS Committee.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                        |
| --------- | ------ | -------- | -------------------------------------------------- |
| `id`      | string | Required | `"1"`                                              |
| `jsonrpc` | string | Required | `"2.0"`                                            |
| `method`  | string | Required | `"GetTransactionsForTxBlock"`                      |
| `params`  | string | Required | Specifed TX block number to return. Example: `"2"` |

## GetNumTxnsTxEpoch

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumTxnsTxEpoch",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const numTxnsTxEpoch = await zilliqa.blockchain.getNumTxnsTxEpoch();
console.log(numTxnsTxEpoch.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<String> numTxnsTxEpoch = client.getNumTxnsTxEpoch();
        System.out.println(new Gson().toJson(numTxnsTxEpoch));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetNumTxnsTxEpoch
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumTxnsTxEpoch())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "0"
}
```

Returns the number of validated transactions included in this Transaction epoch. <br> This is represented as `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description           |
| --------- | ------ | -------- | --------------------- |
| `id`      | string | Required | `"1"`                 |
| `jsonrpc` | string | Required | `"2.0"`               |
| `method`  | string | Required | `"GetNumTxnsTxEpoch"` |
| `params`  | string | Required | Empty string `""`     |

## GetNumTxnsDSEpoch

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetNumTxnsDSEpoch",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const numTxnsDSEpoch = await zilliqa.blockchain.getNumTxnsDSEpoch();
console.log(numTxnsDSEpoch.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<String> numTxnsDSEpoch = client.getNumTxnsDSEpoch();
        System.out.println(new Gson().toJson(numTxnsDSEpoch));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetNumTxnsDSEpoch
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumTxnsDSEpoch())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "0"
}
```

Returns the number of validated transactions included in this DS epoch. <br> This is represented as `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description           |
| --------- | ------ | -------- | --------------------- |
| `id`      | string | Required | `"1"`                 |
| `jsonrpc` | string | Required | `"2.0"`               |
| `method`  | string | Required | `"GetNumTxnsDSEpoch"` |
| `params`  | string | Required | Empty string `""`     |

## GetMinimumGasPrice

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetMinimumGasPrice",
    "params": [""]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const minimumGasPrice = await zilliqa.blockchain.getMinimumGasPrice();
console.log(minimumGasPrice.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<String> minimumGasPrice = client.getMinimumGasPrice();
        System.out.println(new Gson().toJson(minimumGasPrice));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetMinimumGasPrice
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetMinimumGasPrice())
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "100"
}
```

Returns the minimum gas price for this DS epoch, measured in the smallest price unit **Qa** (or 10^-12 **Zil**) in Zilliqa.
<br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description            |
| --------- | ------ | -------- | ---------------------- |
| `id`      | string | Required | `"1"`                  |
| `jsonrpc` | string | Required | `"2.0"`                |
| `method`  | string | Required | `"GetMinimumGasPrice"` |
| `params`  | string | Required | Empty string `""`      |

# Contract-related methods

## GetSmartContractCode

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractCode",
    "params": ["fe001824823b12b58708bf24edd94d8b5e1cfcf7"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const smartContractCode = await zilliqa.blockchain.getSmartContractCode(
  "fe001824823b12b58708bf24edd94d8b5e1cfcf7"
);
console.log(smartContractCode.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<HttpProvider.ContractResult> smartContractCode = client.getSmartContractCode("fe001824823b12b58708bf24edd94d8b5e1cfcf7");
        System.out.println(new Gson().toJson(smartContractCode));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetSmartContractCode("fe001824823b12b58708bf24edd94d8b5e1cfcf7")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetSmartContractCode("fe001824823b12b58708bf24edd94d8b5e1cfcf7"))
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "code": "scilla_version 0\n\n    (* HelloWorld contract *)\n    \n    import ListUtils\n    \n    (***************************************************)\n    (*               Associated library                *)\n    (***************************************************)\n    library HelloWorld\n    \n    let one_msg = \n      fun (msg : Message) => \n      let nil_msg = Nil {Message} in\n      Cons {Message} msg nil_msg\n    \n    let not_owner_code = Int32 1\n    let set_hello_code = Int32 2\n    \n    (***************************************************)\n    (*             The contract definition             *)\n    (***************************************************)\n    \n    contract HelloWorld\n    (owner: ByStr20)\n    \n    field welcome_msg : `String` = \"\"\n    \n    transition setHello (msg : `String`)\n      is_owner = builtin eq owner _sender;\n      match is_owner with\n      | False =>\n        msg = {_tag : \"Main\"; _recipient : _sender; _amount : Uint128 0; code : not_owner_code};\n        msgs = one_msg msg;\n        send msgs\n      | True =>\n        welcome_msg := msg;\n        msg = {_tag : \"Main\"; _recipient : _sender; _amount : Uint128 0; code : set_hello_code};\n        msgs = one_msg msg;\n        send msgs\n      end\n    end\n    \n    \n    transition getHello ()\n        r <- welcome_msg;\n        e = {_eventname: \"getHello()\"; msg: r};\n        event e\n    end"
  }
}
```

Returns the Scilla code associated with a smart contract address. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                                                      |
| --------- | ------ | -------- | ------------------------------------------------------------------------------------------------ |
| `id`      | string | Required | `"1"`                                                                                            |
| `jsonrpc` | string | Required | `"2.0"`                                                                                          |
| `method`  | string | Required | `"GetSmartContractCode"`                                                                         |
| `params`  | string | Required | A smart contract address of 20 bytes. <br> Example: `"fe001824823b12b58708bf24edd94d8b5e1cfcf7"` |

## GetSmartContractInit

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractInit",
    "params": ["fe001824823b12b58708bf24edd94d8b5e1cfcf7"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const smartContractInit = await zilliqa.blockchain.getSmartContractInit(
  "fe001824823b12b58708bf24edd94d8b5e1cfcf7"
);
console.log(smartContractInit.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<List<Contract.State>> smartContractInit = client.getSmartContractInit("fe001824823b12b58708bf24edd94d8b5e1cfcf7");
        System.out.println(new Gson().toJson(smartContractInit));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetSmartContractInit("fe001824823b12b58708bf24edd94d8b5e1cfcf7")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetSmartContractInit("fe001824823b12b58708bf24edd94d8b5e1cfcf7"))
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": [
    {
      "type": "Uint32",
      "value": "0",
      "vname": "_scilla_version"
    },
    {
      "type": "ByStr20",
      "value": "0x67a08f4aefbe1798970be37dc3d0c7954be349de",
      "vname": "owner"
    },
    {
      "type": "BNum",
      "value": "140",
      "vname": "_creation_block"
    },
    {
      "type": "ByStr20",
      "value": "0x65fc5463805e3d7c753392e8a1e721aebda8d27f",
      "vname": "_this_address"
    }
  ]
}
```

Returns the initialization (immutable) parameters of a given smart contract, represented in a JSON format.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                                                      |
| --------- | ------ | -------- | ------------------------------------------------------------------------------------------------ |
| `id`      | string | Required | `"1"`                                                                                            |
| `jsonrpc` | string | Required | `"2.0"`                                                                                          |
| `method`  | string | Required | `"GetSmartContractInit"`                                                                         |
| `params`  | string | Required | A smart contract address of 20 bytes. <br> Example: `"fe001824823b12b58708bf24edd94d8b5e1cfcf7"` |

## GetSmartContractSubState

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractSubState",
    "params": ["fe001824823b12b58708bf24edd94d8b5e1cfcf7","admins",[]]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const smartContractState = await zilliqa.blockchain.getSmartContractSubState(
  "fe001824823b12b58708bf24edd94d8b5e1cfcf7"
);
console.log(smartContractState.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        List<Object> param = new ArrayList<>();
        param.add("9611c53BE6d1b32058b2747bdeCECed7e1216793");
        param.add("admins");
        param.add(new ArrayList<>());
        String state = client.getSmartContractSubState(param);
        System.out.println(state);
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetSmartContractSubState("fe001824823b12b58708bf24edd94d8b5e1cfcf7")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetSmartContractSubState("fe001824823b12b58708bf24edd94d8b5e1cfcf7","admins",[]))
```

> **Example response:**


```json
{
   "admins" : {
      "0xdfa89866ae86632b36361d53b76c1373448c28fa" : {
         "argtypes" : [],
         "arguments" : [],
         "constructor" : "True"
      }
   }
} 
```

Returns the state (or a part specified) of a smart contract address, represented in a JSON format.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                                                      |
| --------- | ------ | -------- | ------------------------------------------------------------------------------------------------ |
| `id`      | string | Required | `"1"`                                                                                            |
| `jsonrpc` | string | Required | `"2.0"`                                                                                          |
| `method`  | string | Required | `"GetSmartContractSubState"`                                                                     |
| `params`  | array  | Required | State params                                                                                     |


### STATE PARAMS

| Parameter     | Type       | Required     | Description                                                                                      |
|---------------|------------|--------------|--------------------------------------------------------------------------------------------------|
|`Address`      | string     | Required     | A smart contract address of 20 bytes.                                                            |
|`Variable Name`| string     | Can be empty | Name of the variable in the Smart Contract                                                       |
|`Indices`      | JSON Array | Can be empty | If the variable is of map type, you can specify an index (or indices)                            |


The `params` is JSON array <br> Example: `"params"`:`["fe001824823b12b58708bf24edd94d8b5e1cfcf7","admins",[\"0x9bfec715a6bd658fcb62b0f8cc9bfa2ade71434a\""]]`

*Note: If Variable Name and Indices Array are both empty, the response would be same as GetSmartContractState*

## GetSmartContractState

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContractState",
    "params": ["fe001824823b12b58708bf24edd94d8b5e1cfcf7"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const smartContractState = await zilliqa.blockchain.getSmartContractState(
  "fe001824823b12b58708bf24edd94d8b5e1cfcf7"
);
console.log(smartContractState.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        String smartContractState = client.getSmartContractState("fe001824823b12b58708bf24edd94d8b5e1cfcf7");
        System.out.println(smartContractState);
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetSmartContractState("fe001824823b12b58708bf24edd94d8b5e1cfcf7")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetSmartContractState("fe001824823b12b58708bf24edd94d8b5e1cfcf7"))
```

> **Example response:**

*Note: The format of response has been changed*

```json
{
   "_balance" : "0",
   "admins" : {
      "0xdfa89866ae86632b36361d53b76c1373448c28fa" : {
         "argtypes" : [],
         "arguments" : [],
         "constructor" : "True"
      }
   }
} 
```

Returns the state (mutable) variables of a smart contract address, represented in a JSON format.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                                                      |
| --------- | ------ | -------- | ------------------------------------------------------------------------------------------------ |
| `id`      | string | Required | `"1"`                                                                                            |
| `jsonrpc` | string | Required | `"2.0"`                                                                                          |
| `method`  | string | Required | `"GetSmartContractState"`                                                                        |
| `params`  | string | Required | A smart contract address of 20 bytes. <br> Example: `"fe001824823b12b58708bf24edd94d8b5e1cfcf7"` |

## GetSmartContracts

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetSmartContracts",
    "params": ["1eefc4f453539e5ee732b49eb4792b268c2f3908"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const smartContracts = await zilliqa.blockchain.getSmartContracts(
  "1eefc4f453539e5ee732b49eb4792b268c2f3908"
);
console.log(smartContracts.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<List<Contract>> smartContracts = client.getSmartContracts("fe001824823b12b58708bf24edd94d8b5e1cfcf7");
        System.out.println(new Gson().toJson(smartContracts));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetSmartContracts("fe001824823b12b58708bf24edd94d8b5e1cfcf7")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetSmartContracts("fe001824823b12b58708bf24edd94d8b5e1cfcf7"))
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": [
    {
      "address": "6b3070b0abf4371b2b3b26e23f11f4c073b636e5",
      "state": [
        {
          "type": "String",
          "value": "Hello World",
          "vname": "welcome_msg"
        },
        {
          "type": "Uint128",
          "value": "0",
          "vname": "_balance"
        }
      ]
    },
    {
      "address": "13cf0f8c1ea003779df0b7fa08a97903bc760e80",
      "state": [
        {
          "type": "String",
          "value": "Hello World",
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

Returns the list of smart contract addresses created by an User's account and the contracts' latest states.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                                                       |
| --------- | ------ | -------- | ------------------------------------------------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                                                             |
| `jsonrpc` | string | Required | `"2.0"`                                                                                           |
| `method`  | string | Required | `"GetSmartContracts"`                                                                             |
| `params`  | string | Required | An User's account address of 20 bytes. <br> Example: `"1eefc4f453539e5ee732b49eb4792b268c2f3908"` |


## GetContractAddressFromTransactionID

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetContractAddressFromTransactionID",
    "params": ["AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const contractAddress = await zilliqa.blockchain.getContractAddressFromTransactionID(
  "AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E"
);
console.log(contractAddress.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<String> contractAddress = client.getContractAddressFromTransactionID("AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E");
        System.out.println(new Gson().toJson(contractAddress));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetContractAddressFromTransactionID("AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetContractAddressFromTransactionID(
     "AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E"
))
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "c458f39c106582c1a49bac6bc76ec603e2ae0497"
}
```

Returns a smart contract address of 20 bytes. This is represented as a `String`. <br>
**NOTE:** This only works for contract deployment transactions.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                                                                      |
| --------- | ------ | -------- | ---------------------------------------------------------------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                                                                            |
| `jsonrpc` | string | Required | `"2.0"`                                                                                                          |
| `method`  | string | Required | `"GetSmartContracts"`                                                                                            |
| `params`  | string | Required | A Transaction ID of 32 bytes. <br> Example: `"AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E"` |

# Account-related methods

## GetBalance

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetBalance",
    "params": ["1eefc4f453539e5ee732b49eb4792b268c2f3908"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const balance = await zilliqa.blockchain.getBalance(
  "1eefc4f453539e5ee732b49eb4792b268c2f3908"
);
console.log(balance.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<HttpProvider.BalanceResult> balance = client.getBalance("1eefc4f453539e5ee732b49eb4792b268c2f3908");
        System.out.println(new Gson().toJson(balance));
    }
}
```

```ruby
provider = Laksa::Jsonrpc::Provider.new('https://api.zilliqa.com')

ret = provider.GetBalance("1eefc4f453539e5ee732b49eb4792b268c2f3908")
puts ret
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetBalance("1eefc4f453539e5ee732b49eb4792b268c2f3908"))
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "balance": "18446744073637511711",
    "nonce": 16
  }
}
```

- Returns the current `balance` of an account, measured in the smallest accounting unit **Qa** (or 10^-12 **Zil**). This is represented as a `String` <br><br>
- Returns the current `nonce` of an account. This is represented as an `Number`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa Mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                                                       |
| --------- | ------ | -------- | ------------------------------------------------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                                                             |
| `jsonrpc` | string | Required | `"2.0"`                                                                                           |
| `method`  | string | Required | `"GetBalance"`                                                                                    |
| `params`  | string | Required | An User's account address of 20 bytes. <br> Example: `"1eefc4f453539e5ee732b49eb4792b268c2f3908"` |
