## 1. Block
database: block_db

table: block

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|block_hash (PRIMARY KEY) | Uint256| hex_string|
|   PrevBlockHash   |   Uint256     | hex_string|
|   TransactionsRoot   |  Uint256      | hex_string|
|  BlockRoot    |    Uint256    | hex_string|
|  Timestamp    |   uint32     | BigInt|
|   Height   |   uint32     | BigInt|
|transaction_num|int|int|
|block_hex|hex|hex|

Note: 
1. 字段中没有交易transaction相关的信息

问题:
1. Notify推送的信息是十六进制字符串吗？YES

## 2. Transaction
database: transaction_db

table: transaction_deploy

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|tx_hash (PRIMARY KEY) | Uint256| hex_string|
|   Height   |   uint32     | BigInt|
|TxType| byte| 209 deploy|
|tx_hex|hex|hex|

table: transaction_invoke

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|tx_hash (PRIMARY KEY) | Uint256| hex_string|
|   Height   |   uint32     | BigInt|
|TxType| byte| 208 invoke|
|tx_hex|hex|hex|


## 3. Event (按合约建表)
### 3.1 event_native_ont
database: event_db

table: event_native_ont

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|  TxHash |  Uint256  |  hex_string | |
|  Contract_address    |  []byte    | hex    |
|method|hex|hex|
|state_hex|hex|hex|
|   Height   |   uint32     | BigInt|


### 3.2 event_native_ong
table: event_native_ong

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|  TxHash |  Uint256  |  hex_string | |
|  Contract_address    |  []byte    | hex    |
|method|hex|hex|
|state_hex|hex|hex|
|   Height   |   uint32     | BigInt|

### 3.3 event_native_ontid
table: event_native_ontid

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|  TxHash |  Uint256  |  hex_string | |
|  Contract_address    |  []byte    | hex    |
|method|hex|hex|
|state_hex|hex|hex|
|   Height   |   uint32     | BigInt|

### 3.4 event_non_native

table: event_contract_name

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|  TxHash |  Uint256  |  hex_string | |
|  Contract_address    |  []byte    | hex    |
|method|hex|hex|
|state_hex|hex|hex|
|   Height   |   uint32     | BigInt|

问题：
1.怎么命名非native的表，建议event_contractHash不会重复

## 4. Contract Deployment
database: contract_db

table: contract

| Field | Original Type  | MySQL type|
| ----------- | ----------- |-----|
|contract_hash (PRIMARY KEY) | Uint256| hex_string|
|tx_hash | Uint256| hex_string|
|   Height   |   uint32     | BigInt|
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
1. signer用公钥地址还是base58地址? base58
