<h1 align="center">API Design of Ontology Official Website</h1>
<p align="center" class="version">Version 0.1</p>

Version | Author | Reviewer | Time
------| ----- |------|------|
0.1 | 赵越 | 周强 | 2019/6/24

## 1. Basic APIs

### 1.1 
```java
url: /api/api-query-data
method: POST
```

| Url RequestField | Type |
| -------------- | --------| 
|type | String|
| language | String |

| ResponseField| Type |  
| -------------- | --------| 
| id         | mediumint(8) unsigned | 
| type       | varchar(255)          | 
| language   | varchar(255)          | 
| message    | longtext              | 
| ctime      | bigint(20)            | 
| created_at | timestamp             | 
| updated_at | timestamp             | 


### 1.2
```java
url: /api/api-upload-img
method: POST
```

| Url RequestField | Type |
| -------------- | --------| 
|file  | MultipartFile|


### 1.3
```java
url: /api/api-upload-file
method: POST
```
| Url RequestField | Type |
| -------------- | --------| 
|file  | MultipartFile|

### 1.4
```java
url: /api/api-upload-code
method: POST
```
| Url RequestField | Type |
| -------------- | --------| 
|file  | MultipartFile|

### 1.5
```java
url: /api/api-save-data
method: POST
```

| Url RequestField | Type |
| -------------- | --------| 
|type |String |
|language|  String |
|message|  String|


### 1.6
```java
url: /api/api-save-mail
method: POST
```

| Url RequestField | Type |
| -------------- | --------| 
|nunito_sans_regular |String |
|first_name |String |
|last_name |String |
|company |String |
|job_title| String |
|email |String|
|your_message |String|

### 1.7
```java
url: /api/api-save-dapp
method: POST
```
| Url RequestField | Type |
| -------------- | --------| 
|dapp_name |String |
|tagline| String |
|referral_person |String|
|description| String |
|category |String |
|email |String|
|website |String|
|logo |String |
|dapp_snapshot |String |
|snap1 |String |
|snap2 |String |
|snap3 |String |
|snap4 |String |
|snap5 |String |
|snap6 |String |
|dapp_client_type| String|
|ont_id |String |
|ont_address |String |
|contract_address |String |
|contracr_abi |String |
|contracr_bytecode |String |
|github_address |String |
|online_date| String |
|twitter |String |
|facebook |String |
|telegram |String |
|reddit |String |
|is_opensouce| Integer|
|report_file| String|


### 1.8
```java
url: /api/api-app-list
method: POST
```
| Url RequestField | Type |
| -------------- | --------| 
|status| long |
|page| int |
|page_size|String|

| ResponseField| Type | 
| -------------- | --------| 
|logo | String|
|dapp_snapshot | String|
|snap1 | String|
|snap2 | String|
|snap3 | String|
|snap4 | String|
|snap5 | String|
|snap6 | String|
|agreement | String|
|is_opensouce| String|
|report_file | String|
|agreement|String|

### 1.9
```java
url: /api/api-app-detail
method: POST
```

| Url RequestField | Type |
| -------------- | --------| 
|id| int |

| ResponseField| Type | 
| -------------- | --------| 
|logo | String|
|dapp_snapshot | String|
|snap1 | String|
|snap2 | String|
|snap3 | String|
|snap4 | String|
|snap5 | String|
|snap6 | String|
|agreement | String|
|is_opensouce| String|
|report_file | String|
|agreement|String|

### 1.10
```java
url: /api/api-banner-list
method: POST
```

| Url RequestField | Type |
| -------------- | --------| 
|status| long |
|page| int |
|page_size|String|

| ResponseField| Type | 
| -------------- | --------| 
| id         | mediumint(8) unsigned | 
| name       | varchar(255)          | 
| pic_url    | varchar(255)          | 
| link       | varchar(255)          | 
| type       | varchar(255)          | 
| status     | varchar(255)          | 
| created_at | timestamp             | 
| updated_at | timestamp             | 

### 1.11 
```java
url: /api/api-banner-detail
method: POST
```
| Url RequestField | Type |
| -------------- | --------| 
|id| int |


| ResponseField| Type | 
| -------------- | --------| 
| id         | mediumint(8) unsigned | 
| name       | varchar(255)          | 
| pic_url    | varchar(255)          | 
| link       | varchar(255)          | 
| type       | varchar(255)          | 
| status     | varchar(255)          | 
| created_at | timestamp             | 
| updated_at | timestamp             | 


## 2. Help APIs

### 2.1 获取全部帮助列表

```java
url: /api/v1/helps/all
method: GET
```

| ResponseField| Type | 
| -------------- | --------| 
| id         | int(10) unsigned | 
| title      | varchar(255)     |        
| content    | longtext         | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp         |
| updated_at | timestamp       |

### 2.2 获取中文帮助列表

```java
url: /api/v1/helps/list/cn
method: GET
```

| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| title      | varchar(255)     |        
| content    | longtext         | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp         |
| updated_at | timestamp       |

### 2.3 获取英文帮助列表

```java
url: /api/v1/helps/list/en
method: GET
```

| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| title      | varchar(255)     |        
| content    | longtext         | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp         |
| updated_at | timestamp       |

### 2.4 获取指定帮助列表

```java
url: /api/v1/helps/{id}
method: GET
```

| Url RequestField | Type|
| -------------- | --------| 
|id| int|


| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| title      | varchar(255)     |        
| content    | longtext         | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp         |
| updated_at | timestamp       |


## 3. Marketing APIs

### 3.1 获取所有市场文章

```java
url: /api/v1/marketing/all
method: GET
```

| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| title      | varchar(255)     |         
| content    | longtext         | 
| language   | varchar(255)   |
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        |        


### 3.2 获取特定类型市场文章

```java
url: /api/v1/marketing/list/{type}
method: GET
```

| Url RequestField | Type |
| -------------- | --------| 
|type| string |


| ResponseField| Type |  
| -------------- | --------| 
| id         | int(10) unsigned | 
| title      | varchar(255)     |         
| content    | longtext         | 
| language   | varchar(255)   |
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        |   


### 3.3 获取特定市场文章

```java
url: /api/v1/marketing/{id}
method: GET
```


| Url RequestField | Type|
| -------------- | --------| 
|id| int|


| ResponseField| Type | 
| -------------- | --------| 
| id         | int(10) unsigned | 
| title      | varchar(255)     |         
| content    | longtext         | 
| language   | varchar(255)   |
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        |   


## 4. Bounty APIs 

### 4.1 获取所有激励项目信息
```java
url: /api/v1/bounty/all
method: GET
```

| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| type       | varchar(255)    |
| name       | varchar(255)     |
| img_url    | text             | 
| summary    | text             | 
| content    | longtext         | 
| bonus      | varchar(255)     | 
| leader     | varchar(255)     | 
| status     | varchar(255)     |
| created_at | timestamp        | 
| updated_at | timestamp        | 


### 4.2 获取指定激励项目信息

```java
url: /api/v1/bounty/{id}
method: GET
```


| Url RequestField | Type | 
| -------------- | --------| 
|id| int|

| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| type       | varchar(255)    |
| name       | varchar(255)     |
| img_url    | text             | 
| summary    | text             | 
| content    | longtext         | 
| bonus      | varchar(255)     | 
| leader     | varchar(255)     | 
| status     | varchar(255)     |
| created_at | timestamp        | 
| updated_at | timestamp        | 


### 4.3 获取指定类型的激励项目信息

#### 获取正在进行中的激励项目信息
```java
url: /api/v1/bounty-claim/list/in-progress
method: GET
```

| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| type       | varchar(255)    |
| name       | varchar(255)     |
| img_url    | text             | 
| summary    | text             | 
| content    | longtext         | 
| bonus      | varchar(255)     | 
| leader     | varchar(255)     | 
| status     | varchar(255)     |
| created_at | timestamp        | 
| updated_at | timestamp        | 


#### 获取已完成的激励项目信息

```java
url: /api/v1/bounty-claim/list/done
method: GET
```

| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| type       | varchar(255)    |
| name       | varchar(255)     |
| img_url    | text             | 
| summary    | text             | 
| content    | longtext         | 
| bonus      | varchar(255)     | 
| leader     | varchar(255)     | 
| status     | varchar(255)     |
| created_at | timestamp        | 
| updated_at | timestamp        | 



### 4.4 提交新的激励项目

```java
url: /api/v1/bounty-claim/new
method: POST
```


| Url RequestField | Type | 
| -------------- | --------| 
|bounty_id | Integer|
|name| String|
|email |String|
|github_url |String|
|completion_time| String |
|team |String|
|plan|String|


| ResponseField| Type |  
| -------------- | --------| 
| id         | int(10) unsigned | 
| type       | varchar(255)    |
| name       | varchar(255)     |
| img_url    | text             | 
| summary    | text             | 
| content    | longtext         | 
| bonus      | varchar(255)     | 
| leader     | varchar(255)     | 
| status     | varchar(255)     |
| created_at | timestamp        | 
| updated_at | timestamp        | 

### 4.5 提交要求或建议

```java
url: /api/v1/request-or-idea/new
method: POST
```


| Url RequestField | Type |
| -------------- | --------| 
|name |String |
|email |String |
|content| String|

| ResponseField| Type |  
| -------------- | --------| 
| id         | int(10) unsigned | 
| name       | varchar(255)   | 
| email      | varchar(255)   | 
| content    | text  | 
| status     | varchar(255)  | 
| created_at | timestamp   | 
| updated_at | timestamp  | 

### 4.6 提交激励项目建议

```java
url: /api/v1/bounty-idea/new
method: POST
```

| Url RequestField | Type | 
| -------------- | --------| 
|name |String |
|email |String |
|programming_lang |String |
|budget_requested |String |
|completion_time| String| 
|summary| String|
|content| String|

| ResponseField| Type |   
| -------------- | --------| 
| id               | int(10) unsigned |      
| name             | varchar(255)     |
| email            | varchar(255)     | 
| programming_lang | varchar(255)     | 
| budget_requested | varchar(255)     | 
| completion_time  | varchar(255)     | 
| summary          | text             | 
| content          | text             | 
| status           | varchar(255)     | 
| created_at       | timestamp        | 
| updated_at       | timestamp        | 


## 5. 提交测试网token申请

```java
url: /api/v1/test-net-token/new
method: POST
```


| Url RequestField | Type | 
| -------------- | --------| 
|name |String |
|phone |String |
|email |String |
|ont |String |
|ong |String |
|address| String |
|project_url| String |
|plan |String |
|team |String|

| ResponseField| Type |   
| -------------- | --------| 
| id          | int(10) unsigned | 
| name        | varchar(255)     | 
| phone       | varchar(255)     | 
| email       | varchar(255)     | 
| ont         | varchar(255)     | 
| ong         | varchar(255)     | 
| address     | varchar(255)     | 
| project_url | varchar(255)     | 
| plan        | varchar(255)     | 
| team        | varchar(255)     | 
| status      | varchar(255)     | 
| created_at  | timestamp        | 
| updated_at  | timestamp        | 


## 6. 网站图片与照片

### 6.1 获取所有网站文字

```java
url: /api/v1/site-text/all
method: GET
```

| ResponseField| Type | 
| -------------- | --------| 
| id         | int(10) unsigned | 
| nickname   | varchar(255)     | 
| key        | varchar(255)     | 
| value      | text             | 
| language   | varchar(255)  | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        | 

### 6.2 获得指定类型的中文信息

```java
url: /api/v1/site-text/list/cn/{type}
method: GET
```

| Url RequestField | Type | Description |
| -------------- | --------| ------ |
|Type|String| type类型： bounty / official / news / wallet / others|

| ResponseField| Type |  
| -------------- | --------| 
| id         | int(10) unsigned | 
| nickname   | varchar(255)     | 
| key        | varchar(255)     | 
| value      | text             | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        | 


### 6.3 获得指定类型的英文信息

```java
url: /api/v1/site-text/list/en/{type}
method: GET
```

| Url RequestField | Type | Description |
| -------------- | --------| ------ |
|Type|String| type类型： bounty / official / news / wallet / others|

| ResponseField| Type |  
| -------------- | --------| 
| id         | int(10) unsigned | 
| nickname   | varchar(255)     | 
| key        | varchar(255)     | 
| value      | text             | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        | 


### 6.4 获得指定站点信息

```java
url: /api/v1/site-text/{id}
method: GET
```

| Url RequestField | Type |
| -------------- | --------| 
|id| int|


| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| nickname   | varchar(255)     | 
| key        | varchar(255)     | 
| value      | text             | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        | 


### 6.5 获取所有网站图片

```java
url: /api/v1/site-img/all
method: GET
```

| ResponseField| Type |  
| -------------- | --------| 
| id         | int(10) unsigned | 
| key        | varchar(255)     | 
| img_url    | text             | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        | 

### 6.6 获得指定类型的中文图片

```java
url: /api/v1/site-img/list/cn/{type}
method: GET
```

| Url RequestField | Type | Description |
| -------------- | --------| ------ |
|Type|String|type类型： bounty / official / news / wallet / others|


| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| key        | varchar(255)     | 
| img_url    | text             | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        | 

### 6.7 获得指定类型的英文图片

```java
url: /api/v1/site-img/list/en/{type}
method: GET
```

| Url RequestField | Type | Description |
| -------------- | --------| ------ |
|Type|String|type类型： bounty / official / news / wallet / others|

| ResponseField| Type |   
| -------------- | --------| 
| id         | int(10) unsigned | 
| key        | varchar(255)     | 
| img_url    | text             | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        | 

### 6.8 获得指定站点图片

```java
url: /api/v1/site-img/{id}
method: GET
```

| Url RequestField | Type |
| -------------- | --------| 
|id|int|

| ResponseField| Type |   
| -------------- | --------|
| id         | int(10) unsigned | 
| key        | varchar(255)     | 
| img_url    | text             | 
| language   | varchar(255)     | 
| type       | varchar(255)     | 
| status     | varchar(255)     | 
| created_at | timestamp        | 
| updated_at | timestamp        | 

## 7. Dapp信息接口

### 7.1 获取全部dapp列表

```java
url: /api/v1/dapp-info/all
method: GET
```

| ResponseField| Type |  
| -------------- | --------| 
| id               | int(10) unsigned | 
| title            | varchar(255)     | 
| url              | varchar(255)     | 
| img_url          | varchar(255)     | 
| summary          | varchar(255)     | 
| content          | longtext         | 
| ont_id           | varchar(255)     | 
| dapp_screen_urls | longtext         | 
| telegram         | varchar(255)     | 
| twitter          | varchar(255)     | 
| discord          | varchar(255)     | 
| qq               | varchar(255)     | 
| github_url       | varchar(255)     | 
| contract_hash    | varchar(255)     | 
| abi              | varchar(255)     | 
| byte_code        | varchar(255)     | 
| token_name       | varchar(255)     | 
| token_type       | varchar(255)     | 
| donate_address   | varchar(255)     | 
| type             | varchar(255)     | 
| schedule         | varchar(255)     | 
| priority         | int(11)          | 
| status           | varchar(255)     | 
| created_at       | timestamp        | 
| updated_at       | timestamp        | 


### 7.2 获取指定dapp列表信息

```java
url: /api/v1/dapp-info/list?type=wallet
method: GET
```

| Url RequestField | Type | Description |
| -------------- | --------| ------ |
|Type |String| Type类型: wallet / dapp / official / game  / other |
|Schedule| String| Schedule类型: coming-soon / online / other|


| ResponseField| Type |   
| -------------- | --------| 
| id               | int(10) unsigned | 
| title            | varchar(255)     | 
| url              | varchar(255)     | 
| img_url          | varchar(255)     | 
| summary          | varchar(255)     | 
| content          | longtext         | 
| ont_id           | varchar(255)     | 
| dapp_screen_urls | longtext         | 
| telegram         | varchar(255)     | 
| twitter          | varchar(255)     | 
| discord          | varchar(255)     | 
| qq               | varchar(255)     | 
| github_url       | varchar(255)     | 
| contract_hash    | varchar(255)     | 
| abi              | varchar(255)     | 
| byte_code        | varchar(255)     | 
| token_name       | varchar(255)     | 
| token_type       | varchar(255)     | 
| donate_address   | varchar(255)     | 
| type             | varchar(255)     | 
| schedule         | varchar(255)     | 
| priority         | int(11)          | 
| status           | varchar(255)     | 
| created_at       | timestamp        | 
| updated_at       | timestamp        | 


### 7.3 获得指定的Dapp内容

```java
url: /api/v1/dapp-info/{id}
method: GET
```

| Url RequestField | Type | 
| -------------- | --------| 
|id| int|

| ResponseField| Type |   
| -------------- | --------| 
| id               | int(10) unsigned | 
| title            | varchar(255)     | 
| url              | varchar(255)     | 
| img_url          | varchar(255)     | 
| summary          | varchar(255)     | 
| content          | longtext         | 
| ont_id           | varchar(255)     | 
| dapp_screen_urls | longtext         | 
| telegram         | varchar(255)     | 
| twitter          | varchar(255)     | 
| discord          | varchar(255)     | 
| qq               | varchar(255)     | 
| github_url       | varchar(255)     | 
| contract_hash    | varchar(255)     | 
| abi              | varchar(255)     | 
| byte_code        | varchar(255)     | 
| token_name       | varchar(255)     | 
| token_type       | varchar(255)     | 
| donate_address   | varchar(255)     | 
| type             | varchar(255)     | 
| schedule         | varchar(255)     | 
| priority         | int(11)          | 
| status           | varchar(255)     | 
| created_at       | timestamp        | 
| updated_at       | timestamp        | 

### 7.4 提交新Dapp信息 

```java
url: /api/v1/dapp-info/new
method: POST
```

| Url RequestField | Type |
| -------------- | --------| 
|title |String |
|url |String |
|img_url |String |
|summary |String |
|content |String| 
|ont_id |String |
|dapp_screen_urls |String |
|telegram |String |
|twitter |String |
|discord |String |
|qq |String |
|github_url |String |
|contract_hash |String |
|abi |String|
|byte_code |String |
|token_name |String |
|token_type |String |
|donate_address |String |
|type |String |
|schedule| String|

| ResponseField| Type |   
| -------------- | --------| 
| id               | int(10) unsigned | 
| title            | varchar(255)     | 
| url              | varchar(255)     | 
| img_url          | varchar(255)     | 
| summary          | varchar(255)     | 
| content          | longtext         | 
| ont_id           | varchar(255)     | 
| dapp_screen_urls | longtext         | 
| telegram         | varchar(255)     | 
| twitter          | varchar(255)     | 
| discord          | varchar(255)     | 
| qq               | varchar(255)     | 
| github_url       | varchar(255)     | 
| contract_hash    | varchar(255)     | 
| abi              | varchar(255)     | 
| byte_code        | varchar(255)     | 
| token_name       | varchar(255)     | 
| token_type       | varchar(255)     | 
| donate_address   | varchar(255)     | 
| type             | varchar(255)     | 
| schedule         | varchar(255)     | 
| priority         | int(11)          | 
| status           | varchar(255)     | 
| created_at       | timestamp        | 
| updated_at       | timestamp        | 


### 7.5 上传Dapp图片

```java
url: /api/v1/dapp-info/upload
method: POST
```

| Url RequestField | Type |
| -------------- | --------| 
|img| MultipartFile|


## 8. Custodian接口 

### 8.1 提交custodian合作信息
```java
url: /api/v1/custodian-collaboration/new
method: POST
```

| Url RequestField | Type | 
| -------------- | --------| 
|name |String|
|company |String |
|email | String |
|phone |String |
|message| String|

| ResponseField| Type |   
| -------------- | --------| 
| id                | int(10) unsigned | 
| name              | varchar(255)     | 
| company           | varchar(255)     | 
| email             | varchar(255)     | 
| phone             | varchar(255)     | 
| message           | varchar(255)     | 
| status            | varchar(255)     | 
| processing_info   | varchar(255)     | 
| processing_person | varchar(255)     | 
| created_at        | timestamp        | 
| updated_at        | timestamp        | 

### 8.2 提交custodian求职信息

```java
url: /api/v1/custodian-job/new
method: POST
```

| Url RequestField | Type | 
| -------------- | --------| 
|name |String |
|email |String |
|phone |String |
|message |String|
|linkedin_url|  String|

| ResponseField| Type |   
| -------------- | --------| 
| id                | int(10) unsigned | 
| name              | varchar(255)     | 
| email             | varchar(255)     | 
| phone             | varchar(255)     | 
| message           | varchar(255)     | 
| linkedin_url      | varchar(255)     | 
| resume_url        | varchar(255)     | 
| status            | varchar(255)     | 
| processing_info   | varchar(255)     | 
| processing_person | varchar(255)     | 
| created_at        | timestamp        | 
| updated_at        | timestamp        | 


### 8.3 提交custodian订阅信息

```java
url: /api/v1/custodian-subscribe/new
method: POST
```


| Url RequestField | Type | 
| -------------- | --------| 
|email | String|

| ResponseField| Type |   
| -------------- | --------| 
| id                | int(10) unsigned | 
| email             | varchar(255)     | 
| status            | varchar(255)     | 
| processing_info   | varchar(255)     | 
| processing_person | varchar(255)     | 
| created_at        | timestamp        | 
| updated_at        | timestamp        | 


