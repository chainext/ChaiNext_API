# ChaiNext API Instruction
Instruction for ChaiNext API use.
## ChaiNext API Introduction
ChaiNext provided a series of API, in order to help users obtain market information in real time.

Currently, ChaiNext API provide following functions:
* get basic information, market quotations and details of CSI indices
* get coin weight coefficient of CSI indices
* get candlestick chart of CSI indices
* get mapping list between CSI indices' CID and their names
* get mapping list between coins' CID and their names
* get daily broadcast of CSI indices
* get hourly broadcast of CSI indices
* get minute performance monitor information of CSI indices
* get hour performance monitor information of CSI indices
* get coin transfer alert information

API access basic address:

users in China: [https://api.chainext.cn/v1](https://api.chainext.io/v1)

otherwise: [https://api.chainext.io/v1](https://api.chainext.io/v1)

## API Detailed Instruction 
| Data Type | Method | type     | Description  |
| ----- | --- | ------ | ----- |
|Basic indices market information|[https://api.chainext.io/v1/index_basic](#基本指数行情--get-index_basic-获取基本指数行情)|GET|Get basic market information of indices|
|Weight|[https://api.chainext.io/v1/weight](#指数权重信息--get-weight-获取指数的权重信息)|GET|Get weight coefficient of coins in indices|
|Index list|[https://api.chainext.io/v1/index_list](#指数列表信息--get-index_list-获取指数列表信息)|GET|get index list|
|Index performance|[https://api.chainext.io/v1/index_detail](#指数表现相关信息--get-index_detail-获取指数表现相关信息)|GET|Get index performance under stated period of time|
|Candlestick chart|[https://api.chainext.io/v1/kchart](#指数k线图--get-kchart-获取指数k线图)|GET|get candlestick chart of CSI indices|
|Mapping list|[https://api.chainext.io/v1/mapping_list](#单币cid与指数名称对应表--get-coin_mapping_list-获取单币cid与单币名称的相关说明)|GET|Get mapping list between CSI indices' CID and their names|
|Coin mapping list|[https://api.chainext.io/v1/coin_mapping_list](#单币cid与指数名称对应表--get-coin_mapping_list-获取单币cid与单币名称的相关说明)|GET|Get mapping list between coins' CID and their names|
|Daily broadcast|[https://api.chainext.io/v1/wechat_broadcast](#指数收盘utc24播报信息--get-wechat_broadcast-获取每日指数收盘播报信息)|GET|Get daily broadcast of CSI indices|
|Hourly broadcast|[https://api.chainext.io/v1/wechat_hour_broadcast](#指数每小时行情播报信息--get-wechat_hour_broadcast-获取整点播报信息)|GET|get hourly broadcast of CSI indices|
|Minute performance monitor information|[https://api.chainext.io/v1/wechat_monitor_min](#指数快速涨跌异动报警信息--get-wechat_monitor_min-获取指数指数快速涨跌异动报警信息)|GET|get minute performance monitor information of CSI indices|
|Hour performance monitor information|[https://api.chainext.io/v1/wechat_monitor_24h](#指数大幅涨跌报警信息--get-wechat_monitor_24h-以utc0时间为基准获取当日的csi指数涨跌幅报警信息)|GET|get hour performance monitor information of CSI indices|
|Coin transfer alert information|[https://api.chainext.io/v1/largement_alert](#代币大额转账报警信息--get-largement_alert-获取代币大额转账报警信息)|GET|get coin transfer alert information|


### 基本指数行情 <span id="v1/index_basic"> GET /index_basic 获取基本指数行情
Request parameters: 

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | string | index CID or index name  | 1 |      |

Response: 

| Name   | Required | Type   | Description   | Range   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |basic index performance data|      |
| updated_time| true | string |data update time|      |

API access example：https://api.chainext.io/v1/index_basic?id=1

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": [
    {
      "abstract": "",
      "download": [
        {
          "name": "编制方案",
          "url": "https://chainext.oss-cn-hongkong.aliyuncs.com/doc/20180626/BZFA.pdf"
        }
      ],
      "related": {
        "name": "ChaiNext大盘规模指数NoBTC",
        "num": 9
      },
      "latest": {
        "lastprice": 983.148788642376,
        "changes": -4.1037298652643495,
        "turnover_24h": 10383149795,
        "earn": -21.902059818540533,
        "marketcap": -42.06200000000001,
        "change_abs": -42.06200000000001
      }
    }
  ],
  "updated_time": 1530690774.3714838
}
```



## 指数权重信息 <span id="v1/weight"> GET /weight 获取指数的权重信息
Request parameters: 

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | string | index CID or index name  | 1 | |

Response: 

| Name | Required  | Type     | Description  |  Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |index weight data|      |
| updated_time| true | string |data update time|      |

API access example：https://api.chainext.io/v1/weight?id=csi100

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": [
      {
        "name": "litecoin",
        "weight": 0.05078488649366153
      },
      {
        "name": "digitalnote",
        "weight": 0.00015166115754669315
      }, ...
  ]
}
```






## 指数列表信息 <span id="v1/index_list"> GET /index_list 获取指数列表信息
Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| page       | true  | integer | page | 1 | |
| page_size       | true  | integer | page size  | 20 | |

Response:

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |index list data|      |
| updated_time| true | string |data update time|      |

API access example：https://api.chainext.io/v1/index_list?page=1&page_size=20

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": {
    "total": 20,
    "current_page": 1,
    "data": [
              {
                "symbol": "csi10X",
                "id": "csi10X",
                "full_name_en": "ChaiNext Large Cap index no BTC",
                "full_name_zh": "ChaiNext大盘规模指数NoBTC",
                "24h_max": 4986.09,
                "24h_min": 4554.08,
                "latest": 4581.11,
                "change": -3.9420954984864633,
                "change_abs": -40.37099999999987,
                "turnover": 5167595300,
                "component_num": 100,
                "marketcap": 246780275125.75586,
                "price7": [
                  1116.12,
                  1119.31,
                  ...
                ],
                "hot": 10000
              }
            ]
          }
        }
```


## 指数表现相关信息 <span id="v1/index_detail"> GET /index_detail 获取指数表现相关信息

Request parameters: 

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | integer | index CID | 1 | |
| tstart       | true  | integer | start time | |Unix timestamp（e.g. 1520691531）|
| tend       | true  | integer | end time | |Unix timestamp（e.g. 1530691531）|

Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |index performance data|      |

API access example：https://api.chainext.io/v1/index_detail?id=1&tstart=1520091531&tend=1530687931

Response example: 
```
  {
  "code": 0,
  "msg": "string",
  "data": {
    "value": [
        [
          1520121600,
          8432.70780551296
        ],
        [
          1520208000,
          8721.81691492141
        ],
    ]
  }
}
```




## 指数K线图 <span id="v1/kchart"> GET /kchart 获取指数K线图

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | integer | index CID | 1 | |
| tstart       | true  | integer | start time | |Unix timestamp（e.g. 1520691531）|
| tend       | true  | integer | end time | |Unix timestamp（e.g. 1530691531）|
| grouping       | true  | string | time grouping method | |1min, 5min,15min, 30min, 1H, 4h, 6h, 12h, 1D, 1w, 1m|

Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |index candlestick chart data|      |

API access example：https://api.chainext.io/v1/kchart?id=4&grouping=1H&tstart=1526798662&tend=1531983011

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": {
    "success": true,
    "lines": [
      [
        "1529093700000, 0.075646, 0.076141, 0.075646, 0.076035, 356.9439"
      ],  # 数据分别为unix时间戳，开盘价，收盘价，最高价，最低价，交易额    
      ...
    ]
  }
}
```

## 指数CID与指数名称对应表 <span id="v1/mapping_list"> GET /mapping_list 获取指数CID与指数名称的相关说明

Request parameters:

None.

Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |index CID and index name|      |

API access example：https://api.chainext.io/v1/mapping_list

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": {
    "CID": {
      "index_CID": 1,
      "index_code": "csi10X",
      "index_name_ch": "ChaiNext大盘规模指数NoBTC"
    }
  }
```



## 单币CID与指数名称对应表 <span id="v1/coin_mapping_list"> GET /coin_mapping_list 获取单币CID与单币名称的相关说明

Request parameters:

None.

Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |coin CID and index name|      |

API access example：https://api.chainext.io/v1/coin_mapping_list

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": {
    "CID": {
      "CID": 0,
      "symbol": "BTC",
      "is_effective": 1 #是否提供报警信息
    }
  }
```



## 指数收盘（UTC24）播报信息 <span id="v1/wechat_broadcast"> GET /wechat_broadcast 获取每日指数收盘播报信息

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| date      | true  | string | query date, e.g. 2018-07-24 | ||


Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |daily broadcast |      |

API access example：https://api.chainext.io/v1/wechat_broadcast?date=2018-08-02

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": [
    {
      "total": 2,
      "current_page": 1,
      "data": {
        "time": "2018-07-21 07:59:37",
        "content": "CSI指数收盘播报\r\n\r\n北京时间2018年08月02日07时59分\r\n\r\n「CSI100」指数报1013.96点,全日涨跌幅为-1.31%。成分币中14上涨，86下跌。涨幅居前为「PPT」(14.19%)、「XMR」(4.91%)、「DOGE」(3.41%)。\r\n\r\n「CSI21-100」指数报6986.63点,全日涨跌幅为-2.19%。成分币中11上涨，69下跌。涨幅居前为「PPT」(14.19%)、「DOGE」(3.41%)、「INK」(2.88%)。\r\n\r\n「CSI5」指数报800.43点,全日涨跌幅为-1.28%。成分币中1上涨，4下跌。涨幅居前为「XRP」(2.77%)。\r\n\r\n「CSI6-20」指数报5160.35点,全日涨跌幅为-1.08%。成分币中2上涨，13下跌。涨幅居前为「XMR」(4.91%)、「DASH」(0.47%)。\r\n\r\n「CSI」指数系列：ChaiNext规模指数（ChaiNext Scale Index，以下简称CSI指数）是由ChaiNext团队按照规模、流动性和可投资性综合排名情况编制的通证市场系列指数，包含13条覆盖不同市值区间的指数，是市场上代表性最强的指数。\r\n\r\n\r\n本信息由企业级数字货币指数服务商ChaiNext提供。\r\nhttps://chainext.io|微信公众号ChaiNext"
      }
    }
  ]
}
```




## 指数每小时行情播报信息 <span id="v1/wechat_hour_broadcast"> GET /wechat_hour_broadcast 获取整点播报信息

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | index CID or index name | ||
| date      | true  | string | query date, e.g. 2018-07-24 | ||


Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |hourly broadcast |      |

API access example：https://api.chainext.io/v1/wechat_hour_broadcast?id=11&date=2018-08-02

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": [
    {
      "total": 100,
      "data": [
        {
        "time": "2018-08-02 10:00:26",
        "content": 	"指数点位整点播报 北京时间2018年08月02日10:00，「CSI100」指数报1020.38点,全日涨跌幅为0.84%。成分币中77上涨，23下跌。涨幅居前为「WTC」(19.97%)、「PAY」(9.49%)、「ARDR」(5.51%)。\r\n\r\n「CSI100」：CSI系列指数中的\"上证综指\"，样本由规模和流动性排名前100的通证组成，市值覆盖率达96%，反映了通证市场整体走势。\r\n本信息由企业级数字货币指数服务商ChaiNext提供。\r\nhttps://chainext.io|微信公众号ChaiNext"
        }
      ]
    }
  ]
}
```



## 指数快速涨跌异动报警信息 <span id="v1/wechat_monitor_min"> GET /wechat_monitor_min 获取指数指数快速涨跌异动报警信息

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | index CID or index name | ||
| date      | true  | string | query date, e.g. 2018-07-24 | ||


Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |minute monitor information |      |

API access example：https://api.chainext.io/v1/wechat_monitor_min?id=csi100&date=2018-08-02

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": [
    {
      "total": 100,
      "data": [
        {
        "time": "2018-08-02 10:00:26",
        "content": 	"CSI指数快速波动预警\r\n2018年08月02日06时09分-06时19分,CSI100指数10min快速上涨1.22%,目前报1005.17点。\r\n成分币中8上涨，92下跌。涨幅居前为「PPT」(9.45%)、「BCD」(3.84%)、「DOGE」(2.30%)。\r\n\r\n「CSI100」：CSI系列指数中的\"上证综指\"，样本由规模和流动性排名前100的通证组成，市值覆盖率达96%，反映了通证市场整体走势。\r\n\r\n本信息由企业级数字货币指数服务商ChaiNext提供。\r\nhttps://chainext.io|微信公众号ChaiNext"
        }
      ]
    }
  ]
}
```






## 指数大幅涨跌报警信息 <span id="v1/wechat_monitor_24h"> GET /wechat_monitor_24h 以utc0时间为基准，获取当日的CSI指数涨跌幅报警信息

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | index CID or index name | ||
| date      | true  | string | query date, e.g. 2018-07-24 | ||


Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |hour monitor information |      |

API access example：https://api.chainext.io/v1/wechat_monitor_24h?id=csi100&date=2018-08-01

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": [
    {
      "total": 100,
      "data": [
        {
        "time": "2018-08-01 07:19:55",
        "content": "CSI指数行情大幅涨跌预警\r\n北京时间2018年08月01日07时19分,CSI100指数今日（UTC0起）累计下跌-5.49%,目前报1026.24点。\r\n其中,成分币中2上涨,98下跌。其中,涨幅居前为「BNB」(5.92%)。「XVG」(0.44%)。\r\n\r\n「CSI100」：CSI指数系列中的\"上证综指\"，样本由规模和流动性排名前100的通证组成，市值覆盖率达96%，反映了通证市场整体走势。\r\n\r\n本信息由企业级数字货币指数服务商ChaiNext提供。\r\nhttps://chainext.io|微信公众号ChaiNext"
        }
      ]
    }
  ]
}
```




## 代币大额转账报警信息 <span id="v1/largement_alert"> GET /largement_alert 获取代币大额转账报警信息

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | coin CID | ||
| date      | true  | string | query date, e.g. 2018-07-24 | ||


Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |代币大额转账报警信息|      |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |coin transfer alert |      |

API access example 1：https://api.chainext.io/v1/largement_alert?id=0&date=2018-07-31

API access example 2：https://api.chainext.io/v1/largement_alert

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": [
    {
      "total": 100,
      "data": [
        {
        "time": "2018-08-01 07:19:55",
        "content": "代币大额转账报警\r\n\r\nUTC0时间07月31日06时13分(北京时间07月31日14时13分)\r\n\r\nBTC发生数量为1297.95的大额转账交易（tx为8310336887225ae3248644201a406d23db0e7f8a7efa1c499b3fdc4079f6bcf2），转出方未知，转入方包含其他（共计1297.95个，100%）\r\n\r\n想了解更多详细信息，请登录ChaiNext官网https://chainext.io查询|微信公众号ChaiNext"
        }
      ]
    }
  ]
}
```
