---
title: GRID API Reference

search: true

code_clipboard: true
---

# API使用说明
前缀：
`http://api.gaiaopen.network`


完整的API地址为：`前缀`+`具体接口路径`

比如，获取账户信息接口为：
`http://api.gaiaopen.network/` + `/api/v1/getAccount?name=prefsabi@homes`

->

`http://api.gaiaopen.network/api/v1/getAccount?name=prefsabi@homes`


- 请注意我们仅支持https访问，不支持http访问。
- API请求：仅支持GET或POST请求。
- 如果为GET请求，所有请求参数以queryString方式传入，例如：/api/v1/getAccount?name=prefsabi@homes
- 如果为POST请求，所有请求参数以JSON形式作为Request Body传入。请求类型必须为Content-Type: application/json。

 
 ``` bash
所有的接口的返回形式都是统一为：

正常返回: 
{
  "errorCode": 0,
  "errorMsg": "",
  "data": 某种类型的数据，比如字符串，数字，字典等等
}

异常返回: 
{
  "errorCode": 具体的错误码,
  "errorMsg": "具体的错误信息字符串"
  "data": null
}
```


# 账户

## 获取账户信息

### HTTP Request

API路径：GET `/api/v1/getAccount`

> 示例:

```bash
/api/v1/getAccount?name=1@homes

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| name | Y | 账户名称 |


> 返回:

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

## 获取账户的Nonce

### HTTP Request

API路径：GET `/api/v1/getNonce`

> 示例:

```bash
/api/v1/getNonce?name=prefsabi@homes

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| name | Y | 账户名称 |


> 返回:

```json
{
    "data": 5,
    "errorCode": 0,
    "errorMsg": ""
}
```


## 获取账户余额

### HTTP Request

API路径：GET `/api/v1/getAccountBalance`

> 示例:

```bash
/api/v1/getAccountBalance?name=prefsabi@homes&assetId=0

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| name | Y | 账户名称 |
| assetId | Y | 资产ID |


> 返回:

```json
{
    "data": 9360999999,
    "errorCode": 0,
    "errorMsg": ""
}
```



## 账户是否存在

### HTTP Request

API路径：GET `/api/v1/accountExist`

> 示例:

```bash
/api/v1/accountExist?name=prefsabi@homes

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| name | Y | 账户名称 |


> 返回:

```json
{
    "data": true,
    "errorCode": 0,
    "errorMsg": ""
}
```

## 构建创建账户结构体

### HTTP Request

API路径：POST `/api/v1/triggerCreatAccount`

> 示例:

```json

{
    "accountName": "@demo",
    "assetId": 0,
    "amount": 100000000000,
    "newAccountName": "admin@demo",
    "founder": "@demo",
    "owner": {
        "type":"publickey",
        "value":"0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd"
    },
    "description": "",
    "remark": "hello"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名 | 
| assetId | Y | 资产ID | 
| amount | Y | 创建账户时转账数量 | 
| newAccountName | Y | 新账户名称 | 
| founder | Y | founder | 
| owner | Y | 所属人 | 
| type | Y | 类型 publickey address account | 
| value | Y | 值 | 
| description | N | 账户描述 | 
| remark | N | 账户备注 | 


> 返回:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "@demo",
                "assetId": 0,
                "remark": "hello",
                "amount": 100000000000,
                "newAccountName": "admin@demo",
                "founder": "@demo",
                "owner": {
                    "type": "publickey",
                    "value": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd"
                },
                "description": ""
            },
            "payloadParameter": {
                "accountName": "admin@demo",
                "founder": "@demo",
                "author": {
                    "owner": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd",
                    "weight": 1
                }
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1,
            "action": {
                "accountName": "@demo",
                "actionType": 256,
                "assetId": 0,
                "toAccountName": "account@acert",
                "gasLimit": 500000,
                "amount": 100000000000,
                "payload": "0xf8598a61646d696e4064656d6f854064656d6ff84501b841047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd0180",
                "remark": "hello",
                "nonce": 18
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

## 获取账户转账记录

### HTTP Request

API路径：POST `/api/v1/accountTransfers`

> 示例:

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

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名 | 
| onlyConfirmed | N | 是否已确认，默认false | 
| limit | N |  查询数量，1~40,默认20 | 
| fingerPrint | N |  查询下一批数据的指纹，首次传空 | 
| orderBy | Y | height#asc,height#desc | 
| searchInternal | N | 查询内部交易 | 
| assetId | N | 资产ID | 




> 返回:

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
                "state": 1,  //0:失败 1:成功
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



## 构建更新账户权重结构体

### HTTP Request

API路径：POST `/api/v1/triggerUpdateAccountAuthor`

> 示例:

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

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名 |
| assetId | Y | 资产ID |
| remark | Y | 备注 |
| activeAuthor | Y | activeAuthor |
| ownerAuthor | Y | ownerAuthor |
| publicKeyAuthors | N | 公钥列表 |
| accountAuthors | N | 账户列表 |
| addressAuthors | N | 地址列表 |
| owner | Y | owner |
| weight | Y | weight |
| authorActionType | Y | authorAction类型 0-添加 1-更新 2-删除 |

> 返回:

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




# 资产

## 构建增发资产结构体

### HTTP Request

API路径：POST `/api/v1/triggerIncrementAsset`

> 示例:

```json

{
    "accountName":"prefsabi@homes",
    "remark":"hello",
    "incrAssetId":1,
    "assetAmount":1000,
    "acceptor":"abc"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名称 |
| remark | N | 备注 |
| incrAssetId | Y | 增发资产ID |
| assetAmount | Y | 增发数量 |
| acceptor | Y | 受益账户 |


> 返回:

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


## 构建发行资产结构体

### HTTP Request

API路径：POST `/api/v1/triggerIssueAsset`

> 示例:

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

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名称 |
| founder | Y | founder |
| owner | Y | owner (必须和accountName保持一致)|
| remark | N | 备注 |
| assetName | Y | 资产全称 |
| symbol | Y | 资产简称 |
| assetAmount | Y | 资产数量 |
| decimals | Y | 精度 |
| upperLimit | Y | 发行上限 |
| contract | Y | 资产协议 |
| description | N | 描述 |



> 返回:

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


## 构建销毁资产结构体

### HTTP Request

API路径：POST `/api/v1/triggerDestroyAsset`

> 示例:

```json

{
    "accountName": "2@homes",
    "assetId": 2,
    "amount":1,
    "remark": "销毁资产"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名称 |
| assetId | Y | 资产ID |
| amount | Y | 数量 |
| remark | N | 备注 |


> 返回:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "2@homes",
                "assetId": 2,
                "remark": "销毁资产",
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
                "remark": "销毁资产",
                "nonce": 5
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}

```

## 根据资产ID查询币种的信息

### HTTP Request

API路径：GET `/api/v1/getAssetInfoById`

> 示例:

```bash
/api/v1/getAssetInfoById?assetId=22

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| assetId | Y | 资产ID |


> 返回:

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
        "description": "精神小伙",
        "logo":"data:image/gif;base64,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"
    },
    "errorCode": 0,
    "errorMsg": ""
}

```



## 根据币种全称获取币种信息

### HTTP Request

API路径：GET `/api/v1/getAssetInfoByName`

> 示例:

```bash
/api/v1/getAssetInfoByName?assetName=@gdemo::jsxh

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| assetName | Y | 资产名称 |


> 返回:

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
        "description": "精神小伙",
        "logo":"data:image/gif;base64,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"
    },
    "errorCode": 0,
    "errorMsg": ""
}

```


## 构建更新资产协议结构体

### HTTP Request

API路径：POST `/api/v1/triggerUpdateContract`

> 示例:

```json

{
    "accountName":"@homes",
    "remark":"更新",
    "assetId":2,
    "contract":"contract0002"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名称 |
| remark | N | 备注 |
| assetId | Y | 资产ID |
| contract | Y | 协议 |


> 返回:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "@homes",
                "assetId": 2,
                "contract": "contract0002",
                "remark": "更新"
            },
            "payloadParameter": {
                "assetId": 2,
                "contract": "contract0002"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "@homes",
                "actionType": 516,
                "assetId": 0,
                "toAccountName": "asset@gon",
                "gasLimit": 100000,
                "amount": 0,
                "payload": "0xce028c636f6e747261637430303032",
                "remark": "更新",
                "nonce": 87
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

# 区块
## 区块详情

### HTTP Request

API路径：GET `api/v1/block`

> 示例:

```bash
/api/v1/block?height=655443

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| height | Y | 高度 |

```json
{
    "data": {
        "height": 655443,
        "latestHeight": 660506,
        "timestamp": 1604370663,
        "hash": "0xa504ffd8be3695f743c4301fc5e07c749a6837647c79b4ffac4ba9e15c08ef6e",
        "producer": "miner1",
        "version": 1,
        "gasLimit": 30000000,
        "gasUsed": "30000000",
        "feeTotal": "30000000",
        "stateCount": 0
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

# 交易


## 构建转账结构体

### HTTP Request

API路径：POST `/api/v1/triggerTransfer`

> 示例:

```json

{
    "accountName":"prefsabi@homes",
    "assetId":0,
    "amount":1,
    "remark":"hello",
    "toAccountName":"prefsabi@homes"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名称 |
| assetId | Y | 资产ID |
| amount | Y | 数量 |
| remark | N | 备注 |
| toAccountName | Y | 转账目标账户 |


> 返回:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "prefsabi@homes",
                "assetId": 0,
                "remark": "hello",
                "amount": 1,
                "toAccountName": "prefsabi@homes"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "prefsabi@homes",
                "actionType": 515,
                "assetId": 0,
                "toAccountName": "prefsabi@homes",
                "gasLimit": 100000,
                "amount": 1,
                "payload": "",
                "remark": "hello",
                "nonce": 5
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

## 根据高度获取交易

### HTTP Request

API路径：POST `/api/v1/getTransactionsByHeight`

> 示例:

```bash
/api/v1/getTransactionsByHeight

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| height | Y | 高度 |
| page | Y | 页码 |
| pageSize | Y | 每页大小 |


> 返回:

```json
{
    "data": {
        "total": 300,
        "content": [
            {
                "txHash": "0x719bf58da147a34a572c85126edd0311fd34814e24a0609437c35815d5db0375",
                "feeAssetName": "acgas",
                "feeAssetSymbol": "acgas",
                "feeAssetId": 0,
                "feeTotal": "100000",
                "gasUsed": "100000",
                "gasPrice": 0,
                "state": "success",
                "actions": [
                    {
                        "assetName": "acgas",
                        "assetSymbol": "acgas",
                        "assetId": 0,
                        "actionType": "Transfer",
                        "from": "c37937",
                        "to": "owner@acert",
                        "amount": "1",
                        "payload": "\"\"",
                        "method": "",
                        "params": "",
                        "remark": "remark",
                        "state": 1,
                        "errorMsg": "",
                        "payer": "owner@acert",
                        "payerGasPrice": "1",
                        "parentSigner": "",
                        "payerParentSigner": ""
                    }
                ]
            }
        ]
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

## 根据Hash查询交易信息

### HTTP Request

API路径：GET `/api/v1/getTransactionInfoByHash`

> 示例:

```bash
/api/v1/getTransactionInfoByHash?hash=0x9895a5145d68988a7aca1fc242885cfb9b517fcb0fdac144eff5eea66cc682f0

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| hash | Y | 交易hash |


> 返回:

```json
{
    "data": {
        "blockHash": "0xf171ccd84fa580f710f3237f623341369ab8fd984ed7fa9b402cd9fab29ab19f",
        "height": 1150931,
        "actions": [
            {
                "actionInfo": {
                    "gasUsed": 500000,
                    "gasLimit": 20000000,
                    "gasPrice": 1000,
                    "gasAssetId": 0,
                    "fee": "500000000",
                    "feeAssetSymbol": "gcoin",
                    "feeAssetName": "gcoin",
                    "feeAssetId": 0,
                    "assetSymbol": "gcoin",
                    "assetName": "gcoin",
                    "assetId": 0,
                    "actionType": 256,
                    "from": "@gopen",
                    "to": "account@gon",
                    "amount": "100000000000",
                    "payload": "{\"accountName\":\"uc6363086f04@gopen\",\"founder\":\"@gopen\",\"publicKey\":\"0x0400000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000\"}",
                    "remark": "",
                    "state": 1,
                    "created": 1602644181,
                    "nonce": 1217,
                    "errorMsg": "",
                    "payer": "",
                    "payerParentSigner": "",
                    "parentSigner": "",
                    "authorObjs": "[{\"index\":0,\"owner\":\"0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd\",\"weight\":1}]",
                    "permitType": 0,
                    "threshold": 1
                },
                "inlineActionInfo": [
                    {
                        "assetName": "gcoin",
                        "assetSymbol": "gcoin",
                        "assetId": 0,
                        "actionType": 515,
                        "from": "account@gon",
                        "to": "uc6363086f04@gopen",
                        "amount": "100000000000",
                        "payload": "\"\"",
                        "remark": "",
                        "state": 1,
                        "errorMsg": ""
                    }
                ],
                "feeActionInfo": [
                    {
                        "assetName": "gcoin",
                        "assetSymbol": "gcoin",
                        "assetId": 0,
                        "actionType": "transfer",
                        "from": "@gopen",
                        "to": "spongebob115",
                        "amount": "100000000",
                        "type": 0
                    },
                    {
                        "assetName": "gcoin",
                        "assetSymbol": "gcoin",
                        "assetId": 0,
                        "actionType": "transfer",
                        "from": "@gopen",
                        "to": "founder@gon",
                        "amount": "400000000",
                        "type": 1
                    }
                ]
            }
        ]
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

## 查询交易状态

### HTTP Request

API路径：GET `/api/v1/getTransactionReceipt`

> 示例:

```bash
/api/v1/getTransactionReceipt?hash=0x3823383e6232d77016f1451a5b6955a977a1f254f73f9e5bdd4ba8c408a96a58

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| hash | Y | 交易hash |


> 返回:

```json
{
    "data": {
        "blockHash": "0x8f5aee795bfd0c5d5a843153f09c7e9dc9f4841566eb2276ab34dc752c908b9a",
        "blockNumber": 640129,
        "txHash": "0x6fecbb35aa6d3c2e80d374dcfe98adbc5c7e2210f58e31389215938e306c3ae9",
        "transactionIndex": 0,
        "postState": "0x7a2240f766a048c05808ac6dd30a6937e523cda951df5d4c4454d228987432d7",
        "actionResults": [
            {
                "gasAllot": [
                    {
                        "name": "spongebob114",
                        "gasLimit": 40000,
                        "typeId": 0
                    },
                    {
                        "name": "founder@gon",
                        "gasLimit": 160000,
                        "typeId": 1
                    }
                ],
                "authors": [
                    {
                        "index": 0,
                        "owner": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd",
                        "weight": 1
                    }
                ],
                "actionType": 0,
                "status": 1,
                "index": 0,
                "gasUsed": 200000,
                "parentIndex": 0,
                "permitType": 0,
                "permitThreshold": 1
            }
        ],
        "cumulativeGasUsed": 200000,
        "totalGasUsed": 200000,
        "logsBloom": "0x04000000000000000000000000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000400000000000000000001000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000008000000000000000020000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000001000800000000000000000000000000000000000001000000000000000000000200000000000000000000000000008000000008080000000000",
        "logs": [
            {
                "name": "suyuan12@gdemo",
                "topics": [
                    "0x310db99d4bb815b63325572e022beb8732ef30844192f3180639dc006cd15e48"
                ],
                "data": "0x000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000004703230300000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000066331303030310000000000000000000000000000000000000000000000000000",
                "blockNumber": 640129,
                "blockHash": "0x8f5aee795bfd0c5d5a843153f09c7e9dc9f4841566eb2276ab34dc752c908b9a",
                "transactionHash": "0x6fecbb35aa6d3c2e80d374dcfe98adbc5c7e2210f58e31389215938e306c3ae9",
                "logIndex": 0,
                "actionIndex": 0,
                "transactionIndex": 0
            },
            {
                "name": "suyuan12@gdemo",
                "topics": [
                    "0xd4412f0364abac1de2d4d29aa3ff724b9a6dd2e68ee93cae480e21f7f39e10fb",
                    "0x73ab18ea7f904cb5a084a573caf1280b6cd139a934275c56e8d6bf0b272e686b",
                    "0x0000000000000000000000000000000000000000000000000000000000000002"
                ],
                "data": "0x0000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000047465737400000000000000000000000000000000000000000000000000000000",
                "blockNumber": 640129,
                "blockHash": "0x8f5aee795bfd0c5d5a843153f09c7e9dc9f4841566eb2276ab34dc752c908b9a",
                "transactionHash": "0x6fecbb35aa6d3c2e80d374dcfe98adbc5c7e2210f58e31389215938e306c3ae9",
                "logIndex": 1,
                "actionIndex": 0,
                "transactionIndex": 0
            }
        ]
    },
    "errorCode": 0,
    "errorMsg": ""
}
```




# 合约

## 查看合约结果
### HTTP Request

API路径：POST `/api/v1/getContractResult`

> 示例:

```json

{
    "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"_key\",\"type\":\"string\"},{\"name\":\"_value\",\"type\":\"bytes\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_accountName\",\"type\":\"string\"},{\"name\":\"_key\",\"type\":\"string\"},{\"name\":\"_value\",\"type\":\"bytes\"}],\"name\":\"setEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_account\",\"type\":\"address\"}],\"name\":\"setWhiteList\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"_accountName\",\"type\":\"string\"},{\"name\":\"_key\",\"type\":\"string\"}],\"name\":\"get\",\"outputs\":[{\"name\":\"_value\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_account\",\"type\":\"address\"}],\"name\":\"delWhiteList\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
    "accountName":"@homes",
    "toAccountName":"prefsabi@homes",
    "function":"get",
    "parameters":["1","2"]
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| abi | Y | ABI 文件内容 |
| accountName | Y | 账户名称 |
| toAccountName | Y | 合约名称 |
| function | Y | 方法名称 |
| parameters | N | 参数 |


> 返回:

```json
{
    "data": {
        "result": "0x08c379a0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000146163636f756e74206973206e6f74206578697374000000000000000000000000",
        "parameter": {
            "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"_key\",\"type\":\"string\"},{\"name\":\"_value\",\"type\":\"bytes\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_accountName\",\"type\":\"string\"},{\"name\":\"_key\",\"type\":\"string\"},{\"name\":\"_value\",\"type\":\"bytes\"}],\"name\":\"setEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_account\",\"type\":\"address\"}],\"name\":\"setWhiteList\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"_accountName\",\"type\":\"string\"},{\"name\":\"_key\",\"type\":\"string\"}],\"name\":\"get\",\"outputs\":[{\"name\":\"_value\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_account\",\"type\":\"address\"}],\"name\":\"delWhiteList\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
            "accountName": "@homes",
            "toAccountName": "prefsabi@homes",
            "function": "get",
            "parameters": [
                "1",
                "2"
            ]
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```


## 获取合约信息

### HTTP Request

API路径：GET `/api/v1/getContract`

> 示例:

```bash
/api/v1/getContract?name=prefsabi@homes

```

### 请求参数

| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| name | Y | 合约名称 |


> 返回:

```json
{
    "data": {
        "abi": "[{\"constant\":false,\"inputs\":[],\"name\":\"unpause\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"pause\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_minAmount\",\"type\":\"uint256\"}],\"name\":\"setMinAmount\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getBaseInfo\",\"outputs\":[{\"name\":\"_originalAssetId\",\"type\":\"uint256\"},{\"name\":\"_lockAssetId\",\"type\":\"uint256\"},{\"name\":\"_minLockAmount\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"applyUnLock\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"cancleApply\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"unLock\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"lock\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"inputs\":[{\"name\":\"_originalAssetId\",\"type\":\"uint256\"},{\"name\":\"_lockAssetId\",\"type\":\"uint256\"},{\"name\":\"_minLockAmount\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
        "accountName": "prefsabi@homes",
        "founder": "@homes",
        "accountId": 4341,
        "accountType": 4,
        "number": 153574,
        "code": "608060405234801561001057600080fd5b5033600260006101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff1602179055506110fb806100616000396000f30060806040526004361061006d576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff1680632b29c0fa146100725780632efb374e146100c557806339e899ee146101305780633e10510b14610173578063605e5ee11461023f575b600080fd5b34801561007e57600080fd5b506100c3600480360381019080803590602001908201803590602001919091929391929390803590602001908201803590602001919091929391929390505050610282565b005b3480156100d157600080fd5b5061012e600480360381019080803590602001908201803590602001919091929391929390803590602001908201803590602001919091929391929390803590602001908201803590602001919091929391929390505050610400565b005b34801561013c57600080fd5b50610171600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291905050506106f2565b005b34801561017f57600080fd5b506101c4600480360381019080803590602001908201803590602001919091929391929390803590602001908201803590602001919091929391929390505050610843565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156102045780820151818401526020810190506101e9565b50505050905090810190601f1680156102315780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561024b57600080fd5b50610280600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610b0b565b005b606060008090506102c486868080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050610c54565b8092508193505050801515610341576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600f8152602001807f4b657920697320696c6c6567616c2e000000000000000000000000000000000081525060200191505060405180910390fd5b83836000803373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020846040518082805190602001908083835b6020831015156103b75780518252602082019150602081019050602083039250610392565b6001836020036101000a038019825116818451168082178552505050505050905001915050908152602001604051809103902091906103f792919061102a565b50505050505050565b600060606000600160003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff1615156001151514806104b25750600260009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff16145b15156104bd57600080fd5b88888080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050805190602001c95050925060008314151515610574576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260148152602001807f6163636f756e74206973206e6f7420657869737400000000000000000000000081525060200191505060405180910390fd5b600090506105b387878080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050610c54565b8092508193505050801515610630576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600f8152602001807f4b657920697320696c6c6567616c2e000000000000000000000000000000000081525060200191505060405180910390fd5b84846000808673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020846040518082805190602001908083835b6020831015156106a65780518252602082019150602081019050602083039250610681565b6001836020036101000a038019825116818451168082178552505050505050905001915050908152602001604051809103902091906106e692919061102a565b50505050505050505050565b600260009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff1614151561074e57600080fd5b600073ffffffffffffffffffffffffffffffffffffffff168173ffffffffffffffffffffffffffffffffffffffff161415151561078a57600080fd5b600160008273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff161515600015151415156107e957600080fd5b60018060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff02191690831515021790555050565b606060006060600087878080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050805190602001c95050925060008314151515610902576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260148152602001807f6163636f756e74206973206e6f7420657869737400000000000000000000000081525060200191505060405180910390fd5b6000905061094186868080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050610c54565b80925081935050508015156109be576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600f8152602001807f4b657920697320696c6c6567616c2e000000000000000000000000000000000081525060200191505060405180910390fd5b6000808473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020826040518082805190602001908083835b602083101515610a325780518252602082019150602081019050602083039250610a0d565b6001836020036101000a03801982511681845116808217855250505050505090500191505090815260200160405180910390208054600181600116156101000203166002900480601f016020809104026020016040519081016040528092919081815260200182805460018160011615610100020316600290048015610af95780601f10610ace57610100808354040283529160200191610af9565b820191906000526020600020905b815481529060010190602001808311610adc57829003601f168201915b50505050509350505050949350505050565b600260009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff16141515610b6757600080fd5b600073ffffffffffffffffffffffffffffffffffffffff168173ffffffffffffffffffffffffffffffffffffffff1614151515610ba357600080fd5b600160008273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff16151560011515141515610c0257600080fd5b600160008273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81549060ff021916905550565b6060600060606000849150600082511415610c755781600093509350611023565b600090505b815181101561101b5760217f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610cb557fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff191610158015610dcd5750607e7f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610d5d57fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff191611155b1515610ddf5781600093509350611023565b60417f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610e1157fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff191610158015610f295750605a7f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610eb957fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff191611155b1561100e5760208282815181101515610f3e57fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027f01000000000000000000000000000000000000000000000000000000000000009004017f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610fdd57fe5b9060200101907effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff1916908160001a9053505b8080600101915050610c7a565b816001935093505b5050915091565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f1061106b57803560ff1916838001178555611099565b82800160010185558215611099579182015b8281111561109857823582559160200191906001019061107d565b5b5090506110a691906110aa565b5090565b6110cc91905b808211156110c85760008160009055506001016110b0565b5090565b905600a165627a7a723058207ea610b86f39c314579e8ddde548904675a8b106112d6322255bf98848038bdb0029",
        "codeHash": "0x759bce2c71d45d28095345775510379fb180af521b35f9c03e197196c71cbe47",
        "threshold": 1,
        "updateAuthorThreshold": 1,
        "balances": [
            {
                "assetId": 0,
                "balance": 9360999999
            }
        ],
        "authors": [
            {
                "authorType": "pubKey",
                "author": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
                "weight": 1,
                "index": 0
            }
        ],
        "description": ""
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

## 构建调用智能合约结构体

### HTTP Request

API路径：POST `/api/v1/triggerSmartContract`

> 示例:

```json

{
    "accountName":"4@homes",
    "toAccountName":"4@homes",
    "assetId":0,
    "amount":0,
    "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
    "function":"addAss",
    "parameters":[1,4127,2],
    "remark":"你好"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名称 |
| toAccountName | Y | 合约账户 |
| assetId | Y | 资产ID |
| amount | Y | 数量 |
| abi | Y | abi文件内容 |
| function | Y | 方法名称 |
| parameters | N | 参数 |
| remark | N | 备注 |



> 返回:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "4@homes",
                "assetId": 0,
                "remark": "你好",
                "toAccountName": "4@homes",
                "amount": 0,
                "function": "addAss",
                "parameters": [
                    1,
                    4127,
                    2
                ]
            },
            "payloadParameter": {
                "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
                "function": "addAss",
                "parameters": [
                    1,
                    4127,
                    2
                ]
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "4@homes",
                "actionType": 0,
                "assetId": 0,
                "toAccountName": "4@homes",
                "gasLimit": 1000000,
                "amount": 0,
                "payload": "0x124de4710000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000101f0000000000000000000000000000000000000000000000000000000000000002",
                "remark": "你好",
                "nonce": 6
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```


## 构建创建合约结构体

### HTTP Request

API路径：POST `/api/v1/triggerCreateContract`

> 示例:

```json

{
    "accountName":"10@homes",
    "remark":"创建合约",
    "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
    "bin":"608060405261107a806100136000396000f300608060405260043610610128576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063124de4711461012a57806317d318bc146101815780631b05c0b2146102045780632b25a38b1461021b5780634708293e14610252578063483b80af146102ae5780634903b0d1146102db5780634bd464481461031c5780635ea32db51461035357806368669bc8146103de5780637a727a41146104285780637d3d999b1461045f57806389174bb7146104ac5780638a108c0e1461051a57806392ff0d31146105475780639b0fd02914610576578063b639096a146105c1578063bf2e5de414610678578063c3397814146106b9578063c6bcfa5c146106fa578063d38abe6b1461082c578063e80c2b311461086d575b005b34801561013657600080fd5b5061017f60048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506108c4565b005b34801561018d57600080fd5b506101e8600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506108e4565b604051808260070b60070b815260200191505060405180910390f35b34801561021057600080fd5b506102196108fa565b005b34801561022757600080fd5b506102506004803603810190808035906020019092919080359060200190929190505050610941565b005b6102ac600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506109d5565b005b3480156102ba57600080fd5b506102d9600480360381019080803590602001909291905050506109e1565b005b3480156102e757600080fd5b5061030660048036038101908080359060200190929190505050610a2d565b6040518082815260200191505060405180910390f35b34801561032857600080fd5b506103516004803603810190808035906020019092919080359060200190929190505050610a37565b005b34801561035f57600080fd5b506103ba600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290505050610c2c565b60405180848152602001838152602001828152602001935050505060405180910390f35b610426600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919080359060200190929190505050610c46565b005b34801561043457600080fd5b5061045d6004803603810190808035906020019092919080359060200190929190505050610c96565b005b34801561046b57600080fd5b506104aa600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610ce4565b005b3480156104b857600080fd5b50610518600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291908035906020019092919080359060200190929190803560070b9060200190929190505050610d42565b005b34801561052657600080fd5b5061054560048036038101908080359060200190929190505050610dcb565b005b34801561055357600080fd5b5061055c610e17565b604051808215151515815260200191505060405180910390f35b34801561058257600080fd5b506105ab6004803603810190808035906020019092919080359060200190929190505050610e20565b6040518082815260200191505060405180910390f35b3480156105cd57600080fd5b506105f66004803603810190808035906020019092919080359060200190929190505050610e2d565b6040518083815260200180602001828103825283818151815260200191508051906020019080838360005b8381101561063c578082015181840152602081019050610621565b50505050905090810190601f1680156106695780820380516001836020036101000a031916815260200191505b50935050505060405180910390f35b34801561068457600080fd5b506106a360048036038101908080359060200190929190505050610f5f565b6040518082815260200191505060405180910390f35b3480156106c557600080fd5b506106f8600480360381019080803590602001909291908035906020019092919080359060200190929190505050610f6f565b005b34801561070657600080fd5b506107b1600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290803590602001908201803590602001908080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050919291929080359060200190929190505050610fbf565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156107f15780820151818401526020810190506107d6565b50505050905090810190601f16801561081e5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561083857600080fd5b506108576004803603810190808035906020019092919050505061102f565b6040518082815260200191505060405180910390f35b34801561087957600080fd5b506108986004803603810190808035906020019092919050505061103a565b604051808460001916600019168152602001838152602001828152602001935050505060405180910390f35b828273ffffffffffffffffffffffffffffffffffffffff1682c150505050565b60008082805190602001cf905080915050919050565b6000ca90507f67657474780000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a150565b6000808383d0915091507f67657445706f63680000000000000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657445706f63680000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b80805190602001c05050565b600081cd90507f74657374476173000000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b6000819050919050565b60008060008060008060008888d296509650965096509650965096507f67657443616e64696461746500000000000000000000000000000000000000008760010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008660010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008560010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008460010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008360010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050505050505050565b600080600083805190602001c99250925092509193909250565b8273ffffffffffffffffffffffffffffffffffffffff166108fc838391821502919060405160006040518083038186868a8ac4945050505050158015610c90573d6000803e3d6000fd5b50505050565b60008282c690507f676574536e617073686f7454696d6500000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050565b7f67657462616c616e6365657800000000000000000000000000000000000000008273ffffffffffffffffffffffffffffffffffffffff1682c360010260405180826000191660001916815260200191505060405180910390a15050565b600080600191505b8260070b82131515610dc2578673ffffffffffffffffffffffffffffffffffffffff16868686c790507f676574536e617042616c616e63650000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a18180600101925050610d4a565b50505050505050565b600081d190507f67657443616e6469646174654e756d00000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b60006001905090565b60008282c8905092915050565b6000606060006060600080ca93507f64617461310000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a160646040519080825280601f01601f191660200182016040528015610eae5781602001602082028038833980820191505090505b509250878784805190602001c580601f01601f191660405101604052509150ca90507f64617461320000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a17f64617461330000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a1818395509550505050509250929050565b60008082d6905080915050919050565b6000838383d390507f676574566f7465725374616b65000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b606080600060146040519080825280601f01601f191660200182016040528015610ff85781602001602082028038833980820191505090505b50915085805190602001868051906020018580519060200189cc80601f01601f191660405101604052905081925050509392505050565b600081cb9050919050565b600080600083c292509250925091939092505600a165627a7a7230582002feaa902ba4a656f8e92bc4dca0e5d7636f039e341a027e3712920f2953c3a40029",
    "parameters":[]
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| accountName | Y | 账户名称 |
| remark | N | 备注 |
| abi | Y | abi文件内容 |
| bin | Y | bin文件内容 |
| parameters | N | 参数 |



> 返回:

```json
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "10@homes",
                "remark": "创建合约",
                "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
                "bin": "608060405261107a806100136000396000f300608060405260043610610128576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063124de4711461012a57806317d318bc146101815780631b05c0b2146102045780632b25a38b1461021b5780634708293e14610252578063483b80af146102ae5780634903b0d1146102db5780634bd464481461031c5780635ea32db51461035357806368669bc8146103de5780637a727a41146104285780637d3d999b1461045f57806389174bb7146104ac5780638a108c0e1461051a57806392ff0d31146105475780639b0fd02914610576578063b639096a146105c1578063bf2e5de414610678578063c3397814146106b9578063c6bcfa5c146106fa578063d38abe6b1461082c578063e80c2b311461086d575b005b34801561013657600080fd5b5061017f60048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506108c4565b005b34801561018d57600080fd5b506101e8600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506108e4565b604051808260070b60070b815260200191505060405180910390f35b34801561021057600080fd5b506102196108fa565b005b34801561022757600080fd5b506102506004803603810190808035906020019092919080359060200190929190505050610941565b005b6102ac600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506109d5565b005b3480156102ba57600080fd5b506102d9600480360381019080803590602001909291905050506109e1565b005b3480156102e757600080fd5b5061030660048036038101908080359060200190929190505050610a2d565b6040518082815260200191505060405180910390f35b34801561032857600080fd5b506103516004803603810190808035906020019092919080359060200190929190505050610a37565b005b34801561035f57600080fd5b506103ba600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290505050610c2c565b60405180848152602001838152602001828152602001935050505060405180910390f35b610426600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919080359060200190929190505050610c46565b005b34801561043457600080fd5b5061045d6004803603810190808035906020019092919080359060200190929190505050610c96565b005b34801561046b57600080fd5b506104aa600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610ce4565b005b3480156104b857600080fd5b50610518600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291908035906020019092919080359060200190929190803560070b9060200190929190505050610d42565b005b34801561052657600080fd5b5061054560048036038101908080359060200190929190505050610dcb565b005b34801561055357600080fd5b5061055c610e17565b604051808215151515815260200191505060405180910390f35b34801561058257600080fd5b506105ab6004803603810190808035906020019092919080359060200190929190505050610e20565b6040518082815260200191505060405180910390f35b3480156105cd57600080fd5b506105f66004803603810190808035906020019092919080359060200190929190505050610e2d565b6040518083815260200180602001828103825283818151815260200191508051906020019080838360005b8381101561063c578082015181840152602081019050610621565b50505050905090810190601f1680156106695780820380516001836020036101000a031916815260200191505b50935050505060405180910390f35b34801561068457600080fd5b506106a360048036038101908080359060200190929190505050610f5f565b6040518082815260200191505060405180910390f35b3480156106c557600080fd5b506106f8600480360381019080803590602001909291908035906020019092919080359060200190929190505050610f6f565b005b34801561070657600080fd5b506107b1600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290803590602001908201803590602001908080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050919291929080359060200190929190505050610fbf565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156107f15780820151818401526020810190506107d6565b50505050905090810190601f16801561081e5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561083857600080fd5b506108576004803603810190808035906020019092919050505061102f565b6040518082815260200191505060405180910390f35b34801561087957600080fd5b506108986004803603810190808035906020019092919050505061103a565b604051808460001916600019168152602001838152602001828152602001935050505060405180910390f35b828273ffffffffffffffffffffffffffffffffffffffff1682c150505050565b60008082805190602001cf905080915050919050565b6000ca90507f67657474780000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a150565b6000808383d0915091507f67657445706f63680000000000000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657445706f63680000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b80805190602001c05050565b600081cd90507f74657374476173000000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b6000819050919050565b60008060008060008060008888d296509650965096509650965096507f67657443616e64696461746500000000000000000000000000000000000000008760010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008660010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008560010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008460010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008360010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050505050505050565b600080600083805190602001c99250925092509193909250565b8273ffffffffffffffffffffffffffffffffffffffff166108fc838391821502919060405160006040518083038186868a8ac4945050505050158015610c90573d6000803e3d6000fd5b50505050565b60008282c690507f676574536e617073686f7454696d6500000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050565b7f67657462616c616e6365657800000000000000000000000000000000000000008273ffffffffffffffffffffffffffffffffffffffff1682c360010260405180826000191660001916815260200191505060405180910390a15050565b600080600191505b8260070b82131515610dc2578673ffffffffffffffffffffffffffffffffffffffff16868686c790507f676574536e617042616c616e63650000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a18180600101925050610d4a565b50505050505050565b600081d190507f67657443616e6469646174654e756d00000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b60006001905090565b60008282c8905092915050565b6000606060006060600080ca93507f64617461310000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a160646040519080825280601f01601f191660200182016040528015610eae5781602001602082028038833980820191505090505b509250878784805190602001c580601f01601f191660405101604052509150ca90507f64617461320000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a17f64617461330000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a1818395509550505050509250929050565b60008082d6905080915050919050565b6000838383d390507f676574566f7465725374616b65000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b606080600060146040519080825280601f01601f191660200182016040528015610ff85781602001602082028038833980820191505090505b50915085805190602001868051906020018580519060200189cc80601f01601f191660405101604052905081925050509392505050565b600081cb9050919050565b600080600083c292509250925091939092505600a165627a7a7230582002feaa902ba4a656f8e92bc4dca0e5d7636f039e341a027e3712920f2953c3a40029",
                "parameters": []
            },
            "payloadParameter": {
                "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
                "bin": "608060405261107a806100136000396000f300608060405260043610610128576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063124de4711461012a57806317d318bc146101815780631b05c0b2146102045780632b25a38b1461021b5780634708293e14610252578063483b80af146102ae5780634903b0d1146102db5780634bd464481461031c5780635ea32db51461035357806368669bc8146103de5780637a727a41146104285780637d3d999b1461045f57806389174bb7146104ac5780638a108c0e1461051a57806392ff0d31146105475780639b0fd02914610576578063b639096a146105c1578063bf2e5de414610678578063c3397814146106b9578063c6bcfa5c146106fa578063d38abe6b1461082c578063e80c2b311461086d575b005b34801561013657600080fd5b5061017f60048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506108c4565b005b34801561018d57600080fd5b506101e8600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506108e4565b604051808260070b60070b815260200191505060405180910390f35b34801561021057600080fd5b506102196108fa565b005b34801561022757600080fd5b506102506004803603810190808035906020019092919080359060200190929190505050610941565b005b6102ac600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506109d5565b005b3480156102ba57600080fd5b506102d9600480360381019080803590602001909291905050506109e1565b005b3480156102e757600080fd5b5061030660048036038101908080359060200190929190505050610a2d565b6040518082815260200191505060405180910390f35b34801561032857600080fd5b506103516004803603810190808035906020019092919080359060200190929190505050610a37565b005b34801561035f57600080fd5b506103ba600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290505050610c2c565b60405180848152602001838152602001828152602001935050505060405180910390f35b610426600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919080359060200190929190505050610c46565b005b34801561043457600080fd5b5061045d6004803603810190808035906020019092919080359060200190929190505050610c96565b005b34801561046b57600080fd5b506104aa600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610ce4565b005b3480156104b857600080fd5b50610518600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291908035906020019092919080359060200190929190803560070b9060200190929190505050610d42565b005b34801561052657600080fd5b5061054560048036038101908080359060200190929190505050610dcb565b005b34801561055357600080fd5b5061055c610e17565b604051808215151515815260200191505060405180910390f35b34801561058257600080fd5b506105ab6004803603810190808035906020019092919080359060200190929190505050610e20565b6040518082815260200191505060405180910390f35b3480156105cd57600080fd5b506105f66004803603810190808035906020019092919080359060200190929190505050610e2d565b6040518083815260200180602001828103825283818151815260200191508051906020019080838360005b8381101561063c578082015181840152602081019050610621565b50505050905090810190601f1680156106695780820380516001836020036101000a031916815260200191505b50935050505060405180910390f35b34801561068457600080fd5b506106a360048036038101908080359060200190929190505050610f5f565b6040518082815260200191505060405180910390f35b3480156106c557600080fd5b506106f8600480360381019080803590602001909291908035906020019092919080359060200190929190505050610f6f565b005b34801561070657600080fd5b506107b1600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290803590602001908201803590602001908080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050919291929080359060200190929190505050610fbf565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156107f15780820151818401526020810190506107d6565b50505050905090810190601f16801561081e5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561083857600080fd5b506108576004803603810190808035906020019092919050505061102f565b6040518082815260200191505060405180910390f35b34801561087957600080fd5b506108986004803603810190808035906020019092919050505061103a565b604051808460001916600019168152602001838152602001828152602001935050505060405180910390f35b828273ffffffffffffffffffffffffffffffffffffffff1682c150505050565b60008082805190602001cf905080915050919050565b6000ca90507f67657474780000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a150565b6000808383d0915091507f67657445706f63680000000000000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657445706f63680000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b80805190602001c05050565b600081cd90507f74657374476173000000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b6000819050919050565b60008060008060008060008888d296509650965096509650965096507f67657443616e64696461746500000000000000000000000000000000000000008760010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008660010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008560010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008460010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008360010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050505050505050565b600080600083805190602001c99250925092509193909250565b8273ffffffffffffffffffffffffffffffffffffffff166108fc838391821502919060405160006040518083038186868a8ac4945050505050158015610c90573d6000803e3d6000fd5b50505050565b60008282c690507f676574536e617073686f7454696d6500000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050565b7f67657462616c616e6365657800000000000000000000000000000000000000008273ffffffffffffffffffffffffffffffffffffffff1682c360010260405180826000191660001916815260200191505060405180910390a15050565b600080600191505b8260070b82131515610dc2578673ffffffffffffffffffffffffffffffffffffffff16868686c790507f676574536e617042616c616e63650000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a18180600101925050610d4a565b50505050505050565b600081d190507f67657443616e6469646174654e756d00000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b60006001905090565b60008282c8905092915050565b6000606060006060600080ca93507f64617461310000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a160646040519080825280601f01601f191660200182016040528015610eae5781602001602082028038833980820191505090505b509250878784805190602001c580601f01601f191660405101604052509150ca90507f64617461320000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a17f64617461330000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a1818395509550505050509250929050565b60008082d6905080915050919050565b6000838383d390507f676574566f7465725374616b65000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b606080600060146040519080825280601f01601f191660200182016040528015610ff85781602001602082028038833980820191505090505b50915085805190602001868051906020018580519060200189cc80601f01601f191660405101604052905081925050509392505050565b600081cb9050919050565b600080600083c292509250925091939092505600a165627a7a7230582002feaa902ba4a656f8e92bc4dca0e5d7636f039e341a027e3712920f2953c3a40029",
                "parameters": []
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "10@homes",
                "actionType": 1,
                "assetId": 0,
                "toAccountName": "10@homes",
                "gasLimit": 10000000,
                "amount": 0,
                "payload": "0x608060405261107a806100136000396000f300608060405260043610610128576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063124de4711461012a57806317d318bc146101815780631b05c0b2146102045780632b25a38b1461021b5780634708293e14610252578063483b80af146102ae5780634903b0d1146102db5780634bd464481461031c5780635ea32db51461035357806368669bc8146103de5780637a727a41146104285780637d3d999b1461045f57806389174bb7146104ac5780638a108c0e1461051a57806392ff0d31146105475780639b0fd02914610576578063b639096a146105c1578063bf2e5de414610678578063c3397814146106b9578063c6bcfa5c146106fa578063d38abe6b1461082c578063e80c2b311461086d575b005b34801561013657600080fd5b5061017f60048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506108c4565b005b34801561018d57600080fd5b506101e8600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506108e4565b604051808260070b60070b815260200191505060405180910390f35b34801561021057600080fd5b506102196108fa565b005b34801561022757600080fd5b506102506004803603810190808035906020019092919080359060200190929190505050610941565b005b6102ac600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506109d5565b005b3480156102ba57600080fd5b506102d9600480360381019080803590602001909291905050506109e1565b005b3480156102e757600080fd5b5061030660048036038101908080359060200190929190505050610a2d565b6040518082815260200191505060405180910390f35b34801561032857600080fd5b506103516004803603810190808035906020019092919080359060200190929190505050610a37565b005b34801561035f57600080fd5b506103ba600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290505050610c2c565b60405180848152602001838152602001828152602001935050505060405180910390f35b610426600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919080359060200190929190505050610c46565b005b34801561043457600080fd5b5061045d6004803603810190808035906020019092919080359060200190929190505050610c96565b005b34801561046b57600080fd5b506104aa600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610ce4565b005b3480156104b857600080fd5b50610518600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291908035906020019092919080359060200190929190803560070b9060200190929190505050610d42565b005b34801561052657600080fd5b5061054560048036038101908080359060200190929190505050610dcb565b005b34801561055357600080fd5b5061055c610e17565b604051808215151515815260200191505060405180910390f35b34801561058257600080fd5b506105ab6004803603810190808035906020019092919080359060200190929190505050610e20565b6040518082815260200191505060405180910390f35b3480156105cd57600080fd5b506105f66004803603810190808035906020019092919080359060200190929190505050610e2d565b6040518083815260200180602001828103825283818151815260200191508051906020019080838360005b8381101561063c578082015181840152602081019050610621565b50505050905090810190601f1680156106695780820380516001836020036101000a031916815260200191505b50935050505060405180910390f35b34801561068457600080fd5b506106a360048036038101908080359060200190929190505050610f5f565b6040518082815260200191505060405180910390f35b3480156106c557600080fd5b506106f8600480360381019080803590602001909291908035906020019092919080359060200190929190505050610f6f565b005b34801561070657600080fd5b506107b1600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290803590602001908201803590602001908080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050919291929080359060200190929190505050610fbf565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156107f15780820151818401526020810190506107d6565b50505050905090810190601f16801561081e5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561083857600080fd5b506108576004803603810190808035906020019092919050505061102f565b6040518082815260200191505060405180910390f35b34801561087957600080fd5b506108986004803603810190808035906020019092919050505061103a565b604051808460001916600019168152602001838152602001828152602001935050505060405180910390f35b828273ffffffffffffffffffffffffffffffffffffffff1682c150505050565b60008082805190602001cf905080915050919050565b6000ca90507f67657474780000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a150565b6000808383d0915091507f67657445706f63680000000000000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657445706f63680000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b80805190602001c05050565b600081cd90507f74657374476173000000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b6000819050919050565b60008060008060008060008888d296509650965096509650965096507f67657443616e64696461746500000000000000000000000000000000000000008760010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008660010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008560010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008460010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008360010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050505050505050565b600080600083805190602001c99250925092509193909250565b8273ffffffffffffffffffffffffffffffffffffffff166108fc838391821502919060405160006040518083038186868a8ac4945050505050158015610c90573d6000803e3d6000fd5b50505050565b60008282c690507f676574536e617073686f7454696d6500000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050565b7f67657462616c616e6365657800000000000000000000000000000000000000008273ffffffffffffffffffffffffffffffffffffffff1682c360010260405180826000191660001916815260200191505060405180910390a15050565b600080600191505b8260070b82131515610dc2578673ffffffffffffffffffffffffffffffffffffffff16868686c790507f676574536e617042616c616e63650000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a18180600101925050610d4a565b50505050505050565b600081d190507f67657443616e6469646174654e756d00000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b60006001905090565b60008282c8905092915050565b6000606060006060600080ca93507f64617461310000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a160646040519080825280601f01601f191660200182016040528015610eae5781602001602082028038833980820191505090505b509250878784805190602001c580601f01601f191660405101604052509150ca90507f64617461320000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a17f64617461330000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a1818395509550505050509250929050565b60008082d6905080915050919050565b6000838383d390507f676574566f7465725374616b65000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b606080600060146040519080825280601f01601f191660200182016040528015610ff85781602001602082028038833980820191505090505b50915085805190602001868051906020018580519060200189cc80601f01601f191660405101604052905081925050509392505050565b600081cb9050919050565b600080600083c292509250925091939092505600a165627a7a7230582002feaa902ba4a656f8e92bc4dca0e5d7636f039e341a027e3712920f2953c3a400293078",
                "remark": "创建合约",
                "nonce": 2
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

## 合约调用记录

### HTTP Request

API路径：POST `/api/v1/contractTransactions`

> 示例:

```json

{
    "contractName":"prefsabi@homes",
    "onlyConfirmed":true,
    "limit":2,
    "fingerPrint":"NdvyCiyhlWAGb0mNex9DPw",
    "orderBy":"height#asc",
    "searchInternal":false
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| contractName | Y | 合约名称 | 
| onlyConfirmed否 | 是否已确认，默认false | 
| limit | N  |  查询数量，1~40,默认20 | 
| fingerPrint | N  |  查询下一批数据的指纹，首次传空 | 
| orderBy | Y | height#asc,height#desc | 
| searchInternal | N | 查询内部交易 | 


> 返回:

```json
{
    "data": {
        "meta": {
            "limit": 2,
            "nextFingerPrint": "mkPRit03EH7GnVPCEwrh0A"
        },
        "content": [
            {
                "txHash": "0x9bb5b5a4f1597905379f6d91230327eaa989db5a2e404b71d86f68be0f8a50a5",
                "blockTime": 1599475284,
                "height": 153816,
                "fromAccount": "@homes",
                "toAccount": "prefsabi@homes",
                "assetSymbol": "gcoin",
                "assetName": "gcoin",
                "decimals": 10,
                "assetId": 0,
                "amount": 0,
                "transactionType": "general",
                "payload": "0x3e10510b00000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000000640686f6d65730000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001b636f6e74726163742e707265667361626940686f6d65732e6162690000000000",
                "state": 1, //0:失败 1:成功
                "errorMsg": ""
            },
            {
                "txHash": "0x4c90f30f260132b2e6ad9d9c25dbc194e08d725259b38d32b29f78ef3ab815cf",
                "blockTime": 1599475500,
                "height": 153888,
                "fromAccount": "@homes",
                "toAccount": "prefsabi@homes",
                "assetSymbol": "gcoin",
                "assetName": "gcoin",
                "decimals": 10,
                "assetId": 0,
                "amount": 0,
                "transactionType": "general",
                "payload": "0x2b29c0fa000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000014636f6e74726163742e3940686f6d65732e61626900000000000000000000000000000000000000000000000000000000000000000000000000000000000006015b7b22636f6e7374616e74223a66616c73652c22696e70757473223a5b5d2c226e616d65223a22756e7061757365222c226f757470757473223a5b5d2c2270617961626c65223a66616c73652c2273746174654d75746162696c697479223a226e6f6e70617961626c65222c2274797065223a2266756e6374696f6e227d2c7b22636f6e7374616e74223a66616c73652c22696e70757473223a5b5d2c226e616d65223a227061757365222c226f757470757473223a5b5d2c2270617961626c65223a66616c73652c2273746174654d75746162696c697479223a226e6f6e70617961626c65222c2274797065223a2266756e6374696f6e227d2c7b22636f6e7374616e74223a66616c73652c22696e70757473223a5b7b226e616d65223a225f6d696e416d6f756e74222c2274797065223a2275696e74323536227d5d2c226e616d65223a227365744d696e416d6f756e74222c226f757470757473223a5b5d2c2270617961626c65223a66616c73652c2273746174654d75746162696c697479223a226e6f6e70617961626c65222c2274797065223a2266756e6374696f6e227d2c7b22636f6e7374616e74223a66616c73652c22696e70757473223a5b5d2c226e616d65223a227472616e7366657261626c65222c226f757470757473223a5b7b226e616d65223a22222c2274797065223a22626f6f6c227d5d2c2270617961626c65223a66616c73652c2273746174654d75746162696c697479223a226e6f6e70617961626c65222c2274797065223a2266756e6374696f6e227d2c7b22636f6e7374616e74223a747275652c22696e70757473223a5b5d2c226e616d65223a2267657442617365496e666f222c226f757470757473223a5b7b226e616d65223a225f6f726967696e616c41737365744964222c2274797065223a2275696e74323536227d2c7b226e616d65223a225f6c6f636b41737365744964222c2274797065223a2275696e74323536227d2c7b226e616d65223a225f6d696e4c6f636b416d6f756e74222c2274797065223a2275696e74323536227d5d2c2270617961626c65223a66616c73652c2273746174654d75746162696c697479223a2276696577222c2274797065223a2266756e6374696f6e227d2c7b22636f6e7374616e74223a66616c73652c22696e70757473223a5b5d2c226e616d65223a226170706c79556e4c6f636b222c226f757470757473223a5b5d2c2270617961626c65223a66616c73652c2273746174654d75746162696c697479223a226e6f6e70617961626c65222c2274797065223a2266756e6374696f6e227d2c7b22636f6e7374616e74223a66616c73652c22696e70757473223a5b5d2c226e616d65223a2263616e636c654170706c79222c226f757470757473223a5b5d2c2270617961626c65223a66616c73652c2273746174654d75746162696c697479223a226e6f6e70617961626c65222c2274797065223a2266756e6374696f6e227d2c7b22636f6e7374616e74223a66616c73652c22696e70757473223a5b5d2c226e616d65223a22756e4c6f636b222c226f757470757473223a5b5d2c2270617961626c65223a747275652c2273746174654d75746162696c697479223a2270617961626c65222c2274797065223a2266756e6374696f6e227d2c7b22636f6e7374616e74223a66616c73652c22696e70757473223a5b5d2c226e616d65223a226c6f636b222c226f757470757473223a5b5d2c2270617961626c65223a747275652c2273746174654d75746162696c697479223a2270617961626c65222c2274797065223a2266756e6374696f6e227d2c7b22696e70757473223a5b7b226e616d65223a225f6f726967696e616c41737365744964222c2274797065223a2275696e74323536227d2c7b226e616d65223a225f6c6f636b41737365744964222c2274797065223a2275696e74323536227d2c7b226e616d65223a225f6d696e4c6f636b416d6f756e74222c2274797065223a2275696e74323536227d5d2c2270617961626c65223a66616c73652c2273746174654d75746162696c697479223a226e6f6e70617961626c65222c2274797065223a22636f6e7374727563746f72227d5d00000000000000000000000000000000000000000000000000000000000000",
                "state": 1,
                "errorMsg": ""
            }
        ]
    },
    "errorCode": 0,
    "errorMsg": ""
}
```


## 根据交易hash获取事件

### HTTP Request

API路径：POST `/api/v1/getEventByHash`

> 示例:

```json

{
    "txHash":"0xd7e108835d9aefcc7e04cbc0048c0299685e8e9543e8624e040f5b851aa23801",
    "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"name\",\"type\":\"string\"},{\"name\":\"weight\",\"type\":\"uint256\"}],\"name\":\"hasIndex\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":true,\"name\":\"name\",\"type\":\"string\"},{\"indexed\":true,\"name\":\"flag\",\"type\":\"bool\"},{\"indexed\":true,\"name\":\"weight\",\"type\":\"uint256\"}],\"name\":\"HasIndex\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"name\",\"type\":\"string\"},{\"indexed\":true,\"name\":\"flag\",\"type\":\"bool\"},{\"indexed\":false,\"name\":\"weight\",\"type\":\"uint256\"}],\"name\":\"TwoEvent\",\"type\":\"event\"}]"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| txHash | Y | 交易hash | 
| abi | Y | 合约abi | 


> 返回:

```json
{
    "data": [
        {
            "txHash": "0xd7e108835d9aefcc7e04cbc0048c0299685e8e9543e8624e040f5b851aa23801",
            "result": {
                "flag": true,
                "name": "0x32546a16566d300ff0ee51ca4dc99d92a9a1cc65a1badb8b6aacaa62b4cd71e1",
                "weight": 300
            },
            "resultType": {
                "flag": "bool",
                "name": "string",
                "weight": "uint256"
            },
            "blockTime": 1602732885,
            "height": 109524,
            "eventName": "HasIndex",
            "contract": "test8@demo",
            "eventIndex": 0,
            "confirmed": true
        },
        {
            "txHash": "0xd7e108835d9aefcc7e04cbc0048c0299685e8e9543e8624e040f5b851aa23801",
            "result": {
                "flag": false,
                "name": "lisi",
                "weight": 123
            },
            "resultType": {
                "flag": "bool",
                "name": "string",
                "weight": "uint256"
            },
            "blockTime": 1602732885,
            "height": 109524,
            "eventName": "TwoEvent",
            "contract": "test8@demo",
            "eventIndex": 1,
            "confirmed": true
        }
    ],
    "errorCode": 0,
    "errorMsg": ""
}
```


## 获取合约事件

### HTTP Request

API路径：POST `/api/v1/contractEvents`

> 示例:

```json

{
    "abi":"[{\"constant\":true,\"inputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"name\":\"groupList\",\"outputs\":[{\"name\":\"groupId\",\"type\":\"uint256\"},{\"name\":\"groupOwner\",\"type\":\"address\"},{\"name\":\"groupName\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_groupName\",\"type\":\"string\"},{\"name\":\"_groupOwner\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"addGroup\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_groupName\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"updateGroupName\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_targetId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"jiagong\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"chuku\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_actionName\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"addAction\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_id\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"yunshu\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_groupOwner\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"updateGroupOwner\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_id\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"chulan\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_user\",\"type\":\"string\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"addUserToGroup\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"user\",\"type\":\"string\"}],\"name\":\"setVerifyUser\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_actionName\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"modifyAction\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_packageId\",\"type\":\"string\"},{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"unpack\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_targetId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"breake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"xiaoshou\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"_user\",\"type\":\"string\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"}],\"name\":\"queryActionForUser\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_user\",\"type\":\"string\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"delUserFromGroup\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_id\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"siyang\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_packageId\",\"type\":\"string\"},{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"pack\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"zhijian\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_user\",\"type\":\"string\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"removeActionForUser\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"ruchang\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"_user\",\"type\":\"string\"},{\"name\":\"_groupId\",\"type\":\"uint256\"}],\"name\":\"queryGroupForUser\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"create\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_id\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"},{\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"cangchu\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_user\",\"type\":\"string\"},{\"name\":\"_groupId\",\"type\":\"uint256\"},{\"name\":\"_actionId\",\"type\":\"uint256\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"addActionForUser\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_productId\",\"type\":\"string\"},{\"name\":\"_remark\",\"type\":\"string\"},{\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"verify\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_groupName\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_groupOwner\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"AddGroup\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_groupOwner\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"UpdateGroupOwner\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_groupName\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"UpdateGroupName\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_actionId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_name\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"AddAction\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_actionId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_name\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"UpdateAction\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_user\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"AddUserToGroup\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_user\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"DelUserFromGroup\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_user\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_actionId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"AddActionForUser\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_user\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_actionId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"RemoveActionForUser\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_productId\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_action\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_remark\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"Create\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_productId\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_groupId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_action\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_remark\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"Tag\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_packageId\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_productId\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_remark\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"Pack\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_packageId\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_productId\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_remark\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"UnPack\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_productId\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_targetId\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_remark\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_deviceId\",\"type\":\"uint256\"},{\"indexed\":false,\"name\":\"_process\",\"type\":\"string\"}],\"name\":\"Break\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"_productId\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_remark\",\"type\":\"string\"},{\"indexed\":false,\"name\":\"_time\",\"type\":\"string\"}],\"name\":\"Verify\",\"type\":\"event\"}]",
    "topic":"UnPack(string,string,string,string,uint256,string)",
    "contractName":"suyuan13@demo",
    "onlyConfirmed":false,
    "limit":40,
    "fingerPrint":"",
    "orderBy":"height#asc"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| abi | Y | 合约abi | 
| topic | Y | 事件主题(含参数类型) | 
| contractName | Y | 合约名称 | 
| onlyConfirmed | N | 是否已确认，默认false | 
| limit | N  |  查询数量，1~40,默认20 | 
| fingerPrint | N  |  查询下一批数据的指纹，首次传空 | 
| orderBy | Y | height#asc,height#desc | 


> 返回:

```json
{
    "data": {
        "meta": {
            "limit": 2,
            "nextFingerPrint": "Gjc2sAOwnNkDRVvHKl6iPA"
        },
        "content": [
            {
                "txHash": "0x60ff4e651d9c8f8f90d6d14a2a7805e5ad72d3d170d7b0809ee3c44b83cad654",
                "result": {
                    "_deviceId": 400,
                    "_packageId": "B001",
                    "_process": "销售",
                    "_productId": "R001,R002,R003,R004,R005,R006",
                    "_remark": "{\"groupName\":\"销售1\",\"deviceName\":\"赵六的ipad\",\"actionName\":\"拆包\"}",
                    "_time": "1603267417"
                },
                "resultType": {
                    "_deviceId": "uint256",
                    "_packageId": "string",
                    "_process": "string",
                    "_productId": "string",
                    "_remark": "string",
                    "_time": "string"
                },
                "blockTime": 1603267419,
                "height": 287702,
                "eventName": "UnPack",
                "contract": "suyuan13@demo",
                "eventIndex": 0,
                "confirmed": true
            },
            {
                "txHash": "0x13c261e7f12df00bc9517dbb5fbc1ce4e963fce5d488b88d8917032a0fd52d94",
                "result": {
                    "_deviceId": 400,
                    "_packageId": "B002",
                    "_process": "销售",
                    "_productId": "R003001,R003002,R003003",
                    "_remark": "{\"groupName\":\"销售1\",\"deviceName\":\"赵六的ipad\",\"actionName\":\"拆包\"}",
                    "_time": "1603279845"
                },
                "resultType": {
                    "_deviceId": "uint256",
                    "_packageId": "string",
                    "_process": "string",
                    "_productId": "string",
                    "_remark": "string",
                    "_time": "string"
                },
                "blockTime": 1603279848,
                "height": 291845,
                "eventName": "UnPack",
                "contract": "suyuan13@demo",
                "eventIndex": 0,
                "confirmed": true
            }
        ]
    },
    "errorCode": 0,
    "errorMsg": ""
}
```




# 工具

## 获取链配置

### HTTP Request

API路径：GET `/api/v1/getChainConfig`

> 示例:

```bash
/api/v1/getChainConfig

```

> 返回:

```json
{
    "data": {
        "bootnodes": [
            "gnode://0469430d2d237a97f932e3aa62eca2d396458f8c41814f860c1afd5b4bed8b7c1e2fd4bba8277d016eb410994a2fe44812fc3edbe61dfb5ec275c7c375d10c2339@boot1.testnet.gaiaopen.network:30000",
            "gnode://04e24a53e2885fa60a9d6ecfc9e582bf11db0bea0881949268edafa5c4d35f9cbcfbaf7513a445f1dfb26ba465d752944078bfd21e22f263bb8bdc53d28248a727@boot2.testnet.gaiaopen.network:30000",
            "gnode://046f82c6136f72dbc56f3ff78048d9becc03e65d086c94ca426ceffee9bea637654924669d8c969c95f52aa2ffeb85a75337f9d6c37f4eb321b1064d6abe0d242d@boot3.testnet.gaiaopen.network:30000"
        ],
        "chainId": 1,
        "chainName": "gon",
        "chainUrl": "https://www.gaiaopen.network",
        "accountParams": {
            "level": 2
        },
        "assetParams": {
            "level": 2
        },
        "chargeParams": {
            "assetRatio": 80,
            "contractRatio": 80
        },
        "upgradeParams": {
            "blockCnt": 10000,
            "upgradeRatio": 80
        },
        "dposParams": {
            "maxURLLen": 512,
            "unitStake": 1,
            "candidateMinQuantity": 100000,
            "voterMinQuantity": 1,
            "activatedMinQuantity": 600000,
            "blockInterval": 3000,
            "blockFrequency": 6,
            "candidateScheduleSize": 6,
            "backupScheduleSize": 4,
            "extraBlockReward": 0,
            "blockReward": 0
        },
        "systemName": "founder@gon",
        "accountName": "account@gon",
        "assetName": "asset@gon",
        "dposName": "dpos@gon",
        "snapshotInterval": 3600000,
        "feeName": "fee@gon",
        "systemToken": "gcoin",
        "sysTokenDecimal": 9,
        "referenceTime": 1598284800000000000
    },
    "errorCode": 0,
    "errorMsg": ""
}

```


## 获取GAS价格

### HTTP Request

API路径：GET `/api/v1/getGasPrice`

> 示例:

```bash
/api/v1/getGasPrice

```

> 返回:

```json
{
    "data": 1000,
    "errorCode": 0,
    "errorMsg": ""
}

```


## 广播交易

### HTTP Request

API路径：POST `/api/v1/broadcast`

> 示例:

```json

{
   "rawData":"0xf8d9808203e8f8d3f8d18201004d808640686f6d65738b6163636f756e7440676f6e8307a12085174876e800b85bf859907465737430303030303340686f6d657380b841047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd833131318568656c6c6ff84a80f847f84525a059800c67532907db349f34313829c8e352ea1d6086dce948b9d6947505f79fa4a03a4ba027822c4133af61605ce0f761a4202125c20bea1612d8ad1b6fff0d66c7c180"
}
```

> 返回:

```json
{
    "data": "0x9ea88efbca2c4777112aec265947e5668059b50b9550a59255d78938f1d7a9ac",
    "errorCode": 0,
    "errorMsg": ""
}
```




## 签名
<aside class="warning">强烈不建议开发人员在生产环境使用该接口</aside>

### HTTP Request

API路径：POST `/api/v1/sign`

> 示例:

```json

{
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
        "remark": "销毁资产",
        "nonce": 3
    },
    "privateKey": "2f5949fb7ffd80cf1ee53fe7d840bec0dc0042f1d0e1fa6ee0f85b8f010cac17e"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| chainId | Y | 链ID |
| gasAssetId | Y | gas资产ID |
| gasPrice | Y | gas价格 |
| action | Y | 要签名的action内容 |
| privateKey | Y | 私钥 |

> 返回:

```json
{
    "data": "0x9ea88efbca2c4777112aec265947e5668059b50b9550a59255d78938f1d7a9ac",
    "errorCode": 0,
    "errorMsg": ""
}
```

## 合约payload解码

### HTTP Request

API路径：POST `/api/v1/contractPayloadDecode`

> 示例:

```json

{
	"abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"name\",\"type\":\"string\"},{\"name\":\"businessName\",\"type\":\"string\"},{\"name\":\"time\",\"type\":\"string\"},{\"name\":\"addr\",\"type\":\"string\"},{\"name\":\"num\",\"type\":\"string\"},{\"name\":\"grade\",\"type\":\"string\"},{\"name\":\"qa\",\"type\":\"string\"}],\"name\":\"storeProduct\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"qiname\",\"outputs\":[{\"name\":\"\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"productName\",\"outputs\":[{\"name\":\"\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"owner\",\"outputs\":[{\"name\":\"\",\"type\":\"address\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"amount\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getAmount\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"name\",\"type\":\"string\"},{\"name\":\"gongshang\",\"type\":\"string\"},{\"name\":\"admin\",\"type\":\"string\"},{\"name\":\"time\",\"type\":\"string\"},{\"name\":\"addr\",\"type\":\"string\"}],\"name\":\"storeBusiness\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"}]",
	"payload":"0xf0d8927a00000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000120000000000000000000000000000000000000000000000000000000000000016000000000000000000000000000000000000000000000000000000000000001a000000000000000000000000000000000000000000000000000000000000000056e616d6531000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000a676f6e677368616e673100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000661646d696e310000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000574696d653100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000046164647200000000000000000000000000000000000000000000000000000000"
}
```

### 请求参数
| 字段名称 | 是否必须 | 描述 |
| --- | ------|-------------|
| abi | Y | ABI文件内容 |
| payload | Y | payload内容 |



> 返回:

```json
{
    "data": {
        "method": "storeBusiness",
        "parameter": {
            "addr": "addr",
            "admin": "admin1",
            "gongshang": "gongshang1",
            "name": "name1",
            "time": "time1"
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}

```

# 参数解释

## 返回参数

### action参数

名称 | 备注
---|---
gasAssetId | gas资产ID
gasPrice | gasPrice
accountName | 账户名
actionType | action类型值
assetId | 资产ID
toAccountName | to账户
gasLimit | gasLimit
amount | 资金数量
payload | payload
remark | 备注
nonce | nonce


### actionType 参数
名称 | 备注
---|---
0 | 调用合约
1 | 创建合约
256 | 创建账户
257 | 更新账户
259 | 更新账户权重
512 | 增发资产
513 | 发行资产 
514 | 销毁资产
515 | 转账
516 | 更新资产协议

### accountType 参数
名称 | 备注
---|---
1 | 系统根账户
2 | 系统子账户
3 | 社区根账户
4 | 社区子账户
5 | 个人账户
6 | 特殊账户
