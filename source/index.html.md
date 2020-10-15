---
title: GRID API Reference

search: true

code_clipboard: true
---

# API instructions
Prefix：
`https://api.testnet.gaiaopen.network`


The complete API address is：`Prefix`+`Specific interface path`

For example, the interface for obtaining account information is：
`https://api.testnet.gaiaopen.network/` + `/api/v1/getAccount?name=prefsabi@homes`

->

`https://api.testnet.gaiaopen.network/api/v1/getAccount?name=prefsabi@homes`


- Please note that we only support https access, not http access.
- API request: Only GET or POST requests are supported.
- If it is a GET request, all request parameters are passed in as queryString, for example：/api/v1/getAccount?name=prefsabi@homes
- If it is a POST request, all request parameters are passed in as Request Body in JSON format.The request type must be Content-Type: application/json。

 
 ``` bash
The return form of all interfaces is unified as：

Normal return: 
{
  "errorCode": 0,
  "errorMsg": "",
  "data": Certain types of data, such as strings, numbers, dictionaries, etc.
}

Abnormal return: 
{
  "errorCode": Specific error code,
  "errorMsg": "Specific error message string"
  "data": null
}
```


# Account

## Get account information

### HTTP Request

API path：GET `/api/v1/getAccount`

> Example:

```bash
/api/v1/getAccount?name=1@homes

```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| name | Y | account name |


> return:

```json
{
    "data": {
        "accountName": "1@homes",
        "founder": "1@homes",
        "accountId": 4117,
        "accountType": 4,
        "number": 2157,
        "code": "",
        "codeHash": "0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
        "threshold": 4,
        "updateAuthorThreshold": 5,
        "balances": [
            {
                "assetId": 0,
                "balance": 999399999998
            },
            {
                "assetId": 2,
                "balance": 2100
            }
        ],
        "authors": [
            {
                "authorType": "pubKey",
                "author": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
                "weight": 2,
                "index": 0
            },
            {
                "authorType": "account",
                "author": "3@homes",
                "weight": 2,
                "index": 1
            },
            {
                "authorType": "address",
                "author": "0x286784414F31B095446d65AB244C15d683CdB7A6",
                "weight": 2,
                "index": 2
            },
            {
                "authorType": "pubKey",
                "author": "0x04f3feb1c117be0f22ce083afd03fb1dc998c9c0d6c1525e75e7b644d116e35af9d31e2dadbe48cd6e9ff2499114b8008792f60243af29df5e729be7a5eefdb64e",
                "weight": 1,
                "index": 3
            },
            {
                "authorType": "pubKey",
                "author": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd",
                "weight": 2,
                "index": 4
            }
        ],
        "description": ""
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

## Get the Nonce of the account

### HTTP Request

API path：GET `/api/v1/getNonce`

> Example:

```bash
/api/v1/getNonce?name=prefsabi@homes

```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| name | Y | account name |


> return:

```json
{
    "data": 5,
    "errorCode": 0,
    "errorMsg": ""
}
```


## Get account balance

### HTTP Request

API path：GET `/api/v1/getAccountBalance`

> Example:

```bash
/api/v1/getAccountBalance?name=prefsabi@homes&assetId=0

```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| name | Y | account name |
| assetId | Y | Asset ID |


> return:

```json
{
    "data": 9360999999,
    "errorCode": 0,
    "errorMsg": ""
}
```



## Does the account exist

### HTTP Request

API path：GET `/api/v1/accountExist`

> Example:

```bash
/api/v1/accountExist?name=prefsabi@homes

```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| name | Y | account name |


> return:

```json
{
    "data": true,
    "errorCode": 0,
    "errorMsg": ""
}
```

## Build a structure for creating an account

### HTTP Request

API path：POST `/api/v1/triggerCreatAccount`

> Example:

```json

{
    "accountName": "@homes",
    "assetId": 0,
    "amount": 100000000000,
    "newAccountName": "test000003@homes",
    "founder": "test000003@homes",
    "publicKey": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd",
    "description": "",
    "remark": "hello"
}
```

### Request parameter
| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name | 
| assetId | Y | Asset ID | 
| amount | Y | Number of transfers when creating an account | 
| newAccountName | Y | New account name | 
| founder | Y | founder | 
| publicKey | Y | publicKey | 
| description | N | description | 
| remark | N | remark | 


> return:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "@homes",
                "assetId": 0,
                "remark": "hello",
                "amount": 100000000000,
                "newAccountName": "test000003@homes",
                "founder": "test000003@homes",
                "publicKey": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd",
                "description": ""
            },
            "payloadParameter": {
                "accountName": "test000003@homes",
                "founder": "test000003@homes",
                "publicKey": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "@homes",
                "actionType": 256,
                "assetId": 0,
                "toAccountName": "account@gon",
                "gasLimit": 500000,
                "amount": 100000000000,
                "payload": "0xf866907465737430303030303340686f6d6573907465737430303030303340686f6d6573b841047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd80",
                "remark": "hello",
                "nonce": 87
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

## Get account transfer records

### HTTP Request

API path：POST `/api/v1/accountTransfers`

> Example:

```json

{
    "accountName":"@homes",
    "onlyConfirmed":true,
    "limit":2,
    "fingerPrint":"",
    "orderBy":"height#asc",
    "searchInternal":true,
    "assetId": 0
}
```

### Request parameter
| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name | 
| onlyConfirmed | N | Whether it has been confirmed, the default is false | 
| limit | N |  Number of queries, 1~40, default 20 | 
| fingerPrint | N |  Query the fingerprint of the next batch of data, and pass it blank for the first time | 
| orderBy | Y | height#asc,height#desc | 
| searchInternal | N | Query internal transactions | 
| assetId | N | Asset ID | 




> return:

```json
{
    "data": {
        "meta": {
            "limit": 2,
            "nextFingerPrint": "FSteDh-5rhICh2qGrJMJHw"
        },
        "content": [
            {
                "txHash": "0x24d9ec4da570ca20bc6237078037823c94a9f9a893f8e0252bbb212ab6b382ff",
                "blockTime": 1599020193,
                "height": 2155,
                "fromAccount": "account@gon",
                "toAccount": "@homes",
                "assetSymbol": "gcoin",
                "assetName": "gcoin",
                "decimals": 10,
                "assetId": 0,
                "amount": 100000000000000,
                "transactionType": "internal",
                "payload": "",
                "state": 1,  //0: Failure 1: Success
                "remark": "",
                "errorMsg": ""
            },
            {
                "txHash": "0x3d9ea766c2eaba54dde2ee91bbdb48ff124c97b871b090e69633c96266f33419",
                "blockTime": 1599027123,
                "height": 4465,
                "fromAccount": "asset@gon",
                "toAccount": "@homes",
                "assetSymbol": "tail",
                "assetName": "@homes::item1",
                "decimals": 10,
                "assetId": 2,
                "amount": 11,
                "transactionType": "internal",
                "payload": "",
                "state": 1,
                "remark": "",
                "errorMsg": ""
            }
        ]
    },
    "errorCode": 0,
    "errorMsg": ""
}
```



## Build a structure for updating account weights

### HTTP Request

API path：POST `/api/v1/triggerUpdateAccountAuthor`

> Example:

```json

{
    "accountName": "3@homes",
    "assetId": 0,
    "remark": "hello",
    "publicKeyAuthors": [
        {
            "owner": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
            "weight": 3,
            "authorActionType":1
        }
    ],
    "accountAuthors": [
        {
            "owner": "3@homes",
            "weight": 3,
            "authorActionType":1
        }
    ],
    "addressAuthors": [
        {
            "owner": "0x04474da0e3024d2089888dd60b",
            "weight": 3,
            "authorActionType":1
        }
    ],
    "activeAuthor": 3,
    "ownerAuthor": 4
}
```

###  Request parameter
| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| assetId | Y | Asset ID |
| remark | Y | remark |
| activeAuthor | Y | activeAuthor |
| ownerAuthor | Y | ownerAuthor |
| publicKeyAuthors | N | PublicKey list |
| accountAuthors | N | Account list |
| addressAuthors | N | Address list |
| owner | Y | owner |
| weight | Y | weight |
| authorActionType | Y | authorAction type 0-add 1-update 2-delete |

> return:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "3@homes",
                "remark": "hello",
                "publicKeyAuthors": [
                    {
                        "authorActionType": 1,
                        "owner": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
                        "weight": 3
                    }
                ],
                "accountAuthors": [
                    {
                        "authorActionType": 1,
                        "owner": "3@homes",
                        "weight": 3
                    }
                ],
                "addressAuthors": [
                    {
                        "authorActionType": 1,
                        "owner": "0x04474da0e3024d2089888dd60b",
                        "weight": 3
                    }
                ],
                "activeAuthor": 3,
                "ownerAuthor": 4
            },
            "payloadParameter": {
                "threshold": 3,
                "updateAuthorThreshold": 4,
                "authorActions": [
                    {
                        "actionType": 1,
                        "author": {
                            "owner": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
                            "weight": 3
                        }
                    },
                    {
                        "actionType": 1,
                        "author": {
                            "owner": "3@homes",
                            "weight": 3
                        }
                    },
                    {
                        "actionType": 1,
                        "author": {
                            "owner": "0x0000000000000004474DA0E3024d2089888Dd60B",
                            "weight": 3
                        }
                    }
                ]
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "3@homes",
                "actionType": 259,
                "assetId": 0,
                "toAccountName": "account@gon",
                "gasLimit": 100000,
                "amount": 0,
                "payload": "0xf8750304f871f84801f84501b84104474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c503cc01ca80873340686f6d657303d901d702940000000000000004474da0e3024d2089888dd60b03",
                "remark": "hello",
                "nonce": 4
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```




# assets

## Build the structure of additional assets

### HTTP Request

API path：POST `/api/v1/triggerIncrementAsset`

> Example:

```json

{
    "accountName":"prefsabi@homes",
    "remark":"hello",
    "incrAssetId":1,
    "assetAmount":1000,
    "acceptor":"abc"
}
```

### Request parameter
| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| remark | N | remark |
| incrAssetId | Y | Additional asset ID |
| assetAmount | Y | Number of additional issuances |
| acceptor | Y | Benefit account |


> return:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "prefsabi@homes",
                "remark": "hello",
                "incrAssetId": 1,
                "assetAmount": 1000,
                "acceptor": "abc"
            },
            "payloadParameter": {
                "assetId": 1,
                "amount": 1000,
                "acceptor": "abc"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "prefsabi@homes",
                "actionType": 512,
                "assetId": 0,
                "toAccountName": "asset@gon",
                "gasLimit": 100000,
                "amount": 0,
                "payload": "0xc8018203e883616263",
                "remark": "hello",
                "nonce": 5
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```


## Build a structure for issuing assets

### HTTP Request

API path：POST `/api/v1/triggerIssueAsset`

> Example:

```json

{
    "accountName": "prefsabi@homes",
    "founder": "prefsabi@homes",
    "owner": "prefsabi@homes",
    "remark": "hello",
    "assetName": "timmyhahahaha",
    "symbol": "th",
    "assetAmount": 1000,
    "decimals": 1,
    "upperLimit": 2000,
    "contract": "hello world",
    "description": "hello"
}
```

### Request parameter
| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| founder | Y | founder |
| owner | Y | owner (Must be consistent with accountName)|
| remark | N | remark |
| assetName | Y | Full name of assets |
| symbol | Y | Asset abbreviation |
| assetAmount | Y | Number of assets |
| decimals | Y | decimals |
| upperLimit | Y | Asset issuance ceiling |
| contract | Y | Asset Agreement |
| description | N | description |



> return:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "prefsabi@homes",
                "founder": "prefsabi@homes",
                "owner": "prefsabi@homes",
                "remark": "hello",
                "assetName": "timmyhahahaha",
                "symbol": "th",
                "assetAmount": 1000,
                "decimals": 1,
                "upperLimit": 2000,
                "contract": "hello world",
                "description": "hello"
            },
            "payloadParameter": {
                "assetName": "timmyhahahaha",
                "symbol": "th",
                "amount": 1000,
                "decimals": 1,
                "founder": "prefsabi@homes",
                "owner": "prefsabi@homes",
                "upperLimit": 2000,
                "contract": "hello world",
                "description": "hello"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "prefsabi@homes",
                "actionType": 513,
                "assetId": 0,
                "toAccountName": "asset@gon",
                "gasLimit": 10000000,
                "amount": 0,
                "payload": "0xf8488d74696d6d7968616861686168618274688203e8018e707265667361626940686f6d65738e707265667361626940686f6d65738207d08b68656c6c6f20776f726c648568656c6c6f",
                "remark": "hello",
                "nonce": 5
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```


## Build a structure for destroying assets

### HTTP Request

API path：POST `/api/v1/triggerDestroyAsset`

> Example:

```json

{
    "accountName": "2@homes",
    "assetId": 2,
    "amount":1,
    "remark": "Destroy assets"
}
```

### Request parameter
| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| assetId | Y | Asset ID |
| amount | Y | Quantity |
| remark | N | remark |


> return:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "2@homes",
                "assetId": 2,
                "remark": "Destroy assets",
                "amount": 1
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "2@homes",
                "actionType": 514,
                "assetId": 2,
                "toAccountName": "asset@gon",
                "gasLimit": 100000,
                "amount": 1,
                "payload": "",
                "remark": "Destroy assets",
                "nonce": 5
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}

```

## Query currency information based on asset ID

### HTTP Request

API path：GET `/api/v1/getAssetInfoById`

> Example:

```bash
/api/v1/getAssetInfoById?assetId=22

```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| assetId | Y | Asset ID |


> return:

```json
{
    "data": {
        "assetId": 22,
        "assetName": "@gdemo::jsxh",
        "symbol": "jsxh",
        "amount": 1000,
        "decimals": 0,
        "founder": "@gdemo",
        "owner": "@gdemo",
        "addIssue": 1000,
        "upperLimit": 0,
        "contract": "item@gdemo",
        "createdAt": 1599049965,
        "destructionNum": 0,
        "description": "Spirit guy",
        "logo":"data:image/gif;base64,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