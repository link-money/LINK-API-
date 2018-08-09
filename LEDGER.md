  
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

### 查询账本（区块） API 

获取指定账本的所有信息  

1. Get /ledgers/:id    获取指定账本的所有信息

URL `http://116.62.226.231:8888/ledgers/{id}`	  
其中{id}是账本的序号  
示例:	

```
# Request

GET：   

http://116.62.226.231:8888/ledgers/619/ 
```
### 1. 如果查询成功，那么：  
```
# Response

{
  "_links": {
    "self": {
      "href": "http://116.62.226.231:8888/ledgers/619"
    },
    "transactions": {
      "href": "http://116.62.226.231:8888/ledgers/619/transactions{?cursor,limit,order}",
      "templated": true
    },
    "operations": {
      "href": "http://116.62.226.231:8888/ledgers/619/operations{?cursor,limit,order}",
      "templated": true
    },
    "payments": {
      "href": "http://116.62.226.231:8888/ledgers/619/payments{?cursor,limit,order}",
      "templated": true
    },
    "effects": {
      "href": "http://116.62.226.231:8888/ledgers/619/effects{?cursor,limit,order}",
      "templated": true
    }
  },
  "id": "3703fbb5a4dff7ab8c1e8ab53420ad87677f62686a01566e6015a209eb683287",
  "paging_token": "2658584756224",
  "hash": "3703fbb5a4dff7ab8c1e8ab53420ad87677f62686a01566e6015a209eb683287",
  "prev_hash": "955e33dce141f87bb8705e605eafabf338f46552aa98ea47dc4931ef4c5ca9d3",
  "sequence": 619,
  "transaction_count": 1,
  "operation_count": 1,
  "closed_at": "2018-08-07T02:37:20Z",
  "total_coins": "100000000000.0000000",
  "fee_pool": "0.0005000",
  "base_fee_in_stroops": 5000,
  "base_reserve_in_stroops": 100000000,
  "max_tx_set_size": 100,
  "protocol_version": 0,
  "header_xdr": "AAAAAJVeM9zhQfh7uHBeYF6vq/M49GVSqpjqR9xJMe9MXKnTbmn+u+tPAziuhvLO86aOjaN1DhNO9h/2ccPl/L3IOo0AAAAAW2kF4AAAAAAAAAAA4K7H0NDNO+W2xprSvzBOFk5FRmDuhaOeRCeqs+j0Hu/nZuk1p/Af6DHupp6D5x+o295BAe4J2l0iJmDrOEg4EAAAAmsN4Lazp2QAAAAAAAAAABOIAAAAAAAAAAAAAAAAAAATiAX14QAAAABkrJ1pvciwSHDTUlchvhjS7A98ZcowdCkwLULBcdpBiZ4AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"
}
```

返回值说明	 
 
- sequence: 账本序号  
- closed_at： 账本关闭（区块结束）的时间

  

如果查询失败，最典型的是返回一个404错误，例如：  
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
|id|String|是|账本的序号(如果不填则返回所有账本)|
