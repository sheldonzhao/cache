## Specification

#### Version

Now in `v2` version, all API URLs start with `/v2`

#### DTO parameter specification

Request and response parameters are in `SNAKE_CASE`  style,such as：`block_height`，`tx_hash`

#### URL specification

Follow the Restful style, define interfaces by resource,such as：`/v2/blocks`,`/v2/transactions/{tx_hash}`

#### URL request parameter specification

Multiple words are connected using underscores,such as：`/v2/blocks?page_size=10&page_number=1`

- **Page parameter**

  - page_size: number of records per page.`1<=page_size<=20`.
  - page_number: number of pages.`1<=page_number`.

- **Time parameter**

  The maximum time range is **one week**.

  - start_time: start time,unix time.
  - end_time: end time,unix time.




## 1. Block APIs

### 1.1 Get latest block list

```java
url: /v2/latest-blocks?count=10,
method: GET,
params: {
},
successResponse: {
    "code":0,
    "msg":"SUCCESS",
    "result":[
        {
            "block_hash":"63355f8e80...6c8108e4e56b264d2a",
            "block_height":112,
            "txs_root":"472af7d21a83156...75b4c0e0b1b4576531",
            "bookkeepers":"AMvXn7U9...HyqNr&AL4CDqBikrj...ZAQf2fg1AC",
            "consensus_data":"12156079575032856115",
            "block_size":532,
            "block_time":1522205080,
            "tx_count":12
        }
    ]
}
```



| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| count |   int|  amount of latest blocks. 1<=count<=50  |



| ResponseField     |     Type |   Description   |
| -------------- | --------| ------ |
|   block_hash|   String|   block hash |
|	block_height|   int|  block height |
|	txs_root|   String|  the merkleroot of all transactions in the block  |
|   bookkeepers|   String| keepers of this block,divided by `&` |
|	consensus_data	|	String|	consensus data  |
|	block_size|	int|   size of this block, unit:byte  |
|	block_time|	int|	unix time of this block|
|	tx_count|	int| the number of transactions in this block |



### 1.2 Get block list by page

```java
url：/v2/blocks?page_size=1&page_number=10,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "records":[
            {
                "block_hash":"63355f8e80...6c8108e4e56b264d2a",
                "block_height":112,
                "txs_root":"472af7d21a83156...75b4c0e0b1b4576531",
                "bookkeepers":"AMvXn7U9...HyqNr&AL4CDqBikrj...ZAQf2fg1AC",
                "consensus_data":"12156079575032856115",
                "block_size":532,
                "block_time":1522205080,
                "tx_count":12
            }
        ],
        "total":23449
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |


| ResponseField     |     Type |   Description   |
| -------------- | --------| ------ |
|   total|   int|   total blocks |


### 1.3 Get block detail by height or hash

```java
url：/v2/blocks/{param}
method：GET
successResponse：
{
	"code":0,
	"msg":"SUCCESS",
	"result":{
        "block_hash":"63355f8e80...6c8108e4e56b264d2a",
        "block_height":112,
        "txs_root":"472af7d21a83156...75b4c0e0b1b4576531",
        "bookkeepers":"AL4CDqBikr...Qf2fg1AC&AL...g1AC",
        "consensus_data":"12156079575032856115",
        "block_size":532,
        "block_time":1522205080,
        "tx_count":12,
        "txs":[
        	{
        		"tx_hash":"000062c6fe4...9a1c33721",
        		"tx_type":209,
        		"tx_time":1522205080,
        		"confirm_flag":1
        	}
        ]

	}
```


| Url Field |     Type |   Description   |
| -------------- | --------| ------ |
| param |   String|  block height or block hash  |



| ResponseField     |     Type |   Description   |
| -------------- | --------| ------ |
|   block_hash|   String|   block hash |
|	block_height|   int|  block height |
|	txs_root|   String|  the merkleroot of all transactions in the block  |
|   bookkeepers|   String| keepers of this block,divided by `&` |
|	consensus_data	|	String|	consensus data  |
|	block_size|	int|   size of this block, unit:byte  |
|	block_time|	int|	unix time of this block|
|	tx_count|	int| the number of transactions in this block |
|	txs.tx_hash|	String|	transaction hash|
|	txs.tx_type|	int|	transaction type.208 or 209|
| txs.confirm_flag | int | transaction state in blockchain.1:succeed 0:failed |
|	txs.tx_time|	int|	unix time of the transaction|

### 1.4 Get generate block time

```java
url：/v2/blocks/generate-time?count=10,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":[
		{
			"block_height":1,
			"generate_time":6
		},
		{
			"block_height":2,
			"generate_time":1
		}
	]
}
```

| RequestField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| count |   int| amount of the latest blocks |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    block_height|   int| block height |
|    generate_time|   int|  time of generating block  |


## 2.Transaction APIs

#### Tx Type

| Value     |     Type |   Description   |
| -------------- | --------| ------ |
|    208|   int|  deploy smart contract |
|    209|   int|  invoke smart contract|


#### Description

| Value     |     Type |   Description   |
| -------------- | --------| ------ |
|    transfer|   String|  transfer  |
|    gasconsume|   String|  gas consume  |
|    ontId- |   String|  OntId |
|    claimRecord- |   String|  claim Record  |
|    auth |   String|  auth  |
|    {"NeedStorage":true,...} |   String|  if the transaction type is 208,the filed is the description of the contract  |


#### Event Type

| Value     |     Type |   Description   |
| -------------- | --------| ------ |
|    0|   int|  others  |
|    1|   int|  deploy contract  |
|    2 |   int| gas consume |
|    3 |   int|  transfer  |
|    4 |   int|  ONT ID  |
|    5 |   int|  claim record  |
|    6 |   int|  authorization  |




### 2.1 Get latest transaction list

```java
url: /v2/latest-transactions?count=10,
method: GET,
params: {
},
successResponse: {
    "code":0,
    "msg":"SUCCESS",
    "result":[
        {
            "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
            "tx_type":209,
            "tx_time":1522210288,
            "block_height":1212,
            "confirm_flag":1,
            "block_index":1,
            "fee":"0.01"
        }
    ]
}
```



| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| count |   int|  amount of latest transactions. 1<=count<=50  |



| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    tx_hash|   String| transaction hash   |
|    tx_type|   int| transaction type.208 or 209 |
|    tx_time|   int|  unix time of the transaction  |
|    block_height| int | block height |
|    confirm_flag|   int|  transaction state in blockchain. 0:failed 1:succeed  |
|    block_index|   int | the index of transaction in block  |
|    fee|   String | fee  |


### 2.2 Get transaction list by page

```java
url：/v2/transactions?page_size=1&page_number=10,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "records":[
            {
                "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
                "tx_type":209,
                "tx_time":1522210288,
                "block_height":1212,
                "confirm_flag":1,
                "block_index":1,
                "fee":"0.01"
            }
        ],
        "total":23449
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |


| ResponseField     |     Type |   Description   |
| -------------- | --------| ------ |
|   total|   int|   total transactions |


### 2.3 Get latest nonnotid transaction list

```java
url: /v2/latest-nonontid-transactions?count=10,
method: GET,
params: {
},
successResponse: {
    "code":0,
    "msg":"SUCCESS",
    "result":[
        {
            "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
            "tx_type":209,
            "tx_time":1522210288,
            "block_height":1212,
            "confirm_flag":1,
            "block_index":1,
            "fee":"0.01"
        }
    ]
}
```



| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| count |   int|  amount of latest nonontid transactions.1<=count<=50  |



| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    tx_hash|   String| transaction hash   |
|    tx_type|   int| transaction type. 209 |
|    tx_time|   int|  unix time of the transaction  |
|    block_height| int | block height |
|    confirm_flag|   int|  transaction state in blockchain. 0:failed 1:succeed  |
|    block_index|   int | the index of transaction in block  |
|    fee|   String | fee  |


### 2.4 Get nonontid transaction list by page

```java
url：/v2/nonontid-transactions?page_size=1&page_number=10,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "records":[
            {
                "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
                "tx_type":209,
                "tx_time":1522210288,
                "block_height":1212,
                "confirm_flag":1,
                "block_index":1,
                "fee":"0.01"
            }
        ],
        "total":23449
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |


| ResponseField     |     Type |   Description   |
| -------------- | --------| ------ |
|   total|   int|   total nonontid transactions |



### 2.5 Get transaction detail by txhash

```java
url：/v2/transactions/{tx_hash},
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "tx_hash":"000004c9903c338...ee5505e171e6d752dbd",
        "tx_type":209,
        "tx_time":1522210288,
        "block_height":1212,
        "confirm_flag":1,
        "block_index":1,
        "fee":"0.01",
        "description":"transfer",
        "event_type":3,
        "detail":{
        
        }
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| tx_hash |   String|  transaction hash  |



| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    tx_hash|   String| transaction hash   |
|    tx_type|   int| transaction type.208 or 209 |
|    tx_time|   int|  unix time of the transaction  |
|    block_height| int | block height |
|    confirm_flag|   int|  transaction state in blockchain. 0:failed 1:succeed  |
|    block_index|   int | the index of transaction in block  |
|    fee|   String | fee  |
|    description|   String | description.reference **Description** |
|    event_type|   int | event type.reference **Event Type** |
|    detail|   Object | transaction detail  |

**detail field:**

- Deploy smart contract transaction

  ```java
  {
  	"detail":{}
  }
  ```
  
- Transfer transaction

```java
{
	"detail":{
		"transfers": [
			{
				"amount": "0.020000000",
				"from_address":"Aege6VvWEiKauFa2ngrtwdXt8FeGkWNPRH",
				"to_address":"ATUD7W6t6tLPGgd8H9tCN6Kwkb9WKFddch",
				"asset_name":"ont",
				"description":"transfer"
			}
		]
	}
}
```


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    transfers.asset_name|   String| asset name |
|    transfers.to_address|   String| toaddres |
|    transfers.from_address|   String| fromaddress |
|    transfers.amount|   String| amount |
|    transfers.description|   String| "transfer".reference **Description** |


- ONT ID transaction

```json
{
	"detail":{
		"ontid":"did:ont:Ahctt129csbc612enxGTss6",
		"description":"register OntId"
	}
}
```


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    ontid|   String|  OntId|
|    description|   String| reference **ONT ID description** |



## 3.ONT ID APIs


#### ONT ID description

| Value     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    register OntId |   String|  register OntId |
|    add publicKey:xxxxx |   String|  add publicKey |
|    remove publicKey:xxxxx |   String|  remove publicKey |
|    add attribute:value1&value2 |   String| add attribute  |
|    update attribute:xxxx |   String|  update attribute |
|    remove attribute:xxxx |   String| remove attribute |
|    change recovery:xxxx |   String|  change recovery |
|    add recovery:xxxx |   String|  add recovery |
| create new claim: claimId:xxxxxx | String | create claim |

#### DDO Attribute

| Key     | Value     |     Type |   Description   |
| -------------- | --------|------ |-----|
|    Claim |    ContextDesc |   String|  description |
|    |    ClaimContext |   String|  claim context  |
|    |    IssuerOntId |   String| ONT ID of the issuer |
|    |    ClaimId |   String|   hash of the claim |
|   SelfDefined |    value |   String|  self defined DDO info |



### 3.1 Get latest ONT ID  list

```java
url：/v2/latest-ontids?count=10,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":[
        {
            "ontid":"did:ont:TA7aqop3BcYJpHtEEyfg1ucausfDETyTQA",
            "description":"register OntId",
            "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
            "tx_type":209,
            "tx_time":1522210288,
            "block_height":1212,
            "fee":"0.01"
        }
    ]
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| count |   int|  amount of latest ontids.1<=count<=50  |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    ontid |   String|  ONT ID |
|    tx_hash|   String|  transaction hash|
|    block_height |   int|  block height|
|    tx_time |   int|  unix time of the transaction|
|    description |   String|  description. reference **ONT ID description**|
|    tx_type |   int|  209  |
|    fee|   String|  fee  |


### 3.2 Get  ONT ID  list by page

```java
url：/v2/ontids?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
    	"records":[
            {
                "ontid":"did:ont:TA7aqop3BcYJpHtEEyfg1ucausfDETyTQA",
                "description":"register OntId",
                "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
                "tx_type":209,
                "tx_time":1522210288,
                "block_height":1212,
                "fee":"0.01"
            }
    	],
    	"total":100
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    total |   int|  total ONT ID |



### 3.3 Get ONT ID transaction list by page

```java
url：/v2/ontids/{ontid}/transactions?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
		"records":[
			{
				"tx_hash":"df272d8bf471ed...669fadc996f1b3f",
				"block_height":123,
				"tx_type": 209,
				"tx_time":1522213966,
				"description":"add attribute:claim",
				"fee":"0.01",
				"ontid": "did:ont:TA96Nqm9HRFKzudLjgH16Zfvdw3ixq8UGZ"
			}
		],
		"total":10
    }
}
```


| RequestField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    ontid|   String|  ONT ID  |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    txs.tx_hash|   String|  transaction hash |
|    txs.block_height|   int|   block height |
|    txs.tx_type|   int|  209  |
|    txs.fee| String|  fee  |
|    txs.ontid| String|  ONT ID  |
|    txs.event_type| int| event type  |
|    txs.tx_time| int|  unix time of the block  |
|    txs.description|   String|  description.reference **ONT ID description** |
|    tx_total| int| total transactions of the ONT ID |

### 3.3 Get ONT ID ddo

```java
url：/v2/ontids/{ontid}/ddo,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "Attributes":[
            {
                "Claim":{
                    "ClaimId":"111ab2f56d106da...8fa65a9996b03ba0",
                    "ClaimContext":"claim:github_authentication",
                    "ContextDesc":"my github claim",
                    "IssuerOntId":"did:ont:TKhyXw8o...sy4p6fYZPB"
                }
            }
        ],
        "OntId":"did:ont:TA7aqop3B...ausfDETyTQA",
        "Owners":[
            {
                "Type": "ECDSA",
                "Curve": "P-256",
                "Value": "120203cef1f2ff7...4031dcdf5c5772e449",
                "PublicKeyId": "did:ont:TA96Nq...vdw3ixq8UGZ#keys-1"
            }
        ]
    }
}
```


| RequestField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    ontid|   String|  ONT ID  |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| Attributes |   list|  |
| OntId |   String|  ONT ID |
| Owners.Type |   String| ECDSA |
| Owners.Curve |   String| P-256 |
| Owners.Value |   String|  publickey in HEX string|



## 4.Address APIS

#### Asset Type

|     value      |  Type  |            Description            |
| :------------: | :----: | :-------------------------------: |
|   oep4\|OEP4   | String |            oep4 asset             |
|   oep5\|OEP5   | String |            oep5 asset             |
|   oep8\|OEP8   | String |            oep8 asset             |
| native\|NATIVE | String | ont,ong,waitbound ong,unbound ong |

#### Native Asset

|     value     |  Type  |  Description  |
| :-----------: | :----: | :-----------: |
|      ont      | String |      ont      |
|      ong      | String |      ong      |
| waitbound_ong | String | waitbound ong |
|  unbound_ong  | String |  unbound ong  |

### 4.1 Get address balance

```java
url：/v2/addresses/{address}/{token_type}/balances,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":[
		{
			"balance": "138172.922008484",
			"asset_name": "ong",
			"asset_type":"native"
		},
		{
			"balance": "14006.83021186",
			"asset_name": "waitbound_ong",
			"asset_type":"native"
		},
		{
			"balance": "71472.14798338",
			"asset_name": "unbound_ong",
			"asset_type":"native"
		},
		{
			"balance": "8637767",
			"asset_name": "ont",
			"asset_type":"native"
		},
		{
			"asset_name": "pumpkin01",
			"balance": "7",
			"asset_type":"oep8"
		},
		{
			"asset_name": "TNT",
			"balance": "19888",
			"asset_type":"oep4"
		},
		{
			"asset_name": "HyperDragons:2",
			"balance": "3",
			"asset_type":"oep5"
		}
	]
}
```


| URL Field     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    address|   String|  address  |
| token_type | String | oep4\|OEP4\|oep5\|OEP5\|oep8\|OEP8\|native\|NATIVE |



| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    asset_name|   String| asset name |
|    balance|   String| balance  |
|    asset_type|   String| asset type：oep4,oep5,oep8,native |



### 4.2  Get transaction list by address

```java
url：/v2/addresses/{address}/transactions?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":[
			{
				"tx_hash":"09e599ecde6ee....55239e1b1bd291558e5a6ef3fa",
				"confirm_flag":1,
				"tx_type":208,
				"tx_time":1522207168,
				"block_height":11,
				"fee":"0.01",
				"block_index":1,
				"transfers": [
					{
                        "amount": "2.01",
                        "from_address":"Aege6VvWEiKauFa2ngrtwdXt8FeGkWNPRH",
                        "to_address":"ATUD7W6t6tLPGgd8H9tCN6Kwkb9WKFddch",
                        "asset_name":"ont"
					},
                    {
                        "amount": "0.01",
                        "from_address":"Aege6VvWEiKauFa2ngrtwdXt8FeGkWNPRH",
                        "to_address":"ATUD7W6t6tLPGgd8H9tCN6Kwkb9WKFddch",
                        "asset_name":"ong"
					}
				]
			}
		]
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| address |   String |  address  |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |



| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| tx_hash |   String| transaction hash  |
| confirm_flag |   int| transaction state in blockchain 1:succeed 0:failed  |
| block_height |   int|   block height |
| tx_type |   int|  208 or 209  |
| tx_time | int|  unix time of the transaction  |
| fee |   String|  fee  |
| block_index |   int| index in the block   |
| transfers.from_address |   String|  from_address  |
| transfers.to_address |   String|  to_address  |
| transfers.amount |   String|  amount  |
| 	 transfers.asset_name | String | asset name |




### 4.3  Get transaction list by address and asset name

```java
url：/v2/addresses/{address}/{asset_name}/transactions?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":[
			{
				"tx_hash":"09e599ecde6ee....55239e1b1bd291558e5a6ef3fa",
				"confirm_flag":1,
				"tx_type":208,
				"tx_time":1522207168,
				"block_height":11,
				"fee":"0.01",
				"block_index":1,
				"transfers": [
					{
                        "amount": "2.01",
                        "from_address":"Aege6VvWEiKauFa2ngrtwdXt8FeGkWNPRH",
                        "to_address":"ATUD7W6t6tLPGgd8H9tCN6Kwkb9WKFddch",
                        "asset_name":"ont"
					}
				]
			}
    	]
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| address |   String |  address  |
| asset_name |   String |  asset name  |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |



|     ResponseField      |  Type  |                    Description                     |
| :--------------------: | :----: | :------------------------------------------------: |
|        tx_hash         | String |                  transaction hash                  |
|      confirm_flag      |  int   | transaction state in blockchain 1:succeed 0:failed |
|      block_height      |  int   |                    block height                    |
|        tx_type         |  int   |                     208 or 209                     |
|        tx_time         |  int   |            unix time of the transaction            |
|          fee           | String |                        fee                         |
|      block_index       |  int   |                 index in the block                 |
| transfers.from_address | String |                    from_address                    |
|  transfers.to_address  | String |                     to_address                     |
|    transfers.amount    | String |                       amount                       |
|  transfers.asset_name  | String |                     asset name                     |



### 4.4  Get transaction list by address and time

```java
url：/v2/addresses/{address}/transactions?begin_time=1556017050&end_time=1556017250,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":[
			{
				"tx_hash":"09e599ecde6ee....55239e1b1bd291558e5a6ef3fa",
				"confirm_flag":1,
				"tx_type":208,
				"tx_time":1522207168,
				"block_height":11,
				"fee":"0.01",
				"block_index":1,
				"transfers": [
					{
                        "amount": "2.01",
                        "from_address":"Aege6VvWEiKauFa2ngrtwdXt8FeGkWNPRH",
                        "to_address":"ATUD7W6t6tLPGgd8H9tCN6Kwkb9WKFddch",
                        "asset_name":"ont"
					},
                    {
                        "amount": "0.01",
                        "from_address":"Aege6VvWEiKauFa2ngrtwdXt8FeGkWNPRH",
                        "to_address":"ATUD7W6t6tLPGgd8H9tCN6Kwkb9WKFddch",
                        "asset_name":"ong"
					}
				]
			}
    ]
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| address |   String |  address  |
| end_time | int |  unxi time  |
| begin_time |   int|  unix time.<br />The maximum time range is **one week**.  |



|     ResponseField      |  Type  |                    Description                     |
| :--------------------: | :----: | :------------------------------------------------: |
|        tx_hash         | String |                  transaction hash                  |
|      confirm_flag      |  int   | transaction state in blockchain 1:succeed 0:failed |
|      block_height      |  int   |                    block height                    |
|        tx_type         |  int   |                     208 or 209                     |
|        tx_time         |  int   |            unix time of the transaction            |
|          fee           | String |                        fee                         |
|      block_index       |  int   |                 index in the block                 |
| transfers.from_address | String |                    from_address                    |
|  transfers.to_address  | String |                     to_address                     |
|    transfers.amount    | String |                       amount                       |
|  transfers.asset_name  | String |                     asset name                     |



### 4.5  Get transaction list by address and asset name and time

```java
url：/v2/addresses/{address}/{asset_name}/transactions?begin_time=1556017050&end_time=1556017250,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":[
			{
				"tx_hash":"09e599ecde6ee....55239e1b1bd291558e5a6ef3fa",
				"confirm_flag":1,
				"tx_type":208,
				"tx_time":1522207168,
				"block_height":11,
				"fee":"0.01",
				"block_index":1,
				"transfers": [
					{
                        "amount": "2.01",
                        "from_address":"Aege6VvWEiKauFa2ngrtwdXt8FeGkWNPRH",
                        "to_address":"ATUD7W6t6tLPGgd8H9tCN6Kwkb9WKFddch",
                        "asset_name":"ont"
					}
				]
			}
    ]
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| address |   String |  address  |
| asset_name |   String |  asset name  |
| begin_time |   int|  unix time  |
| end_time |   int| unxi time<br />The maximum time range is **one week**. |



|     ResponseField      |  Type  |                    Description                     |
| :--------------------: | :----: | :------------------------------------------------: |
|        tx_hash         | String |                  transaction hash                  |
|      confirm_flag      |  int   | transaction state in blockchain 1:succeed 0:failed |
|      block_height      |  int   |                    block height                    |
|        tx_type         |  int   |                     208 or 209                     |
|        tx_time         |  int   |            unix time of the transaction            |
|          fee           | String |                        fee                         |
|      block_index       |  int   |                 index in the block                 |
| transfers.from_address | String |                    from_address                    |
|  transfers.to_address  | String |                     to_address                     |
|    transfers.amount    | String |                       amount                       |
|  transfers.asset_name  | String |                     asset name                     |



### 4.6  Get transaction list by address and asset name and time and page(for ONTO)

```java
url：/v2/addresses/{address}/{asset_name}/transactions?page_size=10&end_time=1556017250,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
		"records":[
			{
				"tx_hash":"09e599ecde6ee....55239e1b1bd291558e5a6ef3fa",
				"confirm_flag":1,
				"tx_type":208,
				"tx_time":1522207168,
				"block_height":11,
				"fee":"0.01",
				"block_index":1,
				"transfers": [
					{
                        "amount": "2.01",
                        "from_address":"Aege6VvWEiKauFa2ngrtwdXt8FeGkWNPRH",
                        "to_address":"ATUD7W6t6tLPGgd8H9tCN6Kwkb9WKFddch",
                        "asset_name":"ont"
					}
				]
			}
		]
    	"total":100
    }
}
```

| Url RequestField | Type   | Description |
| ---------------- | ------ | ----------- |
| address          | String | address     |
| asset_name       | String | asset name  |
| page_size       | int    | page size   |
| end_time         | int    | unxi time   |



|       ResponseField        |  Type  |                    Description                     |
| :------------------------: | :----: | :------------------------------------------------: |
|        txs.tx_hash         | String |                  transaction hash                  |
|      txs.confirm_flag      |  int   | transaction state in blockchain 1:succeed 0:failed |
|      txs.block_height      |  int   |                    block height                    |
|        txs.tx_type         |  int   |                     208 or 209                     |
|        txs.tx_time         |  int   |            unix time of the transaction            |
|          txs.fee           | String |                        fee                         |
|      txs.block_index       |  int   |                 index in the block                 |
| txs.transfers.from_address | String |                    from_address                    |
|  txs.transfers.to_address  | String |                     to_address                     |
|    txs.transfers.amount    | String |                       amount                       |
|  txs.transfers.asset_name  | String |                     asset name                     |
| txs.transfers.description  | String |                    description                     |
|  txs.transfers.event_type  |  int   |                     event type                     |





## 5.Contract APIs

### 5.1 Get contract lsit

```java
url：/v2/contracts?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "records":[
            {
                "contract_hash": "16edbe366d...99424c94aeef02",
                "name": "name",
                "logo":"",
                "description": "is a decentralized, tru.....",
                "creator": "AFmseVrdL9f9oyCzZefL9tG6UbvhPbdYzM",
                "create_time":1516946305,
                "update_time":1516948340,
                "contact_info":"{\"website\":\"www.test.cn\",\"github\":\"github.com\"}",
                "ont_sum": "2123.000000000",
                "ong_sum": "1233123123.000000000",
                "address_count": 122,
                "tx_count": 30,
                "token_sum":{\"Ht\":\"124\"}",
                "category":"oep",
                "type":"oep4"
            }
        ],
        "total":12
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| contract_hash |   String| contract hash |
| name|   String| contract name |
| create_time	|	int| create time |
| update_time|	int| update time |
| contact_info|	String| contact information.JSON format string |
| logo|	String| logo url |
| description|	String| contract description |
| creator|	String| creator address |
| ong_sum|	String| total ong |
| ont_sum|	String| total ont |
| address_count|	int| total address |
| tx_count|   int| total transaction |
| token_sum|   String| total token.JSON format string |
| category | String | category |
| type | String | oep4,oep5,oep8,others |
| total | int | total contract |




### 5.2 Get contract detail by contract_hash

```java
url：/v2/contracts/{contract_hash},
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "contract_hash": "16edbe366d...99424c94aeef02",
        "name": "name",
        "abi":"25a80bbc...5381",
        "code": "013ec56b6...006a5",
        "source_code":"",
        "create_time":1516946305,
        "update_time":1516948340,
        "contact_info":"{\"website\":\"www.test.cn\",\"github\":\"github.com\"}",
        "logo":"",
        "description": "LuckyNumber is a decentralized, tru.....",
        "creator": "AFmseVrdL9f9oyCzZefL9tG6UbvhPbdYzM",
        "ont_sum": "2123.000000000",
        "ong_sum": "1233123123.000000000",
        "address_count": 122,
        "tx_count": 30,
        "token_sum":{\"Ht\":\"124\"}",
        "category":"oep",
        "type":"oep5"
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| contract_hash | String |  contract hash  |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| contract_hash |   String| contract hash |
| name|   String| contract name |
| create_time	|	int| create time |
| update_time|	int| update time |
| contact_info|	String| contact information.JSON format string |
| logo|	String| logo url |
| description|	String| contract description |
| creator|	String| creator address |
| ong_sum|	String| total ong |
| ont_sum|	String| total ont |
| address_count|	int| total address |
| tx_count|   int| total transaction |
| token_sum|   String| total token.JSON format string |
| type | String | oep4,oep5,oep8,others |
| abi | String | contract abi |
| code | String | contract code |
| source_code | String | contract source code |
| category | String | category |



### 5.3 Get contract transaction list by contracthash

```java
url：/v2/contracts/{contract_type}/{contract_hash}/transactions?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
    	"txs":[
    		{
                "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
                "tx_type":209,
                "tx_time":1522210288,
                "block_height":1212,
                "confirm_flag":1,
                "block_index":1,
                "fee":"0.01"
    		}
    	],
    	"total":20
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |
| contract_type | String | oep4,oep5,oep8,others |
| contract_hash | String | contract_hash |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    txs.tx_hash|   String| transaction hash   |
|    txs.tx_type|   int| transaction type.208 or 209 |
|    txs.tx_time|   int|  unix time of the transaction  |
|    txs.block_height| int | block height |
|    txs.confirm_flag|   int|  transaction state in blockchain. 0:failed 1:succeed  |
|    txs.block_index|   int | the index of transaction in block  |
|    txs.fee|   String | fee  |
|    total|   int | total  |



#### 云斗龙Oep5合约

返回多两个字段：

- asset_name：资产名
- json_url：dragon logo和name的json字符串。如果asset_name没有对应的json描述，该字段不返回。

```java
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
    	"txs":[
    		{
                "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
                "tx_type":209,
                "tx_time":1522210288,
                "block_height":1212,
                "confirm_flag":1,
                "block_index":1,
                "fee":"0.01",
                "asset_name":"HyperDragons: 1360",
                "json_url":"{\"image\":\"https://hyd-go-res.alfakingdom.com/normal/1360.svg\",\"name\":\"dragon#1360\"}"   //如果asset_name没有找到对应的json描述，该字段不返回
    		}
    	],
    	"total":20
    }
}
```





### 5.4 Get dappstore contracts information 

```java
url：/v2/contracts/dappstore?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
    	"txs":[
    		{
                "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
                "tx_type":209,
                "tx_time":1522210288,
                "block_height":1212,
                "confirm_flag":1,
                "block_index":1,
                "fee":"0.01"
    		}
    	],
    	"total":20
    }
}
```

| Url RequestField | Type   | Description                                     |
| ---------------- | ------ | ----------------------------------------------- |
| page_size        | int    | amount of records in one page. 1<=page_size<=20 |
| page_number      | int    | number of the page. 1<=page_number              |
| contract_type    | String | oep4,oep5,oep8,others                           |
| contract_hash    | String | contract_hash                                   |

|  ResponseField   |  Type  |                     Description                     |
| :--------------: | :----: | :-------------------------------------------------: |
|   txs.tx_hash    | String |                  transaction hash                   |
|   txs.tx_type    |  int   |             transaction type.208 or 209             |
|   txs.tx_time    |  int   |            unix time of the transaction             |
| txs.block_height |  int   |                    block height                     |
| txs.confirm_flag |  int   | transaction state in blockchain. 0:failed 1:succeed |
| txs.block_index  |  int   |          the index of transaction in block          |
|     txs.fee      | String |                         fee                         |
|      total       |  int   |                        total                        |




### 5.5 Get contract transaction list by contracthash(no contract_type url param)

```java
url：/v2/contracts/{contract_hash}/transactions?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
    	"txs":[
    		{
                "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
                "tx_type":209,
                "tx_time":1522210288,
                "block_height":1212,
                "confirm_flag":1,
                "block_index":1,
                "fee":"0.01"
    		}
    	],
    	"total":20
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |
| contract_hash | String | contract_hash |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    txs.tx_hash|   String| transaction hash   |
|    txs.tx_type|   int| transaction type.208 or 209 |
|    txs.tx_time|   int|  unix time of the transaction  |
|    txs.block_height| int | block height |
|    txs.confirm_flag|   int|  transaction state in blockchain. 0:failed 1:succeed  |
|    txs.block_index|   int | the index of transaction in block  |
|    txs.fee|   String | fee  |
|    total|   int | total  |





## 6.Token APIs

### 6.1 Get token list by token type

```java
url：/v2/tokens/{token_type}?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "records":[
            {
                "contract_hash": "16edbe366d1337eb...4c94aeef02",
                "creator": "AUr5QUfeBADq6BMY6Tp5yuMsUNGpsD7nLZ",
                "description": "30",
                "logo": "",
                "create_time":1516946305,
                "update_time":1516948340,
                "contact_info":"{\"website\":\"www.test.cn\",\"github\":\"github.com\"}",
                "total_supply": 1000000000,
                "name": "name",
                "symbol": "MYT",
                "decimals": 8,
                "address_count": 1,
                "tx_count": 30
            }
        ],
        "total":12
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| token_type |   String| oep4,oep5,oep8 |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| contract_hash |   String| contract hash |
| name|   String| contract name |
| creator|	String| creator address |
| description|	String| contract description |
| logo|	String| logo url |
| create_time	|	int| create time |
| update_time|	int| update time |
| contact_info|	String| contact information.JSON format string |
| total_supply|	int| total supply of the token |
| symbol|	String| symbol of the token |
| decimals|	int| decimals of the token. If the token type is oep5,response not have this param |
| address_count|	int| total address |
| tx_count|   int| total transaction |
| total | int | total contract |

##### Oep8 token
if the param `token_type` == **oep8**, then the result is:

```java

successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "records":[
            {
                "contract_hash": "16edbe366d1337eb...4c94aeef02",
                "name": "name",
                "creator": "AUr5QUfeBADq6BMY6Tp5yuMsUNGpsD7nLZ",
                "description": "test contract",
                "logo": "",
                "create_time":1516946305,
                "update_time":1516948340,
                "contact_info":"{\"website\":\"www.tst.cn\",\"github\":\"github.com\"}",,
                "total_supply": {
                	"01":"1002",
                	"02":"899",
                	"03":"321"
                },
                "symbol": {
                	"01":"TNA",
                	"02":"TNB",
                	"03":"TNC"
                },
                "token_name":{
                	"01":"TokenNameFrist",
                	"02":"TokenNameSecond",
                	"03":"TokenNameThird"
                },
                "token_id":{
                	"01":"01",
                	"02":"02",
                	"03":"03"
                }
                "address_count": 1,
                "tx_count": 30
            }
        ],
        "total":12
    }
}

```


### 6.2 Get oep8 token transaction list by token name


```java
url：/v2/tokens/oep8/{contract_hash}/{token_name}/transactions?page_size=10&page_number=1,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
    	"records":[
    		{
                "tx_hash":"9762458cd30612509f7c...a010ccc7b347057eb5",
                "tx_type":209,
                "tx_time":1522210288,
                "block_height":1212,
                "confirm_flag":1,
                "block_index":1,
                "fee":"0.01",
    		}
    	],
    	"total":20
    }
}
```

| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| contract_hash |   String| oep8 token contract hash |
| token_name |   String| oep8 token name |
| page_size |   int|  amount of records in one page. 1<=page_size<=20  |
| page_number |   int| number of the page. 1<=page_number |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| records.tx_hash |   String| transaction hash   |
| records.tx_type |   int| transaction type.208 or 209 |
| records.tx_time |   int|  unix time of the transaction  |
| records.block_height | int | block height |
| records.confirm_flag |   int|  transaction state in blockchain. 0:failed 1:succeed  |
| records.block_index |   int | the index of transaction in block  |
| records.fee |   String | fee  |
|    total|   int | total  |



### 6.3 Get token detail by token type and contracthash

```java
url：/v2/tokens/{token_type}/{contract_hash},
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "contract_hash": "16edbe366d...99424c94aeef02",
        "name": "name",
        "abi":"25a80bbc...5381",
        "code": "013ec56b6...006a5",
        "source_code":"",
        "create_time":1516946305,
        "update_time":1516948340,
        "contact_info":"{\"website\":\"www.test.cn\",\"github\":\"github.com\"}",
        "logo":"",
        "description": "oep4 token",
        "creator": "AFmseVrdL9f9oyC....G6UbvhPbdYzM",
        "ont_sum": "2123.000000000",
        "ong_sum": "1233123123.000000000",
        "address_count": 122,
        "tx_count": 30,
        "token_sum":{\"Ht\":\"124\"}",
        "category":"oep",
        "type":"oep4",
        "total_supply": 1000000000,
        "symbol": "MYT",
        "decimals": 8
    }
}
```


| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| token_type |   String| oep4,oep5,oep8 |
| contract_hash |   String|  contract_hash  |


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| contract_hash |   String| contract hash |
| name|   String| contract name |
| create_time	|	int| create time |
| update_time|	int| update time |
| contact_info|	String| contact information.JSON format string |
| logo|	String| logo url |
| description|	String| contract description |
| creator|	String| creator address |
| ong_sum|	String| total ong |
| ont_sum|	String| total ont |
| address_count|	int| total address |
| tx_count|   int| total transaction |
| token_sum|   String| total token.JSON format string |
| type | String | oep4,oep5,oep8,others |
| abi | String | contract abi |
| code | String | contract code |
| source_code | String | contract source code |
| category | String | category |
| total_supply|	int| total supply of the token |
| symbol|	String| symbol of the token |
| decimals|	int| decimals of the token. If the token type is oep5,response not have this param |



##### Oep8 token
if the param `token_type` == **oep8**, then the result is:

```java

successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
        "contract_hash": "16edbe366d...99424c94aeef02",
        "name": "name",
        "abi":"25a80bbc...5381",
        "code": "013ec56b6...006a5",
        "source_code":"",
        "create_time":1516946305,
        "update_time":1516948340,
        "contact_info":"{\"website\":\"www.test.cn\",\"github\":\"github.com\"}",
        "logo":"",
        "description": "LuckyNumber is a decentralized, tru.....",
        "creator": "AFmseVrdL9f9oyCzZefL9tG6UbvhPbdYzM",
        "ont_sum": "2123.000000000",
        "ong_sum": "1233123123.000000000",
        "address_count": 122,
        "tx_count": 30,
        "token_sum":{\"Ht\":\"124\"}",
        "category":"oep",
        "type":"oep8",
        "total_supply": {
            "01":"1002",
            "02":"899",
            "03":"321"
        },
        "symbol": {
            "01":"TNA",
            "02":"TNB",
            "03":"TNC"
        },
        "token_name":{
            "01":"TokenNameFrist",
            "02":"TokenNameSecond",
            "03":"TokenNameThird"
        },
        "token_id":{
            "01":"01",
            "02":"02",
            "03":"03"
        }
    }
}

```


## 7.Summary APIs

### 7.1 Get blockchain latest summary information

```java
url：/v2/summary/blockchain/latest-info,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
		"block_height":12323,
		"tx_count":52000,
		"ontid_count":12,
		"node_count":188,
        "address_count":122,
        "ontid_tx_count": 24188
    }
}
```


| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    block_height|   int| current latest block height |
|    tx_count|   int|  current latest transaction count  |
|    ontid_count| int | current latest ONT ID count |
|    node_count|   int|  current latest node count  |
| address_count | int | current address count |
| ontid_tx_count | int | current latest ontid transaction count |



### 7.2 Get blockchain tps information

```java
url：/v2/summary/blockchain/tps,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
	    "current_tps": 10.02,
		"max_tps": 10000
	}
}
```

| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
|    current_tps|   double| current tps |
|    max_tps|  double |  max tps  |



### 7.3 Get blockchain daily summary information

```java
url：/v2/summary/blockchain/daily?start_time=1556027861&end_time=1556087861,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
    	"total": 3,
        "records":[
              {
                  "time": 1543622400,
                  "tx_count": 124,
                  "block_count": 120,
                  "active_address_count": 21,
                  "new_address_count": 12,
                  "ong_sum": "1204.003",
                  "ont_sum": "342451",
                  "active_ontid_count": 32,
                  "new_ontid_count": 29,
                  "ontid_total": 293,
                  "address_total": 390
              }
           ]
    }
}
```

| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| type |   String| daily or weekly or monthly  |
| start_time |   int| start time |
| end_time | int |end time |



| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| total|   int| total records   |
| records.time| int |	unix timestamp |
| records.tx_count|   int|  transaction count |
| records.block_count|   int| block count   |
| records.active_address_count |	int| active address count |
| records.new_address_count|   int|  new address count  |
| records.ong_sum|   String|  ong sum  |
| records.ont_sum|   String|  ont sum  |
| records.active_ontid_count|   int|  active ontid count  |
| records.new_ontid_count|   int|  new ontid count  |
| records.ontid_total|   int|  total ONT ID volume as of today   |
| records.address_total|   int|  total address volume as of today |



### 7.4 Get contract daily summary information

```java
url：/v2/summary/contracts/{contract_hash}/daily?start_time=1556027861&end_time=1556087861,
method：GET,
successResponse：{
    "code":0,
    "msg":"SUCCESS",
    "result":{
    	"total": 3,
        "records":[
              {
                  "time": 1543622400,
                  "tx_count": 0,
                  "active_address_count": 0,
                  "new_address_count": 0,
                  "ont_sum": "1244",
                  "ong_sum": "324123.00345003"
              }
           ]
    }
}
```

| Url RequestField |     Type |   Description   |
| -------------- | --------| ------ |
| contract_hash |   String| contract hash  |
| start_time |   int| start time |
| end_time | int |end time |



| ResponseField     |     Type |   Description   |
| :--------------: | :--------:| :------: |
| total|   int| total records   |
| records.time| int |	unix timestamp |
| records.tx_count|   int|  transaction count |
| records.active_address_count |	int| active address count |
| records.new_address_count|   int|  new address count  |
| records.ong_sum|   String|  ong sum  |
| records.ont_sum|   String|  ont sum  |

