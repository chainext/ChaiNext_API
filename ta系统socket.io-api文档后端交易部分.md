## 后端交易
## 功能
* login：登录
* ordinary_new_order：普通订单
* query_collective_order：TA查询集合订单执行情况
* fund_quote&info：基金报价与基本信息
* query_fund_info：基金经理主动查询基金基本信息
* subscribe_message：特殊情况沟通
* wholesale_order：大额订单
* wholesale_order_outcome：大额订单执行结果

## 各api接口详解

### 基本规范

- socket.io 规范

- 数据

  - 时间戳：13 位 unix 时间戳，精确到毫秒

- 请求数据 json 格式统一样例

```json
{
  "requestId": "流水号 使用uuid自动生成，唯一即可不过多要求",
  "version": "",
  "data": {}
}
```

- 响应回执 json 格式统一样例

```json
{
  "code": "0000000",
  "message": "description",
  "requestId":"对方请求时传递过来的requestId",
  "data": {}
}
```

- 注：若有未知或待定字段，统一定为 null

---

### login

- 事件名称: login
- 事件方向: cobo/基金经理 -> ta
- 事件描述: cobo/基金经理登录认证
- 数据样例：

```json
{
  "requestId": "",
  "version": "0.0.1",
  "data": {
    "signTime": ,
    "apiKey": "",
    "signature": ""
  }
}
```

- 字段说明:

| 字段名称   |  类型  |                   说明                    |
| ---------- | :----: | :---------------------------------------: |
| requestId  | String |   请求流水 ID(UUID 生成唯一 id 传过来)    |
| version    | String |               api 接口版本                |
| signTime   |  Long  | 用于计算signature的时间戳，精确到毫秒     |
| apiKey     | String | API 访问账号，ta 生成给 cobo 或者基金经理 |
| signature  | String |         签名，签名算法如下详解。          |

注解:signature 生成算法
signature 使用 HMAC 进行签名计算
使用 HMAC 进行签名计算过程中需要的参数说明如下:
verb="AUTH" 常量
path="/api/v1/auth" 常量
signTime=1559182261328  时间戳，精确到毫秒
apiSecret="y1iLdwRxhTB1PgsqRtqHoDpOsNkCSDsu2hZPFwMyu12ZB6lzz5amg3WZtagZYo2v" 私下传递的密钥,TA提供。
signature = HEX(HMAC_SHA256(apiSecret,verb+path+str(signTime))


### login_response

- 事件名称: login_response
- 事件方向: ta -> 基金经理
- 事件描述: ta 认证后返回结果到 基金经理
- 数据样例：

```json
{
  "code": "000000",
  "message": "",
  "requestId": "",
  "data": {}
}
```

- 字段说明:

| 字段名称  |  类型  |          说明           |
| --------- | :----: | :---------------------: |
| code      | String | 返回错误码              |
| message   | String | 返回描述信息            |
| requestId | String | 请求时传递过来的流水 ID |

### reverse_auth

- 事件名称: reverse_auth
- 事件方向: ta -> 基金经理
- 事件描述: 基金经理反向认证 ta
- 数据样例：

```json
{
  "requestId": "",
  "version": "0.0.1",
  "data": {
    "signTime": ,
    "signature": ""
  }
}
```

- 字段说明:

| 字段名称   |  类型  |                 说明                 |
| ---------- | :----: | :----------------------------------: |
| requestId  | String | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version    | String |             api 接口版本             |
| signTime   |  Long  | 用于计算signature的时间戳，精确到毫秒     |
| signature  | String |       签名，签名算法如下详解。       |

注解:signature 生成算法
signature 使用 HMAC 进行签名计算
使用 HMAC 进行签名计算过程中需要的参数说明如下:
verb="AUTH" 常量
path="/api/v1/auth" 常量
signTime =45233245235 时间戳，精确到毫秒
apiSecret="c45ersxgsdf0-dgsdfghh35" 基金经理设置的密码的 md5 值
signature = HEX(HMAC_SHA256(apiSecret,verb+path+str(signTime))

### reverse_auth_response

- 事件名称: reverse_auth_response
- 事件方向: 基金经理 -> ta
- 事件描述: 基金经理反向认证结果返回给 ta
- 数据样例：

```json
{
  "code": "",
  "message": "",
  "requestId": "",
  "data": {}
}
```

- 字段说明:

| 字段名称  |  类型  |          说明           |
| --------- | :----: | :---------------------: |
| code      | String | 返回错误码              |
| message   | String | 返回描述信息            |
| requestId | String | 请求时传递过来的流水 ID |

### query_system_time

- 事件名称：query_system_time
- 事件方向：基金经理 -> ta
- 事件描述：获取ta服务器时间
- 数据样例：

```json
{
  "requestId": "sjr5tjs5xrctfyi34jsxdgejkxrey6xfy",
  "version": "0.0.1"
}
```

- 字段说明：

| 字段名称   |    类型    |                 说明                 |
| ---------- | :--------: | :----------------------------------: |
| requestId  |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version    |   String   |             api 接口版本             |


### query_system_time_response

- 事件名称：query_system_time_response
- 事件方向：ta -> 基金经理
- 事件描述：响应获取ta服务器时间
- 数据样例：

```json
{
  "code": "0000000",
  "message": "success",
  "requestId": "sjr5tjs5xrctfyi34jsxdgejkxrey6xfy",
  "data": {
      "dateTime":1558687514330
  }
    
}
```

- 字段说明:

| 字段名称  |  类型  |          说明           |
| --------- | :----: | :---------------------: |
| code      | String | 返回错误码              |
| message   | String | 返回描述信息            |
| requestId | String | 请求时传递过来的流水 ID |
| dateTime | Long    | 系统当前时间戳13位      |


### query_currency_info

- 事件名称：query_currency_info
- 事件方向：基金经理 -> ta
- 事件描述：查询币种与币种ID在ta系统内部的对应关系
- 数据样例：

```json
{
  "requestId": "sjr5tjs5xrctfyi34jsxdgejkxrey6xfy",
  "version": "0.0.1"
}
```

- 字段说明：

| 字段名称   |    类型    |                 说明                 |
| ---------- | :--------: | :----------------------------------: |
| requestId  |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version    |   String   |             api 接口版本             |


### query_currency_info_response
- 事件名称：query_currency_info
- 事件方向：ta -> 基金经理 
- 事件描述：响应查询币种与币种ID在ta系统内部的对应关系结果
- 数据样例

```json
{
  "code": "0000000",
  "message": "success",
  "requestId": "sjr5tjs5xrctfyi34jsxdgejkxrey6xfy",
  "data": {
    "counts":2,
    "details": [{
    "currencyId": 123,
    "symbol":"BTC"
    },{
    "currencyId": 124,
    "symbol":"USDT"
    }]
  }
}
```
- 字段说明:

| 字段名称  |  类型  |          说明           |
| --------- | :----: | :---------------------: |
| code      | String | 返回错误码              |
| message   | String | 返回描述信息            |
| requestId | String | 请求时传递过来的流水 ID |
| counts    | Integer| 币种映射数量            |
| currencyId| Integer| 币种ID                  |
| symbol    | String | 币种名称                |

### query_fund_composition

- 事件名称：query_fund_composition
- 事件方向：基金经理 -> ta
- 事件描述：查询基金的成分币组成信息和该基金所对应的计价币
- 数据样例：

```json
{
    "requestId": "asdghhsda",
	"version": "0.0.1",
	"data": {
	    "fundIds":[123,4576]
	}
}
```

- 字段说明

| 字段名称         |       类型 |                  说明                  |
| ---------------- | ---------: | :------------------------------------: |
| requestId        |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version          |   String   |             api 接口版本             |
| fundIds          |  List<Integer> | 查询基金fundId集合,当传递的值为空时,查询当前基金经理拥有的全部基金相应信息|


### query_fund_composition_response

- 事件名称：query_fund_composition_response
- 事件方向：ta -> 基金经理
- 事件描述：响应查询基金的成分币组成信息和该基金所对应的计价币的结果
- 数据样例：

```json
{
	"code": "000000",
	"message": "success",
	"requestId": "xxsdfgdfshsgsdhg",
	"data": [{
		"fundId": 11,
		"valuationCurrency": [12, 43],
		"fundComposition": [{
			"currencyId": 1,
			"weight": "2"
		}]
	}]
}
```
- 字段说明

| 字段名称         |       类型 |                  说明                  |
| ---------------- | ---------: | :------------------------------------: |
| code             | String     | 返回信息码                              |
| message          | String     | 返回结果描述信息                     |
| requestId        | String     | 请求流水 ID(UUID 生成唯一 id 传过来) |
| fundId           |Integer     |                基金 id                 |
| valuationCurrency|List<Integer>|     基金所对应的计价币id集合      |
| fundComposition  |    List    |                基金成分                |
| currencyId       |    Integer |                成分币 id                 |
| weight           |    String  |          一份基金该成分币所对应的数量          |

### subscribe_collective_order

- 事件名称：subscribe_collective_order
- 事件方向：ta -> 基金经理
- 事件描述：ta 定时发送 status 为 1 的普通订单集合给基金经理
- 数据样例：

```json
{
  "requestId": "asdfgd",
  "version": "0.0.1",
  "data": {
    "collectiveId": "qewwesdadsasddacxzvbipesajfgvailujr1",
    "orderCounts": 2,
    "orderList": [
      {
        "orderId": "dsahjdksahkj7xciucxii1",
        "fundId": 123456,
        "currencyId": 189728,
        "amount": 2,
        "price": 5,
        "side": 1,
        "placeTime": 1598287877411
      },
      {
        "orderId": "asduiuczxuiyu2klfjdzx",
        "fundId": 123456,
        "currencyId": 32667,
        "amount": 5,
        "price": 2,
        "side": -1,
        "placeTime": 159828783412
      }
    ]
  }
}
```

- 字段说明

| 字段名称     |    类型    |                 说明                 |
| ------------ | :--------: | :----------------------------------: |
| requestId    |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version      |   String   |             api 接口版本             |
| collectiveId |   String   |             集合订单 ID              |
|orderCounts   | Integer    |       订单的数量                     |
| orderList    |    List    |               订单集合               |
| orderId      |   String   |               订单 ID                |
| fundId       |  Integer   |               基金 ID                |
| currencyId   |  Integer   |              计价币 ID               |
| amount       |   String   |               基金份数               |
| price        |   String   |               基金报价               |
| side         |  Integer   |  申赎方向：1 表示申购，-1 表示赎回   |
| placeTime    |    Long    |            用户下单时间戳            |

### subscribe_collective_order_response

- 事件名称：subscribe_collective_order_response
- 事件方向：基金经理 -> ta
- 事件描述：基金经理成功收到 ta 传送的集合订单后,传送给 ta 的回执
- 数据样例：

```json
{
  "code": "000000",
  "message": "success",
  "requestId": "asdfgd",
  "data": {
    "collectiveId": "qewwesdadsasddacxzvbipesajfgvailujr1"
  }
}
```

- 字段说明

| 字段名称  |  类型  |                 说明                 |
| --------- | :----: | :----------------------------------: |
| code      | String | 返回状态码                           |
| message   | String | 返回描述信息                         |
| requestId | String | 请求流水 ID(UUID 生成唯一 id 传过来) |
| collectiveId |  String  | 基金经理收到的普通集合订单 ID   |

### collective_order_outcome

- 事件名称：collective_order_outcome
- 事件方向：基金经理 -> ta
- 事件描述：基金经理处理完集合订单,反馈给 ta 处理结果
- 数据样例：

```json
{
	"requestId": "qweuuuiijkmjhgsyuhx8892isjx7us21",
	"version": "0.0.1",
	"data": {
		"collectiveId": "26e447934c0141fb9f44e9c766b9538a",
		"orderCounts": 1,
		"completeOrderList": [{
          "orderId": "asdfnasdlfkjgbfiawlerojgvbipesajfgvailujr1",
          "fundId": 1,
          "amount": "2",
          "side": -1,
          "deliveryPrice": "189728",
          "currencyId": 1,
          "isSuccess": true,
          "reason": ""
        }]
	}
}
```

- 字段说明

| 字段名称      |    类型    |                 说明                 |
| ------------- | :--------: | :----------------------------------: |
| requestId     |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version       |   String   |             api 接口版本             |
| collectiveId  |   String   |             集合订单 ID              |
|orderCounts | Integer    |       订单的数量                     |
| orderId       |   String   |               订单 ID                |
| fundId        |  Integer   |               基金 ID                |
| amount        |   String   |               基金份数               |
| side          |  Integer   |  申赎方向：1 表示申购，-1 表示赎回   |
| deliveryPrice |   String   |                执行价                |
| currencyId    |  Integer   |                币种 ID             |
| isSuccess     |  Boolean   |             是否执行成功             |
| reason        |   String   |         非必填，执行失败原因         |



### collective_order_outcome_response

- 事件名称：collective_order_outcome_response
- 事件方向：ta -> 基金经理
- 事件描述：基金经理反馈给 ta 处理结果后,ta 发送给基金经理,表示已收到的回执
- 数据样例：

```json
{
  "code": "",
  "message": "",
  "requestId": "",
  "data": {
    "collectiveId": "93030976b20440a39ece581bd2779618"
  }
}
```
- 字段说明

| 字段名称      |    类型    |      说明       |
| --------- | :----: | :---------------------: |
| code      | String | 返回错误码              |
| message   | String | 返回描述信息            |
| requestId | String | 请求流水 ID(UUID 生成唯一 id 传过来) |
| collectiveId| String | 集合订单ID             |


### query_collective_order_status

- 事件名称：collective_order_status
- 事件方向：ta -> 基金经理
- 事件描述：查看基金经理处理集合订单的状态
- 数据样例：

```json
{
    "requestId": "qweuuuiijkmjhgsyuhx8892isjx7us21",
	"version": "0.0.1",
	"data": {
	    "collectiveId": "93030976b20440a39ece581bd2779618"
	}
}
```

- 字段说明

| 字段名称      |    类型    |      说明       |
| --------- | :----: | :---------------------: |
| requestId     |   String   | 请求流水 ID(UUID 生成唯一 id 传过来)  |
| version       |   String   |             api 接口版本              |
| collectiveId  |   String   | 订单集合号                            |


### query_collective_order_status_response

- 事件名称：query_collective_order_status_response
- 事件方向：基金经理 -> ta
- 事件描述：查看基金经理处理集合订单的状态
- 数据样例：

```json
{
  "code": "000000",
  "message": "success",
  "requestId": "asdfgd",
  "data": {
        "collectiveId": "26e447934c0141fb9f44e9c766b9538a",
        "orderCounts": 1,
        "completeOrderList": [{
          "orderId": "asdfnasdlfkjgbfiawlerojgvbipesajfgvailujr1",
          "fundId": 1,
          "amount": "2",
          "side": -1,
          "deliveryPrice": "189728",
          "currencyId": 1,
          "status": 4,
          "reason": ""
        }]
  }
}
```

- 字段说明

| 字段名称      |    类型    |                 说明                 |
| ------------- | :--------: | :----------------------------------: |
| code          | String     | 返回信息码                           |
| message       | String     | 返回结果描述信息                     |
| requestId     | String     | 请求流水 ID(UUID 生成唯一 id 传过来) |
| collectiveId  |  String   |             集合订单 ID              |
| orderCounts   | Integer    |       订单的数量                     |
| orderId       |  String   |               订单 ID                |
| fundId        |  Integer   |               基金 ID                |
| amount        |  String   |               基金份数               |
| side          |  Integer   |  申赎方向：1 表示申购，-1 表示赎回   |
| deliveryPrice |  String   |                执行价                |
| currencyId    |  Integer   |                币种 ID             |
| status        |  Integer   |   订单状态，3表示正在执行, 4表示执行成功，6表示执行失败  |
| reason        |  String   |         非必填，执行失败原因         |


### fund_quote_ta

- 事件名称：fund_quote_ta
- 事件方向：基金经理 -> ta
- 事件描述：基金经理推送给 ta 基金行情
- 数据样例：

```json
{
  "requestId": "asddas",
  "version": "0.0.1",
  "data": [
    {
      "fundId": 123,
      "currencyId": 1,
      "bids": ["2.5"],
      "asks": ["2.6"],
      "purchaseBalance": ["1.2"],
      "redemptionBalance": ["2.3"],
      "netValue": "2.6",
      "timestamp": 1558344117579
    }
  ]
}
```

- 字段说明

| 字段名称          |       类型       |     说明     |
| ----------------- | :--------------: | :----------: |
| requestId     |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version       |   String   |             api 接口版本             |
| fundId            |     Integer      |   基金 ID    |
| currencyId        |     Integer      |   币种 ID    |
| bid               |   List<String>   |    买入价    |
| ask               |   List<String>   |    卖出价    |
| purchaseBalance   |   List<String>   | 申购盘口余额 |
| redemptionBalance |   List<String>   | 赎回盘口余额 |
| netValue          |      String      |     净值     |
| timestamp         |   Long           |  推送时间    |

- 备注：asks bids purchaseBalance redemptionBalance 档位从左向右由小往大



### fund_quote_ta_response

- 事件名称：fund_quote_ta_response
- 事件方向：ta -> 基金经理
- 事件描述：基金经理推送给 ta 基金行情后,ta返回给基金经理的响应
- 数据样例：

```json
{
  "code": "0000000",
  "message": "success",
  "requestId": "xxsdfgdfshsgsdhg"
}
```

- 字段说明

| 字段名称          |       类型       |     说明     |
| ----------------- | :--------------: | :----------: |
| code      | String  | 返回信息码                           |
| message   | String  | 返回结果描述信息                     |
| requestId | String  | 请求流水 ID(UUID 生成唯一 id 传过来) |


### subscribe_fund_info

- 事件名称：subscribe_fund_info
- 事件方向：ta -> 基金经理
- 事件描述：ta 发给 基金经理 所有基金的基本信息
- 数据样例：

```json
{
	"requestId": "asdghhsda",
	"version": "0.0.1",
	"data": [{
		"fundId": 11,
		"name": "DEC",
		"type": 1,
		"isPurchase": 1,
		"isRedemption": 0,
		"baseMeasurementUnit": "0.1000000000",
		"minTradeAmount": "5.5",
		"maxTradeAmount": "22",
		"purchaseRate": "1.1",
		"redemptionRate": "1.1",
		"holdingRate": "1.1",
		"manageFeeCurrencyId": 12,
		"minWholesaleRedemptionCash": "1",
		"maxWholesaleRedemptionCash": "2",
		"wholesale": [{
			"currencyId": 1,
			"minWholesalePurchaseCash": "2",
			"maxWholesalePurchaseCash": "2",
			"purchaseRateWholesale": "2",
			"redemptionRateWholesale": "2"
		}]
	}]
}
```

- 字段说明

| 字段名称         |       类型 |                  说明                  |
| ---------------- | ---------: | :------------------------------------: |
| requestId        |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version          |   String   |             api 接口版本             |
| fundId           |    Integer |                基金 id                 |
| name             |     String |                基金名称                |
| type             |    Integer |    基金类型，0 表示 ETF，1 表示其他    |
| isPurchase       |    Integer | 是否允许申购，0 表示可以，1 表示不可以 |
| isRedemption     |    Integer | 是否允许赎回,0 表示可以，1 表示不可以  |
| baseMeasurementUnit|    String |      基本计量单位                     |
| minTradeAmount   |    String  |               最小下单量               |
| maxTradeAmount   |    String  |               最大下单量               |
| purchaseRate     |    String  |                申购费率                |
| redemptionRate   |    String  |                赎回费率                |
| holdingRate      |    String  |              基金管理费率              |
| manageFeeCurrencyId     |    String  |                管理费币种id                |
| minWholesaleRedemptionCash   |    String  |                大额赎回最小赎回基金份额                |
| maxWholesaleRedemptionCash      |    String  |              大额赎回最大赎回基金份额              |
| currencyId       |    Integer |                币种 id                 |
| minWholesalePurchaseCash     |    String  |                大额申购最小申购金额                |
| maxWholesalePurchaseCash   |    String  |                大额申购最大申购金额                |
| purchaseRateWholesale      |    String  |              大额申购费率              |
| redemptionRateWholesale       |    Integer |                大额赎回费率                |

### query_fund_info

- 事件名称：query_fund_info
- 事件方向：基金经理 -> ta
- 事件描述：基金经理查询基金的基本信息
- 数据样例：

```json
{
    "requestId": "asdghhsda",
	"version": "0.0.1",
	"data": {
	    "fundIds":[123,4576]
	}
}
```

- 字段说明

| 字段名称         |       类型 |                  说明                  |
| ---------------- | ---------: | :------------------------------------: |
| requestId        |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version          |   String   |             api 接口版本             |
| fundIds          |  List<Integer> | 查询基金fundId集合,当传递的值为空时,查询当前基金经理拥有的全部基金信息|


### query_fund_info_response

- 事件名称：query_fund_info_response
- 事件方向：ta -> 基金经理
- 事件描述：响应基金经理查询基金的基本信息结果
- 数据样例：

```json
{
    "code": "000000",
    "message": "success",
    "requestId": "xxsdfgdfshsgsdhg",
    "data": [
    {
        "fundId": 11,
		"name": "DEC",
		"type": 1,
		"isPurchase": 1,
		"isRedemption": 0,
		"baseMeasurementUnit": "0.1000000000",
		"minTradeAmount": "5.5",
		"maxTradeAmount": "22",
		"purchaseRate": "1.1",
		"redemptionRate": "1.1",
		"holdingRate": "1.1",
		"manageFeeCurrencyId": 12,
		"minWholesaleRedemptionCash": "1",
		"maxWholesaleRedemptionCash": "2",
		"wholesale": [{
			"currencyId": 1,
			"minWholesalePurchaseCash": "2",
			"maxWholesalePurchaseCash": "2",
			"purchaseRateWholesale": "2",
			"redemptionRateWholesale": "2"
		}]
    },
    {
        "fundId": 12,
		"name": "DEC",
		"type": 1,
		"isPurchase": 1,
		"isRedemption": 0,
		"baseMeasurementUnit": "0.1000000000",
		"minTradeAmount": "5.5",
		"maxTradeAmount": "22",
		"purchaseRate": "1.1",
		"redemptionRate": "1.1",
		"holdingRate": "1.1",
		"manageFeeCurrencyId": 12,
		"minWholesaleRedemptionCash": "1",
		"maxWholesaleRedemptionCash": "2",
		"wholesale": [{
			"currencyId": 1,
			"minWholesalePurchaseCash": "2",
			"maxWholesalePurchaseCash": "2",
			"purchaseRateWholesale": "2",
			"redemptionRateWholesale": "2"
		}]
    }
    ]
}
```
- 字段说明

| 字段名称         |       类型 |                  说明                  |
| ---------------- | ---------: | :------------------------------------: |
| code             | String     | 返回信息码                              |
| message          | String     | 返回结果描述信息                     |
| requestId        | String     | 请求流水 ID(UUID 生成唯一 id 传过来) |
| fundId           |    Integer |                基金 id                 |
| name             |     String |                基金名称                |
| type             |    Integer |    基金类型，0 表示 ETF，1 表示其他    |
| isPurchase       |    Integer | 是否允许申购，0 表示可以，1 表示不可以 |
| isRedemption     |    Integer | 是否允许赎回,0 表示可以，1 表示不可以  |
| baseMeasurementUnit|    String |      基本计量单位                     |
| minTradeAmount   |    String  |               最小下单量               |
| maxTradeAmount   |    String  |               最大下单量               |
| purchaseRate     |    String  |                申购费率                |
| redemptionRate   |    String  |                赎回费率                |
| holdingRate      |    String  |              基金管理费率              |
| manageFeeCurrencyId     |    String  |                管理费币种id                |
| minWholesaleRedemptionCash   |    String  |                大额赎回最小赎回基金份额                |
| maxWholesaleRedemptionCash      |    String  |              大额赎回最大赎回基金份额              |
| currencyId       |    Integer |                币种 id                 |
| minWholesalePurchaseCash     |    String  |                大额申购最小申购金额                |
| maxWholesalePurchaseCash   |    String  |                大额申购最大申购金额                |
| purchaseRateWholesale      |    String  |              大额申购费率              |
| redemptionRateWholesale       |    Integer |                大额赎回费率                |



### subscribe_message （意外情况备用接口）

- 事件名称：subscribe_message
- 事件方向：基金经理 -> ta
- 事件描述：基金经理特殊情况报警
- 数据样例：

```json
{
	"requestId": "",
	"version":"",
	"data": {
	  "text": ""
	}
}
```

- 字段说明

| 字段名称  |  类型  |       说明       |
| --------- | :----: | :--------------: |
| requestId | String |     请求 ID      |
| version    | String |    api 接口版本|
| text      | String | 具体报警内容文本 |

- 无响应提示

### subscribe_wholesale_order

- 事件名称：subscribe_wholesale_order
- 事件方向：ta -> 基金经理
- 事件描述：发送大额申购赎回的订单给基金经理
- 数据样例：

```json
{
	"requestId": "sjr5tjs5xrctfyi34jsxdgejkxrey6xfy",
	"version": "0.0.1",
	"data": {
		"collectiveId": "aasfsfxvcjjxvca",
		"fundId": 12456,
		"placeTime": 158723478,
		"orderCounts": 11,
		"orderList": [{
			"orderId": "93030976b20440a39ece581bd2779618",
			"currencyId": 1,
			"currencyAmount": 1,
			"amount": 1,
			"side": 1
		}]
	}
}
```

- 字段说明

| 字段名称   |    类型    |                 说明                 |
| ---------- | :--------: | :----------------------------------: |
| requestId  |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version    |   String   |             api 接口版本             |
| collectiveId |   String   |             集合订单 ID              |
| fundId     |  Integer   |             基金产品 ID              |
| placeTime  |  Long      |            用户下单时间戳            |
|orderCounts | Integer    |       订单的数量                     |
| orderId    |   String   |       订单id       |
| currencyId |  Integer   |              计价币 id               |
| currencyAmount |  String    |      申购计价币数量 (申购使用字段) |
| amount     |  String    |            基金份数(赎回使用字段)      |
| side       |  Integer   |  申赎方向：1 表示申购，-1 表示赎回   |

### subscribe_wholesale_order_response

- 事件名称：subscribe_wholesale_order_response
- 事件方向：基金经理 -> ta
- 事件描述：基金经理成功收到 ta 传送的大额订单后,传送给 ta 的回执
- 数据样例：

```json
{
  "code": "000000",
  "message": "success",
  "requestId": "sjr5tjs5xrctfyi34jsxdgejkxrey6xfy",
  "data": {
    "collectiveId": "qewwesdadsasddacxzvbipesajfgvailujr1"
  }
}
```

- 字段说明

| 字段名称  |  类型  |                 说明                 |
| --------- | :----: | :----------------------------------: |
| code      | String | 返回错误码                           |
| message   | String | 返回描述信息                         |
| requestId | String | 请求流水 ID(UUID 生成唯一 id 传过来) |
| collectiveId |   String   |             集合订单 ID      |

### wholesale_order_outcome

- 事件名称：wholesale_order_outcome
- 事件方向：基金经理 -> ta
- 事件描述：基金经理处理完大额订单,反馈给 ta 处理结果
- 数据样例：

```json
{
	"requestId": "qwew1232733218",
	"version": "0.0.1",
	"data": {
		"collectiveId": "qewwesdadsasddacxzvbipesajfgvailujr1",
		"fundId": 123,
		"orderCounts": 11,
		"completeOrderList": [{
			"orderId": "asdfnasdlfkjgbfiawlerojgvbipesajfgvailujr1",
			"side": -1,
			"deliveryPrice": "189728",
			"currencyId": 1,
			"succeededAmount": "1",
			"wholesaleExcess": "2.1",
			"reason": "reason"
		}]
	}
}
```

- 字段说明

| 字段名称      |    类型    |                 说明                 |
| ------------- | :--------: | :----------------------------------: |
| requestId     |   String   | 请求流水 ID(UUID 生成唯一 id 传过来) |
| version       |   String   |             api 接口版本             |
| collectiveId |   String   |             集合订单 ID      |
| orderId       |   String   |               订单 ID                |
| fundId        |  Integer   |               基金 ID                |
|orderCounts    | Integer    |       订单的数量                     |
| side          |  Integer   |  申赎方向：1 表示申购，-1 表示赎回   |
| deliveryPrice |   String   |                执行价                |
| currencyId    |  Integer   |                币种 ID             |
| succeededAmount     |  String   |             执行成功份数        |
| wholesaleExcess        |   String   |         大额订单执行结余       |


### wholesale_order_outcome_response

- 事件名称：wholesale_order_outcome_response
- 事件方向：ta -> 基金经理
- 事件描述：基金经理反馈给 ta 大额订单处理结果后,ta 发送给基金经理,表示已收到的回执
- 数据样例：

```json
{
  "code": "",
  "message": "",
  "requestId": "",
  "data": {
    "collectiveId": "93030976b20440a39ece581bd2779618"
  }
}
```
- 字段说明

| 字段名称      |    类型    |      说明       |
| --------- | :----: | :---------------------: |
| code      | String | 返回错误码              |
| message   | String | 返回描述信息            |
| requestId | String | 请求流水 ID(UUID 生成唯一 id 传过来) |
| collectiveId| String | 集合订单ID             |



## 错误信息和错误码

| 错误信息                  |                                   描述 | 错误码 |
| ------------------------- | -------------------------------------: | :----: |
| success                   |                             成功所返回 | 000000 |
| data not ready            |                         数据没有准备好 | 010001 |
| wrong parameter           |                           传入参数错误 | 010002 |
| Timestamp request expired |                         请求时间戳过期 | 010003 |
| Invalid sign              |                               签名无效 | 010004 |
| Requested too frequent    | 用户请求频率过快，超过该接口允许的限额 | 010005 |
| Internal system error     |                           系统内部错误 | 010006 |
| User not logged in        |                           用户需要登录 | 010007 |
| request id empty                   |                             requestid为空 | 010008 |
| collective double send            |                         集合订单重复发生或无效 | 020001 |
| collective id empty           |                           集合订单id为空 | 020008 |
| double send |                         重复传入 | 040001 |
| param less              |                               参数缺失 | 040002 |
| not allow    | 用户请求频率过快，不允许申购赎回 | 040003 |
| not multiple     |                           交易数量不为交易单位的整数倍 | 040004 |
| not enough balance        |                           交易数量大于对应档次的盘口余额 | 040005 |
| over num                   |                             交易数量大于最大数量限制 | 040006 |
| less num            |                         交易数量小于最小数量限制 | 040007 |
| over locked num           |                           申购赎回数量大于未冻结资产 | 040008 |
| other wrong |                         未知错误 | 040009 |
| wholesale check              |                               大额校验错误 | 042001 |
| wholesale wrong type    | 订单类型不符合要求 | 042002 |
| wholesale order mix type     |                           集合订单里面同时包含了申购和赎回 | 042003 |
| wholesale order currence amount too big        |                           集合订单总额大于最大总额数 | 042004 |
| wholesale order currence amount too small           |                           集合订单总额小于最小总额数 | 042005 |
| wholesale order amount too big |                         集合订单赎回总份数大于最大总份数数 | 042006 |
| wholesale order amount too small              |                               集合订单赎回总份数小于最小总份数 | 042007 |
| wholesale order amount times error    | 集合订单出现订单非基本单位的整数倍情况 | 042008 |
| wholesale order user account not fount     |                           赎回时，有用户基金账号不存在 | 042009 |
| wholesale order amount more than own        |                           赎回时，订单赎回份额比持有份额要多 | 042010 |