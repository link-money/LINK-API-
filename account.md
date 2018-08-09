  
# 查询账户的API    

## 请求交互    

REST访问的根URL：  
- 主网：'http://47.75.115.19:8888'   
- 测试网：'http://116.62.226.231:8888'
	
请求交互说明    
- 请求参数：根据接口请求参数规定进行参数封装。    
- 提交请求参数：将封装好的请求参数通过 POST 或 GET 方式提交至服务器。    
- 服务器响应：服务器首先对用户请求数据进行参数安全校验，通过校验后根据业务逻辑将响应数据以JSON格式返回给用户。    
- 数据处理：对服务器响应数据进行处理。 

## API参考  

### 查询账户 API 

获取指定账户的所有信息  

1. Get /accounts/:id    获取指定账户的所有信息

URL `http://116.62.226.231:8888/accounts/{id}`	  
其中{id}是账户的地址  
示例:	

```
# Request

GET：   

http://116.62.226.231:8888/accounts/GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT  
```
### 1. 如果查询成功，那么：  
```
# Response
{
  "_links": {
    "self": {
      "href": "http://116.62.226.231:8888/accounts/GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT"
    },
    "transactions": {
      "href": "http://116.62.226.231:8888/accounts/GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT/transactions{?cursor,limit,order}",
      "templated": true
    },
    "operations": {
      "href": "http://116.62.226.231:8888/accounts/GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT/operations{?cursor,limit,order}",
      "templated": true
    },
    "payments": {
      "href": "http://116.62.226.231:8888/accounts/GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT/payments{?cursor,limit,order}",
      "templated": true
    },
    "effects": {
      "href": "http://116.62.226.231:8888/accounts/GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT/effects{?cursor,limit,order}",
      "templated": true
    },
    "offers": {
      "href": "http://116.62.226.231:8888/accounts/GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT/offers{?cursor,limit,order}",
      "templated": true
    },
    "trades": {
      "href": "http://116.62.226.231:8888/accounts/GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT/trades{?cursor,limit,order}",
      "templated": true
    },
    "data": {
      "href": "http://116.62.226.231:8888/accounts/GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT/data/{key}",
      "templated": true
    }
  },
  "id": "GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT",
  "paging_token": "",
  "account_id": "GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT",
  "sequence": "7821135446016",
  "subentry_count": 0,
  "thresholds": {
    "low_threshold": 0,
    "med_threshold": 0,
    "high_threshold": 0
  },
  "flags": {
    "auth_required": false,
    "auth_revocable": false
  },
  "balances": [
    {
      "balance": "20.0000000",
      "asset_type": "native"
    }
  ],
  "signers": [
    {
      "public_key": "GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT",
      "weight": 1,
      "key": "GD7RTAUCR2RZC6NYFMI4NVM7V2RNUBIOXRWQ2VVNJCU7X7U6HGL44IQT",
      "type": "ed25519_public_key"
    }
  ],
  "data": {}
}
```

返回值说明	 
 
- balances: 余额  
- balances键的值是一个列表，每个项代表一个资产的信息，每个项包含以下四个键：  
    - balance: 余额数量
    - limit: 限额
    - asset_type: 资产类型
    - asset_code: 资产代码
    - asset_issuer: 资产发行者  
- 这四个值都是字符串型数据，使用时请将balance和limit转换成Currency、Decimal或者Double等精度较高的类型  
  


### 2. 如果查询失败，最典型的是返回一个404错误，例如：  
```
# Response
{
  "type": "https://fotono.org/horizon-errors/not_found",
  "title": "Resource Missing",
  "status": 404,
  "detail": "The resource at the url requested was not found.  This is usually occurs for one of two reasons:  The url requested is not valid, or no data in our database could be found with the parameters provided."
}
```

返回值说明	 
 
- status: 错误代码  
- title: 错误类型，如果其值为'Resource Missing'，说明这个账户暂时不存在，意味着所有的资产余额都是0
  

请求参数	

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|id|String|是|账户的地址|
