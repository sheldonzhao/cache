## 1. Block
database: block_db

table: block

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|Hash (PRIMARY KEY) | Uint256| hex_string|
| Version |  uint32   | string |
|   PrevBlockHash   |   Uint256     | hex_string|
|   TransactionsRoot   |  Uint256      | hex_string|
|  BlockRoot    |    Uint256    | hex_string|
|  Timestamp    |   uint32     | BigInt|
|   Height   |   uint32     | BigInt|
|   ConsensusData   |    uint64    | string |
|   ConsensusPayload   |    []byte     | string|
|   NextBookkeeper   |    20 bytes    | hex_string |
|   Bookkeepers   |   [][]byte    | serialize and save as json type |
|   SigData  |    [][]byte  | serialize and save as json type |

Note: 
1. 字段中没有交易transaction相关的信息

问题:
1. Go代码里面的block有raw, signedAddr, nonDirectConstracted三个字段，但块信息打印出来的时候没有这三个字段
2. Notify推送的信息是十六进制字符串吗？

## 2. Transaction
database: transaction_db

table: transaction

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|Hash (PRIMARY KEY) | Uint256| hex_string|
|   Height   |   uint32     | BigInt|
|     Version       |        byte        | string |
|      Nonce      |       uint32         | BigInt|
|     GasPrice       |        uint64        |BigInt|
|    GasLimit        |     uint64           |BigInt|
|     Payer        |     20 bytes           | hex_string|
|TxType| byte| string|
|    Payload: Code       |   interface   |string          |
|     attributes       |   byte  |string           |
|Sigs| [][]byte| serialize and save as json type |

问题：
1. 我记得attributes现阶段是空值，以后会是什么类型？
2. Sigs有更好的存储方案吗？

## 3. Event (按合约建表)
### 3.1 event_native_ont
database: event_db

table: event_native_ont

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|  TxHash |  Uint256  |  hex_string |
| Action    |   string   |   string      |
|  Result    |  interface{}    |   不知道啊      |
|  Error   |    int64  |   int  |

问题：
1. result是个啥类型？

### 3.2 event_native_ong
table: event_native_ong

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|  TxHash |  Uint256  |  hex_string |
| Action    |   string   |   string      |
|  Result    |  interface{}    |   不知道啊      |
|  Error   |    int64  |   int  |

### 3.3 event_native_ontid
table: event_native_ontid

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|  TxHash |  Uint256  |  hex_string |
| Action    |   string   |   string      |
|  Result    |  interface{}    |   不知道啊      |
|  Error   |    int64  |   int  |

### 3.4 event_non_native

table: event_contract_name

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|  TxHash |  Uint256  |  hex_string |
| Action    |   string   |   string      |
|  Result    |  interface{}    |   不知道啊      |
|  Error   |    int64  |   int  |

问题：
1.怎么命名非native的表，建议event_contractHash不会重复
2.result到底是个啥类型。

## 4. Contract Deployment
database: contract_db

table: contract

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|avm_code((PRIMARY KEY))| hex_string| hex_string|
|  gasPrice     |   uint64     | BigInt|
|   gasLimit    |   uint64     | BigInt|
|  signer     |    20 bytes(address)  | hex_string|
|   needStorage    |   bool   | bool|
|  name     |   string    | string    |
|  version     |   string     | string    |
|  author     |   string     | string    |
|   email    |   string     | string    |
|   desc    |   string     | string    |

问题：
1. 我是以avm_code作为主键，唯一值嘛。但会不会太长了？
2. signer用公钥地址还是base58地址
