#### 通用字段定义

| 字段  | 含义                                               |
| ----- | -------------------------------------------------- |
| op    | 事件主题                                           |
| args  | 传送信息内容                                       |
| info  | 成功或失败原因                                     |
| topic | 订阅数据类型（目前有index_data, index_data_type2） |
| id    | 币种id                                             |
| code  | 信息码                                             |

#### 登录

* 登录方式：

    登录网址 ws://{ip}:{port}/websocket
    * 发送登录

    ```json
    {
      "op": "login",
      "args": {
        "signTime": ,
        "apiKey": "",
        "signature": ""
      }
    }
    ```

    * 字段说明:

    | 字段名称  |  类型  |                    说明                     |
    | --------- | :----: | :-----------------------------------------: |
    | signTime  |  Long  | 用于计算signature的时间戳，十位长度精确到秒 |
    | apiKey    | String |       API 访问账号，由我们生成给用户        |
    | apiSecret | String |       API 访问密码，由我们生成给用户        |
    | signature | String |           签名，签名算法如下详解            |

    注：signature 生成算法：

    signature 使用 HmacSHA256 进行签名计算，

    需要的参数说明如下:

    * 加密的原始信息应为： "blockchain" + {apiKey1} + signTime
    * 私钥为apiSecret
    * signTime与服务器时间相差前后五分钟内有效

* 登录返回信息
* 登录成功

```json
{
    "op": "loginResponse",
    "args": {
        "info": "success",
        "code": 2001
    }
}
```
* 登录失败

```json
{
    "op": "loginResponse",
    "args": {
        "info": "login error",
        "code": 2012
    }
}
```

#### 登出

* 登出方式：

    * 发送登出

    ```json
    {
      "op": "logout",
      "args": {}
    }
    ```

* 登出返回信息

    ```json
    {
     "op":"logoutResponse",
     "args":{
         "code":2001,
         "info":"success"
     }
    }
    ```

#### 订阅

* 发送订阅

    ```json
    {
      "op": "subscribe",
      "args": {
          "topic": "index_data",
          "id": "1"
      }
    }
    ```
* 订阅返回信息
    * 订阅成功

    ```json
    {
        "op": "subscribeResponse",
        "args": {
            "topic": "index_data",
            "id": "1",
            "info": "success",
            "code": 2001
        }
    
    }
    ```

    * 订阅失败（info不为success，原因多种多样）

    ```json
    {
      "op": "subscribeResponse",
      "args": {
          "topic": "index_data",
          "id": "1",
          "info": "already subscribed",
          "code": 3005
      }
    
    }
    ```

#### 取消订阅

* 发送取消订阅

    ```json
    {
      "op": "unsubscribe",
      "args": {
          "topic": "index_data",
          "id": "1"
      }
    
    }
    ```

* 取消订阅返回信息
    * 取消订阅成功

    ```json
    {
      "op": "unsubscribeResponse",
      "args": {
          "topic": "index_data",
          "id": "1",
          "info": "success",
          "code": 2001
      }
    
    }
    ```

    * 取消订阅失败（info不为success，原因多种多样）

    ```json
    {
      "op": "unsubscribeResponse",
      "args": {
          "topic": "index_data",
          "id": "1",
          "info": "coin not subscribed",
          "code": 3008
      }
    
    }
    ```

* coin_index

    * 信息样例

    ```json
    {
      "op": "coin_index",
      "args": {
        "cid":0,
        "symbol":"BTC",
        "cmcSymbol":"bitcoin",
        "latest":"7997.374999932528",
        "updateTime":1558863246
      }
    }
    ```

    | 字段名称   |  类型   |              说明               |
    | ---------- | :-----: | :-----------------------------: |
    | cid        | Integer |    币种id（对应订阅时的id）     |
    | symbol     | String  |         该币种的symbol          |
    | cmcSymbol  | String  | 该币种在coinmarketcap上的symbol |
    | latest     | String  |          该币种最新价           |
    | updateTime |  Long   |            更新时间             |


* pair_index

    * 信息样例

    ```json
    {
      "op": "pair_index",
      "args":{
        "symbol":"BNB",
        "cmcSymbol":"binance-coin",
        "latest":"0.3745",
        "updateTime":1558863261785,
        "cid":18,
        "exchangeInfos":[
            {
                "market":"Gate.io",
                "pair":"ICX_USDT",
                "price":"0.3727",
                "timestamp":1558858217214
            },{
                "market":"OKEx",
                "pair":"ICX_USDT",
                "price":"0.3751",
                "timestamp":1558863255151
            },{
                "market":"Binance",
                "pair":"ICX_USDT",
                "price":"0.3757",
                "timestamp":1558863246025
            }
        ]
        }
    }
    ```

    | 字段名称   |  类型   |              说明               |
    | ---------- | :-----: | :-----------------------------: |
    | symbol     | String  |         该币种的symbol          |
    | cmcSymbol  | String  | 该币种在coinmarketcap上的symbol |
    | latest     | String  |          该币种最新价           |
    | updateTime |  Long   |            更新时间             |
    | cid        | Integer |    币种id（对应订阅时的id）     |
    | market     | String  |           交易所名称            |
    | pair       | String  |             交易对              |
    | price      | String  |             成交价              |
    | timestamp  |  Long   |             时间戳              |

* index

    * 信息样例

    ```json
    {
      "op": "index",
      "args":{
        "indexId":11,
        "lastPrice":"733.5075872479424850213940004",
        "marketCap":"205470844554.610094",
        "turnover24h":"55105586667.50589",
        "updateTime":1559285819
      }
    }
    ```

    | 字段名称    |  类型   |              说明               |
    | ----------- | :-----: | :-----------------------------: |
    | indexId     | Integer |    币种id（对应订阅时的id）     |
    | lastPrice   | String  |         该币种的symbol          |
    | marketCap   | String  | 该币种在coinmarketcap上的symbol |
    | turnover24h | String  |          该币种最新价           |
    | updateTime  |  Long   |            更新时间             |

### code信息码

* 返回信息

| code | 事件                     | 提示文本                                                    |
| ---- | ------------------------ | ----------------------------------------------------------- |
| 2001 | 成功                     | success                                                     |
| 2002 | 参数错误                 | wrong param                                                 |
| 2003 | 密码错误                 | wrong password                                              |
| 2004 | 重复登陆                 | double login                                                |
| 2005 | 权限错误，请联系chainext | unauthorized access, please contact ChaiNext for permission |
| 2006 | 登出成功                 | logout success                                              |
| 2009 | 数据转换出错             | data transfer error                                         |
| 2010 | 登录状态出错，请重新登陆 | login status error, please login again                      |
| 2011 | 未知错误                 | unknown error                                               |
| 2013 | 用户不存在               | user absent                                                 |

* 事件事务

| code | 事件                         | 提示文本             |
| ---- | ---------------------------- | -------------------- |
| 3001 | 事件不存在                   | event absent         |
| 3002 | 订阅成功                     | success              |
| 3004 | 取消订阅成功                 | unsubscribe success  |
| 3005 | 重复订阅                     | already subscribed   |
| 3006 | 主题不存在                   | topic absent         |
| 3007 | 币种不存在                   | coin absent          |
| 3008 | 尚未订阅该币种，无法取消订阅 | coin not subscribed  |
| 3009 | 尚未订阅该指数，无法取消订阅 | index not subscribed |
| 3010 | 指数不存在                   | index absent         |
