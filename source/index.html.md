---
title: Zilliqa JSON-RPC API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript: node.js
  - java: java
  - python: python
  - go: go

toc_footers:
  - <a href='https://github.com/Zilliqa/Zilliqa-Javascript-Library'>Javascript SDK</a>
  - <a href='https://github.com/FireStack-Lab/LaksaJ'>Java SDK</a>
  - <a href='https://github.com/deepgully/pyzil'>Python SDK</a>
  - <a href='https://github.com/Zilliqa/gozilliqa-sdk'>Golang SDK</a>
  - <a href='http://scilla.readthedocs.io/'>Scilla Documentation</a>

includes:

search: true
---

# Introduction

[JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC) is a remote procedure call protocol encoded in JSON. You can use this API to access data from the Zilliqa nodes.
The JSON-RPC API server runs on:

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```go
func GetNetworkId() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetNetworkId()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
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
| **Zilliqa mainnet**   | `1`        |
| **Developer testnet** | `333`      |

**NOTE:** `CHAIN_ID` from `2` to `9` are reserved for Zilliqa Core use.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetBlockchainInfo())
```

```go
func GetBlockchainInfo() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetBlockchainInfo()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "CurrentDSEpoch": "5898",
    "CurrentMiniEpoch": "589778",
    "DSBlockRate": 0.00014142137245459714,
    "NumDSBlocks": "5899",
    "NumPeers": 2400,
    "NumTransactions": "4350627",
    "NumTxBlocks": "589778",
    "NumTxnsDSEpoch": "748",
    "NumTxnsTxEpoch": "4",
    "ShardingStructure": {
      "NumPeers": [600, 600, 600]
    },
    "TransactionRate": 0.09401852277720939,
    "TxBlockRate": 0.014137955733170903
  }
}
```

Returns the current network statistics for the specified network.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetDsBlock("1"))
```

```go
func GetDsBlock() {
  provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetDsBlock("40")
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
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
      "LeaderPubKey": "0x020035B739426374C5327A1224B986005297102E01C29656B8B086BF4B352C6CA9",
      "PoWWinners": [],
      "PrevHash": "0800bfda2b715fe7e401f7cf73182f072f8459318cb4bb90d195f681c5bbebdd",
      "Timestamp": "1548928944839738"
    },
    "signature": "1515B838C310485ADE001822470E9CF9D0068E8528516AB71D8A964B642AF59A874A5345CC8239254B951EE53CB509A9A3D5F5FF63380D5F70D9A32A060DB0CD"
  }
}
```

Returns the details of a specified Directory Service block.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetLatestDsBlock())
```

```go
func GetLatestDsBlock() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetLatestDsBlock()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "header": {
      "BlockNum": "5898",
      "Difficulty": 91,
      "DifficultyDS": 149,
      "GasPrice": "1000000000",
      "LeaderPubKey": "0x026964CBF00EE542F5CBE80395FFEA747227BC3EFCC21D04956380180A9BE21546",
      "PoWWinners": [
        "0x0219DB403A630022EE014AFD97D02E2DBC6BCEED2506A9E57B5EE5D9EA4F154929",
        "0x02D9C8FC6C87891968ECCEE5EF1CD8A9F8FC32C6463F2FE4E846DFD5C5F45A625E",
        "0x02E07F03C71D26433E7F290416FA43374DA72704F8AA973D4771AA763ACD7C509C",
        "0x02E0FB6CDAEA57738959B493652A74E86339AF2CFE998FB7424BBD7A813450743F",
        "0x0315E9B13D5A5D29902F1EECE0933E96A0AF9939853D5F82B438AAED9F7560B3FC",
        "0x034D9B1B0DC80A0103AE7826886B415C29BF3E814FF6720F6C9C47B57589EFEAAA",
        "0x0394EA64F2F833B88C56464E12B37780BDB9684875F55BC569B397ABE0FCCD8E0E",
        "0x03C53B6C3D901ED46E786DA383BE61A46A442461D2A83379A11A42D7403FB7102E",
        "0x03F6427EE15A5EC409FE7F8CDCC8E7C7704CC07AD2BF8CADFD2A19BB98E80836AF"
      ],
      "PrevHash": "968e2e7820a3795de8c8a7a2e94379cc10f50ada5ea6f90c03c4e61e22ee83b5",
      "Timestamp": "1590641169078644"
    },
    "signature": "803D64288A6F827DAFA529235C7A78E7BC2D1C882C5DA643E03CB0B2A786C7A5508CCD5F409CDAA325709E4E9A98F1D67596E61CB8CF958AD98B7DB842F87A44"
  }
}
```

Returns the details of the most recent Directory Service block.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumDSBlocks())
```

```go
func GetNumDSBlocks() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetNumDSBlocks()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "5899"
}
```

Returns the current number of validated Directory Service blocks in the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetDSBlockRate())
```

```go
func GetDSBlockRate() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetDSBlockRate()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 0.00014142137245459714
}
```

Returns the current Directory Service blockrate per second.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.DSBlockListing(1))
```

```go
func DSBlockListing() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.DSBlockListing(1)
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}

```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "data": [
      {
        "BlockNum": 5898,
        "Hash": "4DEED80AFDCC89D5B691DCB54CCB846AD9D823D448A56ACAC4DBE5E1213244C7"
      },
      {
        "BlockNum": 5897,
        "Hash": "968E2E7820A3795DE8C8A7A2E94379CC10F50ADA5EA6F90C03C4E61E22EE83B5"
      },
      {
        "BlockNum": 5896,
        "Hash": "A52D113357910ADECEFA713D89A667030F521FFB153EEFA97A0D9E7E4AA5230B"
      },
      {
        "BlockNum": 5895,
        "Hash": "8d49d4b18b441dc0da6ca580f468c9e83278c47f0f54fe342e1fe1425c39044f"
      },
      {
        "BlockNum": 5894,
        "Hash": "b966c36557480a35a36a0d1c33723fd9bac8538588dea6716b4dfb2a05815458"
      },
      {
        "BlockNum": 5893,
        "Hash": "fc20118eec0f14fdc089fcfee528276337dcf403a308153485f24f2856998613"
      },
      {
        "BlockNum": 5892,
        "Hash": "4ed593d66b1ea5fa9a77cc1bb119baf90029c249bf5507b01079bc2fbf45aec7"
      },
      {
        "BlockNum": 5891,
        "Hash": "1385bf48e584ebb82cf11a9064d99b5e0b4ae560866a92efe9b78604e08fc821"
      },
      {
        "BlockNum": 5890,
        "Hash": "05d6d24a8f5411ff70fe58a09f38fd4b49ec4122b7c26817964a4a8b8a089c1f"
      },
      {
        "BlockNum": 5889,
        "Hash": "137e56be8966eba0c04138d79faa1515997fc790ccf5213c00bb13a3550cca39"
      }
    ],
    "maxPages": 590
  }
}
```

Returns a paginated list of up to **10** Directory Service (DS) blocks and their block hashes for a specified page. The `maxPages` variable that specifies the maximum number of pages available is also returned.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTxBlock("40"))
```

```go
func GetTxBlock(t *testing.T) {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetTxBlock("40")
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
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
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetLatestTxBlock())
```

```go
func GetLatestTxBlock() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetLatestTxBlock()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "body": {
      "BlockHash": "01a61cc22ab5ae1d77cd6da65385771dca408fbea90688c845bdd2ffe1797bb7",
      "HeaderSign": "DEACD285A5D2AED23052B08BE9CEEE1C9C4C8CB69F3DF4106D87BA9B0AC067E16AA2C5D129F2318824723A2A75CA5F32632DCD4E5D8A634234E1037B6025779D",
      "MicroBlockInfos": [
        {
          "MicroBlockHash": "8cf6285c259613a79c7b5dfcfbada4f9631fa15d626037f048d1d9a9649d562c",
          "MicroBlockShardId": 0,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        },
        {
          "MicroBlockHash": "01d7da6e80b81711aaf7cdbc74bc50994f4ed99be085d451c93abe31882e8b44",
          "MicroBlockShardId": 1,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        },
        {
          "MicroBlockHash": "1eaf0a468eff13a2d7ecd33b5177fb850bdfce23bca3a330ecef951bde44eb62",
          "MicroBlockShardId": 2,
          "MicroBlockTxnRootHash": "fa80cb720f7612229909295640266eb618cc2a73dd78da17b4d68d7ffc7cce82"
        },
        {
          "MicroBlockHash": "bf86108de525ba4954e40631949ad71f7f7b0a620f350da2c736f92aa157d2ba",
          "MicroBlockShardId": 3,
          "MicroBlockTxnRootHash": "0000000000000000000000000000000000000000000000000000000000000000"
        }
      ]
    },
    "header": {
      "BlockNum": "589789",
      "DSBlockNum": "5898",
      "GasLimit": "325000",
      "GasUsed": "1",
      "MbInfoHash": "ba2a326bcc595fae5ddcbdc5d53cca06ce7c8d1d046ffb635341e3aa9d5cbb7c",
      "MinerPubKey": "0x0207FF35CFA9F3D8336430BBD09BBF9B36C283358E8CA91FAB551ACB5FE1E38B68",
      "NumMicroBlocks": 4,
      "NumTxns": 1,
      "PrevBlockHash": "be825dd949caf36d6a20372fdc88b1912dc1515d1ecf8624e6cd928b33c9a705",
      "Rewards": "1000000000",
      "StateDeltaHash": "c2c43d6a277a92df12d7d5ab5c657d6a7d823000061da5802c6354b47e56ebd5",
      "StateRootHash": "d00196c0a8f28d81e49253a1a561da79a526a47e12b4e208da20b96a6e3a1ac7",
      "Timestamp": "1590645487342412",
      "Version": 1
    }
  }
}
```

Returns the details of the most recent Transaction block.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumTxBlocks())
```

```go
func GetNumTxBlocks() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetNumTxBlocks()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "589790"
}
```

Returns the current number of Transaction blocks in the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTxBlockRate())
```

```go
func GetTxBlockRate() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetTxBlockRate()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 0.014138050978963283
}
```

Returns the current Transaction blockrate per second for the network.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTxBlockListing(1))
```

```go

func TxBlockListing() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.TxBlockListing(1)
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "data": [
      {
        "BlockNum": 589790,
        "Hash": "E0743F8E0CAEFB4DD6B15D9A5B71975CD1CFFC453EC57F85541E224A9C60B4E8"
      },
      {
        "BlockNum": 589789,
        "Hash": "01a61cc22ab5ae1d77cd6da65385771dca408fbea90688c845bdd2ffe1797bb7"
      },
      {
        "BlockNum": 589788,
        "Hash": "be825dd949caf36d6a20372fdc88b1912dc1515d1ecf8624e6cd928b33c9a705"
      },
      {
        "BlockNum": 589787,
        "Hash": "4d097b9e283dd2bfeb78f2bb6ef9fe960b45b96e027f999316cea4c3d8f70ea9"
      },
      {
        "BlockNum": 589786,
        "Hash": "1714472999972237b887db32cc6e27c44dc4ceecdc310ae3b18f44673e860d87"
      },
      {
        "BlockNum": 589785,
        "Hash": "a40cb278801b22609245e240c1386894829d36ec2c081cf33d6b0f11cb6d6c70"
      },
      {
        "BlockNum": 589784,
        "Hash": "e6a66682866dec2b44124b0daa419696cca396bc04ab2d342a65b43db5cbd24e"
      },
      {
        "BlockNum": 589783,
        "Hash": "a7be65da85167c2cd0b044698a3e7dc74e2478b367f87d85536d4c108d9fde96"
      },
      {
        "BlockNum": 589782,
        "Hash": "060b06d40fcca1cedb9099031e1cb37927700bc263f14a3b05481f1f9b211b7c"
      },
      {
        "BlockNum": 589781,
        "Hash": "db190feb1f2099875ca2dc9734efbeb5b1cef676f85d7fa9a4b84d64a9e463b6"
      }
    ],
    "maxPages": 58980
  }
}
```

Returns a paginated list of up to **10** Transaction blocks and their block hashes for a specified page. The `maxPages` variable that specifies the maximum number of pages available is also returned.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumTransactions())
```

```go
func GetNumTransactions() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetNumTransactions()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "4350695"
}
```

Returns the current number of validated Transactions in the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTransactionRate())
```

```go
func GetTransactionRate() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetTransactionRate()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 9.169180550334216
}
```

Returns the current Transaction rate per second **(TPS)** of the network. <br> This is represented as an `Number`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetCurrentMiniEpoch())
```

```go
func GetCurrentMiniEpoch() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetCurrentMiniEpoch()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "589793"
}
```

Returns the current TX block number of the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetCurrentDSEpoch())
```

```go
func GetCurrentDSEpoch() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetCurrentDSEpoch()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "5898"
}
```

Returns the current number of DS blocks in the network. <br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetPrevDifficulty())
```

```go
func GetPrevDifficulty() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetPrevDifficulty()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 91
}
```

Returns the minimum shard difficulty of the previous block. <br> This is represented as an `Number`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetPrevDSDifficulty())
```

```go
func GetPrevDSDifficulty() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetPrevDSDifficulty()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": 149
}
```

Returns the minimum DS difficulty of the previous block. <br> This is represented as an `Number`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```go
func GetTotalCoinSupply() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetTotalCoinSupply()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "13452081092.277490607172"
}
```

Returns the total supply (ZIL) of coins in the network. This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

### ARGUMENTS

| Parameter | Type   | Required | Description            |
| --------- | ------ | -------- | ---------------------- |
| `id`      | string | Required | `"1"`                  |
| `jsonrpc` | string | Required | `"2.0"`                |
| `method`  | string | Required | `"GetTotalCoinSupply"` |
| `params`  | string | Required | Empty string `""`      |

## GetMinerInfo

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetMinerInfo",
    "params": ["5500"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
```

```java

```

```ruby

```

```python

```

```go

```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "dscommittee": [
      "0x03F25E4B68050496086758C33D16C47792F18D1102BB5DFC0CE5E3A57927008A0B",
      "0x03CF937B2EBE194C72350A6A7E6612C2D8636A33753929F1553E6273442B2F8E5B",
      "0x0372E43C4E7960F02E10F5AFE800E903579E2BE853B160681CBDF7C048FFB78A0F",
      ..."0x0397FD33ED459AD72939CA531385271311DA74094D89109F3876E81BEE84B4E414"
    ],
    "shards": [
      {
        "nodes": [
          "0x0245C0DDAA493700F86A3943260EB04D05DEBD62897E3EC51AE65A704E5C65C0A6",
          "0x0250CF4B40C0C984F2BB005599D2A7503F9C68F701A24CBC10B1EB2533575ADBA7",
          "0x023F2F657F170563E9B28BF837AB295FD13A7E2A4117DB44B2ADFE536F28D28102",
          ..."0x02358F60B4BD90805E6940A901E3C3A5867FFF5BDBD5AD9BFD66FE47C9FA6F1035"
        ],
        "size": 535
      },
      {
        "nodes": [
          "0x02646640964F472CBE1E9BAF2DC5F1A0915AE529DDFF08F28DDE3E460C755DC8C4",
          "0x025EC6741880EC217F921A8FFB4AACDB95FF6477E1BB66CB39950FB2723D3740C8",
          "0x03DE42F6719E8A0147A93604C5F6A4304D14AD5F6A70C011EE37DBFC65D1E7F842",
          ..."0x02B1DB735BF54FC5765D89248DA1C07934282182F3C65CD9152D8F48C539BB5C53"
        ],
        "size": 535
      },
      {
        "nodes": [
          "0x0218C2BA9876BCF3EE9EFF220C9F4CF433F5BE09D9D592F3C657AE7353CFFC3245",
          "0x02BCD61D2F47165E0CD6B3CF9429140C3F017C440DA63E9F44A84503A7D1E41590",
          "0x03E7699C19CFF554D265DC9C797713A7403D99A607EA7C8794259150436EB9FFBB",
          ..."0x031169CB469B6083954F578C19FC7833A90D835AA75942820119272FC6EE4361A5"
        ],
        "size": 534
      }
    ]
  }
}
```

Returns the mining nodes (i.e., the members of the DS committee and shards) at the specified DS block.

**Notes:**

1. Nodes owned by Zilliqa Research are omitted.
2. `dscommittee` has no `size` field since the DS committee size is fixed for a given chain.
3. For the Zilliqa mainnet, this API is only available from DS block 5500 onwards.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                        |
| --------- | ------ | -------- | ---------------------------------- |
| `id`      | string | Required | `"1"`                              |
| `jsonrpc` | string | Required | `"2.0"`                            |
| `method`  | string | Required | `"GetMinerInfo"`                   |
| `params`  | string | Required | DS block number. Example: `"5500"` |

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
  gasLimit: Long.fromNumber(1),
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

```go
func SendTransaction() {
	wallet := NewWallet()
	wallet.AddByPrivateKey("e19d05c5452598e24caad4a0d85a49146f7be089515c905ae6a19e8a578a6930")
	provider := provider2.NewProvider("https://api.zilliqa.com/")

	tx := &transaction.Transaction{
		Version:      strconv.FormatInt(int64(util.Pack(1, 1)), 10),
		SenderPubKey: "0246E7178DC8253201101E18FD6F6EB9972451D121FC57AA2A06DD5C111E58DC6A",
		ToAddr:       "4BAF5faDA8e5Db92C3d3242618c5B47133AE003C",
		Amount:       "10000000",
		GasPrice:     "1000000000",
		GasLimit:     "1",
		Code:         "",
		Data:         "",
		Priority:     false,
	}

	err := wallet.Sign(tx, *provider)
	if err != nil {
		fmt.Println(err)
	}

	rsp := provider.CreateTransaction(tx.ToTransactionPayload())

	if rsp.Error != nil {
		fmt.Println(rsp.Error)
	} else {
		result := rsp.Result.(map[string]interface{})
		hash := result["TranID"].(string)
		fmt.Printf("hash is %s\n", hash)
		tx.Confirm(hash, 1000, 3, provider)
	}
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "Info": "Non-contract txn, sent to shard",
    /*
    Other possible Info:
    Contract Creation txn, sent to shard
    Contract Txn, Shards Match of the sender and reciever
    Contract Txn, Sent To Ds
    */
    "TranID": "2d1eea871d8845472e98dbe9b7a7d788fbcce226f52e4216612592167b89042c"
  }
}
```

Create a new Transaction object and send it to the network to be process. <br> See [Quick Start](https://github.com/Zilliqa/Zilliqa-JavaScript-Library#quick-start) in Javascript-SDK for an example of how to construct a Transaction object.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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
| `gasLimit`  | string  | Required | The amount of gas units that is needed to be process this transaction. <br><br> **-** For **regular transaction**, please use `"1"`. <br> **-** For **smart contract transaction**, please consult the [gas documentation](https://github.com/Zilliqa/scilla-docs/blob/master/docs/texsources/gas-costs/gas-doc.pdf).                                                                                                                      |
| `code`      | string  | Optional | The smart contract source code. This is present only when deploying a new contract.                                                                                                                                                                                                                                                                                                                                                        |
| `data`      | string  | Optional | `String`-ified JSON object specifying the transition parameters to be passed to a specified smart contract. <br><br> - When creating a contract, this JSON object contains the **init** parameters. <br> - When calling a contract, this JSON object contains the **msg** parameters. <br><br> _For more information on the Scilla interpreter, please visit the [documentation](https://scilla.readthedocs.io/en/latest/interface.html)._ |
| `signature` | string  | Required | An **EC-Schnorr** signature of 64 bytes of the entire Transaction object as stipulated above.                                                                                                                                                                                                                                                                                                                                              |
| `priority`  | boolean | Optional | A flag for this transaction to be processed by the DS committee. <br><br> This is only required for [Category III transactions](https://blog.zilliqa.com/provisioning-sharding-for-smart-contracts-a-design-for-zilliqa-cd8d012ee735).                                                                                                                                                                                                     |

## GetTransaction

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTransaction",
    "params": ["cd8727674bc05e0ede405597a218164e1c13c7103b9d0ba43586785f3d8cede5"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const txn = await zilliqa.blockchain.getTransaction(
  "cd8727674bc05e0ede405597a218164e1c13c7103b9d0ba43586785f3d8cede5"
);
console.log(txn.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<Transaction> transaction = client.getTransaction("cd8727674bc05e0ede405597a218164e1c13c7103b9d0ba43586785f3d8cede5");
        System.out.println(new Gson().toJson(transaction));
    }
}
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTransaction("cd8727674bc05e0ede405597a218164e1c13c7103b9d0ba43586785f3d8cede5"))
```

```go
func GetTransaction() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetTransaction("cd8727674bc05e0ede405597a218164e1c13c7103b9d0ba43586785f3d8cede5")
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
// Note: If the transaction is a for payment.
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "ID": "cd8727674bc05e0ede405597a218164e1c13c7103b9d0ba43586785f3d8cede5",
    "amount": "24999000000000",
    "gasLimit": "1",
    "gasPrice": "1000000000",
    "nonce": "1",
    "receipt": {
      "cumulative_gas": "1",
      "epoch_num": "589763",
      "success": true
    },
    "senderPubKey": "0x0347B5C6833ABD2AC0A6A7D85CF6BD0CC18084F6260B0C9DD2D491015BF2D47862",
    "signature": "0x593454623A6CE0FEA287E42583445B140F696F79CA508762B8AB44F202686CFA115A2AC36C31E643C9EB0D46A4E6CA8C4EEFD78D7E9A25220DC512C13C9600F0",
    "toAddr": "9148616bfdfab321bdd626682a8c446e193eabb2",
    "version": "65537"
  }
}
```

```json
// Note: If the transaction is for contract deployment.
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "ID": "f9170f9661a2ec5a90e6701618ba38d76257c00a1e5848d8f541e1ef52d11ede",
    "amount": "0",
    "code": "scilla_version 0\n\nimport BoolUtils IntUtils\n\n(* Twitter contract *)\n\n(***************************************************)\n(*               Associated library                *)\n(***************************************************)\nlibrary SocialPay\n\nlet one_msg =\n    fun (msg : Message) =>\n    let nil_msg = Nil {Message} in\n    Cons {Message} msg nil_msg\n\nlet two_msgs =\nfun (msg1 : Message) =>\nfun (msg2 : Message) =>\n  let msgs_tmp = one_msg msg2 in\n  Cons {Message} msg1 msgs_tmp\n\nlet is_valid_substring =\n  fun (tweet_text : String) =>\n  fun (start_pos : Uint32) =>\n  fun (hashtag_len : Uint32) =>\n    let string_length = builtin strlen tweet_text in\n    let valid_start_pos = builtin lt start_pos string_length in\n    let end_pos = builtin add start_pos hashtag_len in\n    let valid_end_pos = uint32_le end_pos string_length in\n    andb valid_start_pos valid_end_pos\n\n(* Error events *)\ntype Error =\n  | CodeNotAuthorized\n  | CodeRegisteredWithinWeek\n  | CodeUserNotRegistered\n  | CodeTweetAlreadyExists\n  | CodeTweetNotValid\n  | CodeTweetWithinDay\n\nlet make_error =\n  fun (result : Error) =>\n    let result_code = \n      match result with\n      | CodeNotAuthorized        => Int32 -1\n      | CodeRegisteredWithinWeek => Int32 -2\n      | CodeUserNotRegistered    => Int32 -3\n      | CodeTweetAlreadyExists   => Int32 -4\n      | CodeTweetNotValid        => Int32 -5\n      | CodeTweetWithinDay       => Int32 -6\n      end\n    in\n    { _exception : \"Error\"; code : result_code }\n\nlet tt = True\n\n(***************************************************)\n(*             The contract definition             *)\n(***************************************************)\n\ncontract SocialPay\n(\n    owner: ByStr20,\n    hashtag: String,\n    zils_per_tweet : Uint128,\n    blocks_per_day : Uint32,\n    blocks_per_week : Uint32,\n    donation_address : ByStr20\n)\n\n(* Map of tweet_id to recipient address *)\nfield verified_tweets: Map String ByStr20 = Emp String ByStr20\n\n(* Map of twitter_id to last withdraw block number *)\nfield last_withdrawal: Map String BNum = Emp String BNum\n\n(* Map of address to bool status of admin *)\nfield admins: Map ByStr20 Bool = Emp ByStr20 Bool\n\n(* Map of twitter_id to recipient address *)\nfield registered_users: Map String ByStr20 = Emp String ByStr20\n\n(* Emit Errors *)\nprocedure ThrowError(err: Error)\n  e = make_error err;\n  throw e\nend\n\nprocedure IsOwner(address: ByStr20)\n  is_owner = builtin eq address owner;\n  match is_owner with\n  | True =>\n  | False =>\n    err = CodeNotAuthorized;\n    ThrowError err\n  end\nend\n\nprocedure IsAdmin()\n  is_admin <- exists admins[_sender];\n  match is_admin with\n  | True =>\n  | False =>\n    err = CodeNotAuthorized;\n    ThrowError err\n  end\nend\n\nprocedure ConfigureAdmin(admin_address: ByStr20)\n  is_admin <- exists admins[admin_address];\n  match is_admin with\n  | True =>\n      delete admins[admin_address];\n      e = {_eventname : \"DeletedAdmin\"; admin_address: admin_address};\n      event e\n  | False =>\n      admins[admin_address] := tt;\n      e = {_eventname : \"AddedAdmin\"; admin_address: admin_address};\n      event e\n  end\nend\n\n(* Only owner can deposit ZIL *)\ntransition Deposit()\n  IsOwner _sender;\n  accept;\n  e = {_eventname : \"DepositSuccessful\"; sender: _sender; deposit_amount: _amount};\n  event e\nend\n\ntransition ConfigureAdmins(admin_addresses: List ByStr20)\n  IsOwner _sender;\n  forall admin_addresses ConfigureAdmin\nend\n\ntransition ConfigureUsers(twitter_id: String, recipient_address: ByStr20)\n  IsAdmin;\n  is_registered <- exists registered_users[twitter_id];\n  match is_registered with\n  | True =>\n      current_block <- & BLOCKNUMBER;\n      withdrawal <- last_withdrawal[twitter_id];\n      not_next_week_yet =\n          match withdrawal with\n          | Some last_withdraw_block =>\n              let next_week_block = builtin badd last_withdraw_block blocks_per_week in\n              builtin blt current_block next_week_block\n          | None =>\n              False\n          end;\n      match not_next_week_yet with\n      | True =>\n          err = CodeRegisteredWithinWeek;\n          ThrowError err\n      | False =>\n          registered_users[twitter_id] := recipient_address;\n          e = {_eventname : \"ConfiguredUserAddress\"; twitter_id: twitter_id; recipient_address: recipient_address};\n          event e\n      end\n  | False =>\n      registered_users[twitter_id] := recipient_address;\n      e = {_eventname : \"ConfiguredUserAddress\"; twitter_id: twitter_id; recipient_address: recipient_address};\n      event e\n  end\nend\n\n(* Only admins can call this transition                                         *)\n(* The following conditions are checked for (in that order):                    *)\n(*   1. Owner initiates the transition.                                         *)\n(*   2. The tweeter is already registered in the app his/her wallet             *)\n(*   3. The tweet hasn't been awarded before.                                   *)\n(*   4. Substring specs (start_pos) is valid.                                   *)\n(*   5. The substring matches the preset hashtag.                               *)\n(*   6. Sufficient time (blocks) have passed since the user was awarded before. *)\ntransition VerifyTweet (twitter_id: String, tweet_id: String, tweet_text: String, start_pos: Uint32)\n  IsAdmin;\n  get_recipient_address <- registered_users[twitter_id];\n  match get_recipient_address with\n  | None =>\n      err = CodeUserNotRegistered;\n      ThrowError err\n  | Some recipient_address =>\n      already_verified <- exists verified_tweets[tweet_id];\n      not_already_verified = negb already_verified;\n      hashtag_len = builtin strlen hashtag;\n      valid_substring = is_valid_substring tweet_text start_pos hashtag_len;\n      is_valid = andb valid_substring not_already_verified;\n      match is_valid with\n      | False =>\n          match already_verified with\n          | True =>\n              err = CodeTweetAlreadyExists;\n              ThrowError err\n          | False =>\n              err = CodeTweetNotValid;\n              ThrowError err\n          end\n      | True =>\n          match_hashtag = builtin substr tweet_text start_pos hashtag_len;\n          is_hashtag = builtin eq match_hashtag hashtag;\n          match is_hashtag with\n          | False =>\n              err = CodeTweetNotValid;\n              ThrowError err\n          | True =>\n              withdrawal <- last_withdrawal[twitter_id];\n              current_block <- & BLOCKNUMBER;\n              not_next_day_yet =\n                  match withdrawal with\n                  | Some last_withdraw_block =>\n                      let next_day_block = builtin badd last_withdraw_block blocks_per_day in\n                      builtin blt current_block next_day_block\n                  | None =>\n                      False\n                  end;\n              match not_next_day_yet with\n              | True =>\n                  err = CodeTweetWithinDay;\n                  ThrowError err\n              | False =>\n                  verified_tweets[tweet_id] := recipient_address;\n                  last_withdrawal[twitter_id] := current_block;\n                  e = {\n                          _eventname : \"VerifyTweetSuccessful\";\n                          sender: _sender;\n                          recipient: recipient_address;\n                          twitter_id: twitter_id;\n                          tweet_id: tweet_id;\n                          reward_amount: zils_per_tweet;\n                          matched_donation: zils_per_tweet\n                      };\n                  event e;\n                  msg_to_recipient = { \n                    _tag: \"\";\n                    _recipient: recipient_address;\n                    _amount: zils_per_tweet \n                  };\n                  msg_to_donation = {\n                    _tag: \"\";\n                    _recipient: donation_address;\n                    _amount: zils_per_tweet\n                  };\n                  msgs = two_msgs msg_to_recipient msg_to_donation;\n                  send msgs\n              end\n          end\n      end\n  end\nend\n\ntransition ReturnFund ()\n  IsOwner _sender;\n  current_bal <- _balance;\n  e = {\n    _eventname : \"ReturnFundSuccessful\";\n    returned_amount: current_bal\n  };\n  event e;\n  msg = {\n      _tag       : \"\";\n      _recipient : owner;\n      _amount    : current_bal\n  };\n  msgs = one_msg msg;\n  send msgs\nend",
    "data": "[{\"vname\":\"owner\",\"value\":\"0xf1a3d56321D6C0C9825bf3c34CB843719e99cBCA\",\"type\":\"ByStr20\"},{\"vname\":\"hashtag\",\"value\":\"#zilcovidheroes\",\"type\":\"String\"},{\"vname\":\"zils_per_tweet\",\"value\":\"25000000000000\",\"type\":\"Uint128\"},{\"vname\":\"blocks_per_day\",\"value\":\"1600\",\"type\":\"Uint32\"},{\"vname\":\"blocks_per_week\",\"value\":\"1600\",\"type\":\"Uint32\"},{\"vname\":\"donation_address\",\"value\":\"0x7AEB68fc38B29387D2e100db1E42c883C0519548\",\"type\":\"ByStr20\"},{\"vname\":\"_scilla_version\",\"type\":\"Uint32\",\"value\":\"0\"}]",
    "gasLimit": "25000",
    "gasPrice": "1000000000",
    "nonce": "9",
    "receipt": {
      "cumulative_gas": "10481",
      "epoch_num": "586524",
      "success": true
    },
    "senderPubKey": "0x020B94FDA851E2BF9392FF13D7CA33B417C5B95BCD0965238FF5074B7C8D31BC0D",
    "signature": "0x16196121EFEA86C9D91102EA200F02C88744E82B886C7AF72256F18615ADEE38EC18AFEE2739615896C5306F3C2642AA98CDFE113AC64A55981BBC2C82D31592",
    "toAddr": "0000000000000000000000000000000000000000",
    "version": "65537"
  }
}
```

```json
// Note: If the transaction is for contract call.
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "ID": "52605cee6955b3d14f5478927a90977b305325aff4ae0a2f9dbde758e7b92ad4",
    "amount": "50000000000000",
    "data": "{\"_tag\":\"sendFunds\",\"params\":[{\"vname\":\"accountValues\",\"type\":\"List (AccountValue)\",\"value\":[{\"constructor\":\"AccountValue\",\"argtypes\":[],\"arguments\":[\"0xc0e28525e9d329156e16603b9c1b6e4a9c7ed813\",\"50000000000000\"]}]}]}",
    "gasLimit": "25000",
    "gasPrice": "1000000000",
    "nonce": "3816",
    "receipt": {
      "accepted": true,
      "cumulative_gas": "878",
      "epoch_num": "589742",
      "success": true,
      "transitions": [
        {
          "addr": "0x9a65df55b2668a0f9f5f749267cb351a37e1f3d9",
          "depth": 0,
          "msg": {
            "_amount": "50000000000000",
            "_recipient": "0xc0e28525e9d329156e16603b9c1b6e4a9c7ed813",
            "_tag": "onFundsReceived",
            "params": []
          }
        }
      ]
    },
    "senderPubKey": "0x03DE40DF885B0E334D53FF5E5554589AAF46F2339FEBEE93213F2CCE52D1F488F4",
    "signature": "0xB19AB66C4410EE4833A9C5DEE600471DB4D711F6B61D2312988E6E70CC655409F18BB42BB6940B6263C8EA5CE08CAEC06111BDF19BE00D7E15F25515CAA45DAA",
    "toAddr": "9a65df55b2668a0f9f5f749267cb351a37e1f3d9",
    "version": "65537"
  }
}
```

```json
// Note: If the transaction has failed.
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "ID": "9b00b3b7d80dfb3818a6aaab0cb6fd3822b1bd7b3c6d5c6260579d12ae631a96",
    "amount": "0",
    "data": "{\"_tag\":\"ConfigureUsers\",\"params\":[{\"vname\":\"twitter_id\",\"type\":\"String\",\"value\":\"111111111\"},{\"vname\":\"recipient_address\",\"type\":\"ByStr20\",\"value\":\"0xAA9AC51920c75bDe16C8c27E529eDaFfcb15f530\"}]}",
    "gasLimit": "9000",
    "gasPrice": "1000000000",
    "nonce": "8260",
    "receipt": {
      "cumulative_gas": "1220",
      "epoch_num": "588004",
      "errors": {
        "0": [
          7
        ]
      },
      "exceptions": [
        {
          "line": 87,
          "message": "Exception thrown: (Message [(_exception : (String \"Error\")) ; (code : (Int32 -2))])"
        },
        {
          "line": 100,
          "message": "Raised from IsAdmin"
        },
        {
          "line": 137,
          "message": "Raised from ConfigureUsers"
        }
      ],
      "success": false
    },
    "senderPubKey": "0x037B1722AAE35694A9F6E6C57DF5DD1274CBF568463AB50CEB6CBAD18C9BE291AA",
    "signature": "0x26676494B528757E602943DD2524277ED3850FE3F8E1060E8F36D8E18B5CB6D347698DB00DF0DD2C6786594BF420585ECA30D030C56FE946574AAD59456F110B",
    "toAddr": "7587a6d9b4def93c9c02475f5854c45eb4d9dac4",
    "version": "65537"
  }
}
```

Returns the details of a specified Transaction.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                              |
| --------- | ------ | -------- | -------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                    |
| `jsonrpc` | string | Required | `"2.0"`                                                  |
| `method`  | string | Required | `"GetTransaction"`                                       |
| `params`  | string | Required | Transaction hash of 32 bytes of a specified transaction. |

## GetPendingTxn

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetPendingTxn",
    "params": ["b9e545ab3ed0b61a4d326425569605255e0990da7dda18b4658fdb17b390844e"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const pendingTransaction = await zilliqa.blockchain.getPendingTxn(txId);
console.log(pendingTransaction.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<PendingStatus> pengdingStatus = client.getPendingTxn("b9e545ab3ed0b61a4d326425569605255e0990da7dda18b4658fdb17b390844e");
        System.out.println(new Gson().toJson(pengdingStatus));
    }
}
```

```go
func GetPendingTxn() {
  provider := NewProvider("https://api.zilliqa.com/")
  response := provider.GetPendingTxn("2cf109b25f2132c08a4248e2be8add6b95b92aef5b2c77e737faefbc9353ee7c")
  result, _ := json.Marshal(response)
  fmt.Println(string(result))
}
```

> **Example response:**

> **Since Zilliqa V6.3.0**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "code": 24,
    "confirmed": false,
    "pending": false
  }
}
```

> **Zilliqa V6.2.0 and before**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "code": 0,
    "confirmed": false,
    "info": "Txn not pending"
  }
}
```

Returns the status (code) of a specified unconfirmed Transaction.

### API AVAILABILITY

Please note that the status of newly created transactions (using `CreateTransaction`) may not immediately be available for checking using this API.

A created transaction will be included in this API if:

1. It has already been dispatched to the network (this may require one transaction epoch)
2. The network has acknowledged receiving this transaction (this occurs at the end of every transaction epoch)

Hence, we recommend calling `GetPendingTxn` around 1-2 transaction epochs after transaction creation to get accurate results.

### STATUS CODES

From Zilliqa `V7.0.0` onwards

**Confirmed Transactions**

| `code` | Transaction Status            |
| ------ | ----------------------------- |
| 3      | Transaction is confirmed      |
| 2      | Transaction is soft-confirmed |

**Pending Transactions**

| `code` | Transaction Status             |
| ------ | ------------------------------ |
| 4      | Nonce is higher than expected  |
| 5      | Microblock gas limit exceeded  |
| 6      | Consensus failure in network   |

**Dispatched Transactions**

| `code` | Transaction Status                      |
| ------ | --------------------------------------- |
| 1      | Transaction was received by the lookup  |

**Dropped / Rejected Transactions**

| `code` | Transaction Status                          |
| ------ | ------------------------------------------- |
| 10     | Transaction caused math error               |
| 11     | Scilla invocation error                     |
| 12     | Contract account initialization error       |
| 13     | Invalid source account                      |
| 14     | Gas limit higher than shard gas limit       |
| 15     | Unknown transaction type                    |
| 16     | Transaction sent to wrong shard             |
| 17     | Contract & source account cross-shard issue |
| 18     | Code size exceeded limit                    |
| 19     | Transaction verification failed             |
| 20     | Gas limit too low                           |
| 21     | Insufficient balance                        |
| 22     | Insufficient gas to invoke Scilla checker   |
| 23     | Duplicate transaction exists                |
| 24     | Transaction with same nonce but higher(or same) gas price exists in the pool |
| 25     | Invalid destination address                 |
| 26     | Failed to add contract account to state     |
| 27     | A txn with same nonce was already confirmed |

_Note: Dropped transactions are available for querying for up to 5 transaction epochs only._

Zilliqa `V6.2.0`

| `confirmed` | `code` | `info`                                           |
| ----------- | ------ | ------------------------------------------------ |
| false       | 0      | Txn not pending                                  |
| false       | 1      | Nonce too high                                   |
| false       | 2      | Could not fit in as microblock gas limit reached |
| false       | 3      | Transaction valid but consensus not reached      |

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                              |
| --------- | ------ | -------- | -------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                    |
| `jsonrpc` | string | Required | `"2.0"`                                                  |
| `method`  | string | Required | `"GetPendingTxn"`                                        |
| `params`  | string | Required | Transaction hash of 32 bytes of a specified transaction. |

## GetPendingTxns

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetPendingTxns",
    "params": []
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const pendingTransaction = await zilliqa.blockchain.getPendingTxns();
console.log(pendingTransaction.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<PendingStatus> pengdingStatus = client.getPendingTxns();
        System.out.println(new Gson().toJson(pengdingStatus));
    }
}
```

```go
func GetPendingTxns() {
  provider := NewProvider("https://api.zilliqa.com/")
  response := provider.GetPendingTxns()
  result, _ := json.Marshal(response)
  fmt.Println(string(result))
}
```

> **Example response:**

> **Since Zilliqa V6.3.0**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "Txns": [
      {
        "TxnHash": "ec5ef8110a285563d0104269081aa77820058067091a9b3f3ae70f38b94abda3",
        "code": 1
      },
      {
        "TxnHash": "cf546d80fa2e0cc0b5b8f9fbb639050fe292d1601aa5d4a7c48106c624311bf9",
        "code": 24
      }
    ]
  }
}
```

> **Zilliqa V6.2.0 and before**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {
    "Txns": [
      {
        "Status": 1,
        "TxnHash": "ec5ef8110a285563d0104269081aa77820058067091a9b3f3ae70f38b94abda3",
      }
    ]
  }
}
```

Returns the status (code) of all unconfirmed Transactions.

Please refer to [GetPendingTxn](#getpendingtxn) for details on API availability and status codes.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

### ARGUMENTS

| Parameter | Type   | Required | Description        |
| --------- | ------ | -------- | ------------------ |
| `id`      | string | Required | `"1"`              |
| `jsonrpc` | string | Required | `"2.0"`            |
| `method`  | string | Required | `"GetPendingTxns"` |
| `params`  | None   |          |                    |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetRecentTransactions())
```

```go
func GetRecentTransactions() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetRecentTransactions()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}

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
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTransactionsForTxBlock("2"))
```

```go
func GetTransactionsForTxBlock() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetTransactionsForTxBlock("1")
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
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

Returns the validated transactions included within a specified final transaction block as an array of length _i_, where _i_ is the number of shards plus the DS committee. The transactions are grouped based on the group that processed the transaction. The first element of the array refers to the first shard. The last element of the array at index, _i_, refers to the transactions processed by the DS Committee.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                        |
| --------- | ------ | -------- | -------------------------------------------------- |
| `id`      | string | Required | `"1"`                                              |
| `jsonrpc` | string | Required | `"2.0"`                                            |
| `method`  | string | Required | `"GetTransactionsForTxBlock"`                      |
| `params`  | string | Required | Specifed TX block number to return. Example: `"2"` |

## GetTxnBodiesForTxBlock

> **Example request:**

```shell
curl -d '{
    "id": "1",
    "jsonrpc": "2.0",
    "method": "GetTxnBodiesForTxBlock",
    "params": ["2"]
}' -H "Content-Type: application/json" -X POST "https://api.zilliqa.com/"
```

```javascript
const txns = await zilliqa.blockchain.getTxnBodiesForTxBlock("2");
console.log(txns.result);
```

```java
public class App {
    public static void main(String[] args) throws IOException {
        HttpProvider client = new HttpProvider("https://api.zilliqa.com");
        Rep<List<List<String>>> transactionList = client.getTxnBodiesForTxBlock("2");
        System.out.println(new Gson().toJson(transactionList));
    }
}
```

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetTxnBodiesForTxBlock("2"))
```

```go
func GetTxnBodiesForTxBlock() {
  provider := NewProvider("https://api.zilliqa.com/")
  response := provider.GetTxnBodiesForTxBlock("1")
  result, _ := json.Marshal(response)
  fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": [
    {
      "ID": "562432bc45c14c788c43c469756453375cbe80cc9c1bc30fa0dfbe77e4220221",
      "amount": "1",
      "gasLimit": "1",
      "gasPrice": "1000000000",
      "nonce": "1",
      "receipt": {
        "cumulative_gas": "1",
        "epoch_num": "2",
        "success": true
      },
      "senderPubKey": "0x03393C256D33127CE18FC3646EC88FCE62DBF661300B4017E2FE57E8023B55BCFE",
      "signature": "0xCC12816DCE156FECFA1D6EF129D13FA2A5677E159CDF0CAFADF2CD33FBA0D239EE1284D4083BFBA4B895B97419FE78AB249C99AA7A7B7F314F17D353F44E784D",
      "toAddr": "b07065cfde6060ad36af3913c65bfb04211608d1",
      "version": "131073"
    },
    {
      "ID": "9ebc07e3e15b08dd82b2f2d57eead1b7dea4d06bef33364bbec5f80fc1d1d130",
      "amount": "2",
      "gasLimit": "1",
      "gasPrice": "1000000000",
      "nonce": "2",
      "receipt": {
        "cumulative_gas": "1",
        "epoch_num": "2",
        "success": true
      },
      "senderPubKey": "0x03393C256D33127CE18FC3646EC88FCE62DBF661300B4017E2FE57E8023B55BCFE",
      "signature": "0x846D90B698B4739979AB8B7F25BDEE5125A36447770D4AC6386606ACD25704747B38DEDE85F0AD26A663F0863199CA336109EB080A6354BB7CC3683C8FC47796",
      "toAddr": "b07065cfde6060ad36af3913c65bfb04211608d1",
      "version": "131073"
    }
  ]
}
```

Returns the validated transactions (in verbose form) included within a specified final transaction block.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                        |
| --------- | ------ | -------- | -------------------------------------------------- |
| `id`      | string | Required | `"1"`                                              |
| `jsonrpc` | string | Required | `"2.0"`                                            |
| `method`  | string | Required | `"GetTxnBodiesForTxBlock"`                         |
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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumTxnsTxEpoch())
```

```go
func GetNumTxnsTxEpoch() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetNumTxnsTxEpoch()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "38"
}
```

Returns the number of validated transactions included in this Transaction epoch. <br> This is represented as `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetNumTxnsDSEpoch())
```

```go
func GetNumTxnsDSEpoch() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetNumTxnsDSEpoch()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "416"
}
```

Returns the number of validated transactions included in this DS epoch. <br> This is represented as `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetMinimumGasPrice())
```

```go
func GetMinimumGasPrice() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetMinimumGasPrice()
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": "1000000000"
}
```

Returns the minimum gas price for this DS epoch, measured in the smallest price unit **Qa** (or 10^-12 **Zil**) in Zilliqa.
<br> This is represented as a `String`.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetSmartContractCode("fe001824823b12b58708bf24edd94d8b5e1cfcf7"))
```

```go
func GetSmartContractCode() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetSmartContractCode("fe001824823b12b58708bf24edd94d8b5e1cfcf7")
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
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
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetSmartContractInit("fe001824823b12b58708bf24edd94d8b5e1cfcf7"))
```

```go
func GetSmartContractInit() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetSmartContractInit("fe001824823b12b58708bf24edd94d8b5e1cfcf7")
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
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
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetSmartContractSubState("fe001824823b12b58708bf24edd94d8b5e1cfcf7","admins",[]))
```

```go
func GetSmartContractSubState() {
	provider := NewProvider("https://zilliqa.com")
	response, _ := provider.GetSmartContractSubState("9611c53BE6d1b32058b2747bdeCECed7e1216793", "admins", []interface{}{})
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

```json
{
  "admins": {
    "0xdfa89866ae86632b36361d53b76c1373448c28fa": {
      "argtypes": [],
      "arguments": [],
      "constructor": "True"
    }
  }
}
```

Returns the state (or a part specified) of a smart contract address, represented in a JSON format.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                  |
| --------- | ------ | -------- | ---------------------------- |
| `id`      | string | Required | `"1"`                        |
| `jsonrpc` | string | Required | `"2.0"`                      |
| `method`  | string | Required | `"GetSmartContractSubState"` |
| `params`  | array  | Required | State params                 |

### STATE PARAMS

| Parameter       | Type       | Required     | Description                                                           |
| --------------- | ---------- | ------------ | --------------------------------------------------------------------- |
| `Address`       | string     | Required     | A smart contract address of 20 bytes.                                 |
| `Variable Name` | string     | Can be empty | Name of the variable in the Smart Contract                            |
| `Indices`       | JSON Array | Can be empty | If the variable is of map type, you can specify an index (or indices) |

The `params` is JSON array <br> Example: `"params"`:`["fe001824823b12b58708bf24edd94d8b5e1cfcf7","admins",[\"0x9bfec715a6bd658fcb62b0f8cc9bfa2ade71434a\""]]`

_Note: If Variable Name and Indices Array are both empty, the response would be same as GetSmartContractState_

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetSmartContractState("fe001824823b12b58708bf24edd94d8b5e1cfcf7"))
```

```go
func GetSmartContractState() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetSmartContractState("fe001824823b12b58708bf24edd94d8b5e1cfcf7")
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
```

> **Example response:**

_Note: The format of response has been changed_

```json
{
  "_balance": "0",
  "admins": {
    "0xdfa89866ae86632b36361d53b76c1373448c28fa": {
      "argtypes": [],
      "arguments": [],
      "constructor": "True"
    }
  }
}
```

Returns the state (mutable) variables of a smart contract address, represented in a JSON format.

### HTTP REQUEST

| Chain(s)              | URL(s)                       |
| --------------------- | ---------------------------- |
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetContractAddressFromTransactionID(
     "AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E"
))
```

```go
func GetContractAddressFromTransactionID() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetContractAddressFromTransactionID("AAF3089596437A7C6984FA2627B6F38B5F5B80FAEAAC6993C2E82C6A8EE2615E")
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
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
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

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

```python
from pyzil.zilliqa import chain
chain.set_active_chain(chain.MainNet)
print(chain.active_chain.api.GetBalance("1eefc4f453539e5ee732b49eb4792b268c2f3908"))
```

```go
func TestGetBalance() {
	provider := NewProvider("https://api.zilliqa.com/")
	response := provider.GetBalance("9bfec715a6bd658fcb62b0f8cc9bfa2ade71434a")
	result, _ := json.Marshal(response)
	fmt.Println(string(result))
}
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
| **Zilliqa mainnet**   | https://api.zilliqa.com/     |
| **Developer testnet** | https://dev-api.zilliqa.com/ |
| **Local testnet**     | http://localhost:4201/       |
| **Isolated server**   | http://localhost:5555/       |

### ARGUMENTS

| Parameter | Type   | Required | Description                                                                                       |
| --------- | ------ | -------- | ------------------------------------------------------------------------------------------------- |
| `id`      | string | Required | `"1"`                                                                                             |
| `jsonrpc` | string | Required | `"2.0"`                                                                                           |
| `method`  | string | Required | `"GetBalance"`                                                                                    |
| `params`  | string | Required | An User's account address of 20 bytes. <br> Example: `"1eefc4f453539e5ee732b49eb4792b268c2f3908"` |
