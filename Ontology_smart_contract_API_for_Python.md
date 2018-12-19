<h1 align="center">Ontology Smart Contract API for Python</h1>
<p align="center" class="version">Version 0.1</p>

## Content

## Introduction

## Ontology API

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|           ontology.interop.Ontology.Attribute |                  GetUsage |                                   transaction_attr | get transaction attribute usage |
|           ontology.interop.Ontology.Attribute |                   GetData |                                   transaction_attr | get transaction attribute data |
|            ontology.interop.Ontology.Contract |                 GetScript |                                           contract | get contract script hash |
|            ontology.interop.Ontology.Contract |                    Create | script, parameter_list, return_type, properties, name, version, author, email, description | create a contract |
|            ontology.interop.Ontology.Contract |                   Migrate | script, parameter_list, return_type, properties, name, version, author, email, description | migrate  contract |
|              ontology.interop.Ontology.Header |                GetVersion |                                             header | get the version of header |
|              ontology.interop.Ontology.Header |             GetMerkleRoot |                                             header | get the merkle root of the transactions contained in the block |
|              ontology.interop.Ontology.Header |          GetConsensusData |                                             header | get the address of the consensus |
|              ontology.interop.Ontology.Header |          GetNextConsensus |                                             header | get the address where the next consensus will occur |
|              ontology.interop.Ontology.Native |                    Invoke |                   param,method,contractAddress,ver | nvoke native contract |
|             ontology.interop.Ontology.Runtime |           Base58ToAddress |                                                arg | transfer base58 address to byte array |
|             ontology.interop.Ontology.Runtime |           AddressToBase58 |                                                arg | byte array address to base58 |
|             ontology.interop.Ontology.Runtime | GetCurrentBlockHash |                                                    | get current block hash |
|         ontology.interop.Ontology.Transaction |                   GetType |                                        transaction | get transaction type |
|         ontology.interop.Ontology.Transaction |             GetAttributes |                                        transaction | get transaction attributes |

## System API

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|                ontology.interop.System.Action |            RegisterAction |                                  event_name, *args | register a notirfy event |
|                   ontology.interop.System.App |           RegisterAppCall |                         smart_contract_hash, *args | call other smart contract |

### Blockchain

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|            ontology.interop.System.Blockchain |                 GetHeight |                                                    | get height of block chain |
|            ontology.interop.System.Blockchain |                 GetHeader |                                     height_or_hash | get header by height or hash |
|            ontology.interop.System.Blockchain |                  GetBlock |                                     height_or_hash | get block by height or hash |
|            ontology.interop.System.Blockchain | GetTransactionByHash |                                               hash | get transaction by hash |
|            ontology.interop.System.Blockchain |               GetContract |                                        script_hash | get contract by script hash |
| ontology.interop.System.Blockchain | GetTransactionHeight | heigh of transaction |  |

### Block

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|                 ontology.interop.System.Block |       GetTransactionCount |                                              block | get transaction count of block |
|                 ontology.interop.System.Block |           GetTransactions |                                              block | get transactions of block |
|                 ontology.interop.System.Block | GetTransactionByIndex |                                       block, index | get the transaction by index |

### Contract

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|              ontology.interop.System.Contract |         GetStorageContext |                                           contract | get contract storage context |
|              ontology.interop.System.Contract |                   Destroy |                                                    | destroy current contract(self) |

### ExecutionEngine

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|       ontology.interop.System.ExecutionEngine |        GetScriptContainer |                                                    | get the current script container of a smart contract execution |
|       ontology.interop.System.ExecutionEngine |    GetExecutingScriptHash |                                                    | get the hash of the script ( smart contract ) which is currently being executed |
|       ontology.interop.System.ExecutionEngine |      GetCallingScriptHash |                                                    | get the hash of the script ( smart contract ) which began execution of the current script. |
|       ontology.interop.System.ExecutionEngine |        GetEntryScriptHash |                                                    | get the hash of the script ( smart contract ) which began execution of the smart contract. |

### Header

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|                ontology.interop.System.Header |                  GetIndex |                                             header | get the height/index of header |
|                ontology.interop.System.Header |       GetBlockHash |                                             header | get the hash of header |
|                ontology.interop.System.Header |               GetPrevHash |                                             header | get the hash of the previous header in the blockchain        |
|                ontology.interop.System.Header |              GetTimestamp |                                             header | get the timestamp of when the header was created |

### Runtime

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|               ontology.interop.System.Runtime |                GetTrigger |                                                    | get trigger |
|               ontology.interop.System.Runtime |              CheckWitness |                                     hash_or_pubkey | check the witness of address |
|               ontology.interop.System.Runtime |                       Log |                                            message | print log on node |
|               ontology.interop.System.Runtime |                    Notify |                                                arg | add notify to event |
|               ontology.interop.System.Runtime |                   GetTime |                                                    | get timestamp of most recent block |
|               ontology.interop.System.Runtime |                 Serialize |                                               item | serialize item to byte array |
|               ontology.interop.System.Runtime |               Deserialize |                                               item | deserialize byte array to item |

### Storage

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|        ontology.interop.System.StorageContext |                AsReadOnly |                                                    | Convert Storage Context to ReadOnly |
|               ontology.interop.System.Storage |                GetContext |                                                    | get the storage context |
|               ontology.interop.System.Storage |        GetReadOnlyContext |                                                    | get the readOnly Storage Context |
|               ontology.interop.System.Storage |                       Get |                                       context, key | get the storage by key |
|               ontology.interop.System.Storage |                       Put |                                context, key, value | put the key-value storage |
|               ontology.interop.System.Storage |                    Delete |                                       context, key | delete storage by key |

### Transaction

| Package | Name | Parameter |      |
| ---- | ---- | ---- | ---- |
|           ontology.interop.System.Transaction | GetTransactionHash |                                        transaction | Get the Transaction of hash |



