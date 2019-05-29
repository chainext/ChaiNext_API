# ChaiNext API Instruction
Instruction for ChaiNext API use.
## ChaiNext API Introduction
ChaiNext provided a series of API, in order to help users obtain market information in real time.

Currently, ChaiNext API provide following functions:
* get basic information, market quotations and details of CSI indices
* get coin weight coefficient of CSI indices
* get chainext index data from tradingview
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
|Basic indices market information|[https://api.chainext.io/v1/index_basic](#basic-index-performance--get-index_basic)|GET|Get basic market information of indices|
|Weight|[https://api.chainext.io/v1/weight](##coin-weight-of-index--get-weight)|GET|Get weight coefficient of coins in indices|
|Index list|[https://api.chainext.io/v1/index_list](#index-list--get-index_list)|GET|get index list|
|Index performance|[https://api.chainext.io/v1/index_detail](#index-performance--get-index_detail)|GET|Get index performance under stated period of time|
|get chainext k chart in tradingview|[https://chainext.cn/tradingview](#get-chainext-k-chart-in-tradingview)|GET|get chainext k chart in tradingview|
|Candlestick chart|[https://api.chainext.io/v1/kchart](#index-candlestick-chart--get-kchart)|GET|get candlestick chart of CSI indices|
|Mapping list|[https://api.chainext.io/v1/mapping_list](#index-mapping-list--get-mapping_list)|GET|Get mapping list between CSI indices' CID and their names|
|Coin mapping list|[https://api.chainext.io/v1/coin_mapping_list](#coin-mapping-list--get-coin_mapping_list)|GET|Get mapping list between coins' CID and their names|
|Daily broadcast|[https://api.chainext.io/v1/wechat_broadcast](#index-daily-broadcast--get-wechat_broadcast)|GET|Get daily broadcast of CSI indices|
|Hourly broadcast|[https://api.chainext.io/v1/wechat_hour_broadcast](#index-hourly-broadcast--get-wechat_hour_broadcast)|GET|get hourly broadcast of CSI indices|
|Minute performance monitor information|[https://api.chainext.io/v1/wechat_monitor_min](#index-minute-monitor-information--get-wechat_monitor_min)|GET|get minute performance monitor information of CSI indices|
|Hour performance monitor information|[https://api.chainext.io/v1/wechat_monitor_24h](#index-hour-monitor-information--get-wechat_monitor_24h)|GET|get hour performance monitor information of CSI indices|
|Coin transfer alert information|[https://api.chainext.io/v1/largement_alert](#coin-transfer-alert--get-largement_alert)|GET|get coin transfer alert information|
|Sentiment Indices List|[https://api.chainext.io/v1/mood_indices](#sentiment-indices-list--get-mood_indices)|GET|get sentiment indices list, currently including BTC Bubble Index and USDT Index|
|Sentiment Indices Performance|[https://api.chainext.io/v1/mood_index](#sentiment-indices-performance--get-mood_index)|GET|get sentiment indices performance, currently including BTC Bubble Index and USDT Index|
|Coin Indices List|[https://api.chainext.io/v1/coinlist](#coin-indices-list--get-coinlist)|GET|get coin indices list, currently including top 100 cryptocurrencies|
|Coin Indices Performance|[https://api.chainext.io/v1/coin_detail](#coin-indices-performance--get-coin_detail)|GET|get coin indices performance, currently including top 100 cryptocurrencies|
|Last Coin Index|[https://api.chainext.cn/v1/coin_list_all](#last-coin-index--get-coin_list_all)|GET|get crypocurrencies realtime price, including most of the cryptocurrencies|
|Stable Coin Index|[https://vipapi.chainext.cn/v1/pegged?Fkey={apikey}](#stable-coin-index--get-pegged)|GET|get stable currency price and volume history|



## Basic Index Performance <span id="v1/index_basic"> GET /index_basic
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



## Coin Weight of Index <span id="v1/weight"> GET /weight
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

API access example：https://api.chainext.io/v1/weight?id=4

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


## Index List <span id="v1/index_list"> GET /index_list
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


## Index Performance <span id="v1/index_detail"> GET /index_detail

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


## get chainext k chart in tradingview


https://chainext.cn/tradingview  is chainext's cis index standard UDF，after you get the lisence from tradingview，you can get chainext k charts in tradingview directly。

including 5 interface 

```
/config
/time
/search
/symbol
/history
```

## Index Candlestick Chart <span id="v1/kchart"> GET /kchart

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
      ],  # unix timestamp，open,high,low,close,turnover    
      ...
    ]
  }
}
```

## Index Mapping List <span id="v1/mapping_list"> GET /mapping_list

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



## Coin Mapping List <span id="v1/coin_mapping_list"> GET /coin_mapping_list

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



## Index Daily Broadcast <span id="v1/wechat_broadcast"> GET /wechat_broadcast

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




## Index Hourly Broadcast <span id="v1/wechat_hour_broadcast"> GET /wechat_hour_broadcast

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



## Index Minute Monitor Information <span id="v1/wechat_monitor_min"> GET /wechat_monitor_min

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






## Index Hour Monitor Information <span id="v1/wechat_monitor_24h"> GET /wechat_monitor_24h

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




## Coin Transfer Alert <span id="v1/largement_alert"> GET /largement_alert

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | coin CID | ||
| date      | true  | string | query date, e.g. 2018-07-24 | ||


Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
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

## Sentiment Indices List <span id="v1/mood_indices"> GET /mood_indices

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| price7       | false  | integer | Display 7 days' data or not  | 1 |0，1|


Response: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |sentiment indices list|      |

API access example 1: https://api.chainext.io/v1/mood_indices


Response example:
```
{
  "code": 1000,
  "msg": "",
  "data": [
    {
      "symbol": "usdt_usd",
      "CID": 90001,
      "intro_en": "USDT Premium Index is designed to measure the premium of USDT against USD in OTC market. If index is greater than 1, the USDT is traded at premium, otherwise the USDT is traded at discount.",
      "intro_zh": "USDT折溢价指数由ChaiNext根据USDT场外价格及离岸人民币汇率进行计算，反映了资金出入通证市场的拥挤程度。指数大于1表示USDT溢价，小于1则表示USDT折价。",
      "url": "https://chainext-doc.oss-cn-beijing.aliyuncs.com/%E6%83%85%E7%BB%AA%E6%8C%87%E6%95%B0/ChaiNext-Index%20Methodology-USDT%20Premium%20INDEX.pdf",
      "full_name_en": "usdt premium index",
      "full_name_zh": "USDT折溢价指数",
      "latest": 0.997759,
      "change_24h": -0.1912629255024928,
      "change_24h_abs": -0.0019120000000000248,
      "change_utc0": -0.273963018490754,
      "change_utc0_abs": -0.0027409999999999934,
      "datetime": 1534993118,
      "price7": [
        1.00663,
        1.00646,
        1.00645,
        1.00649,
        1.00652,
        1.00669,
        ]
    }
}
```
API access example 2:https://api.chainext.io/v1/mood_indices?price7=0


Response example:
```
{
  "code": 1000,
  "msg": "",
  "data": [
    {
      "symbol": "usdt_usd",
      "CID": 90001,
      "intro_en": "USDT Premium Index is designed to measure the premium of USDT against USD in OTC market. If index is greater than 1, the USDT is traded at premium, otherwise the USDT is traded at discount.",
      "intro_zh": "USDT折溢价指数由ChaiNext根据USDT场外价格及离岸人民币汇率进行计算，反映了资金出入通证市场的拥挤程度。指数大于1表示USDT溢价，小于1则表示USDT折价。",
      "url": "https://chainext-doc.oss-cn-beijing.aliyuncs.com/%E6%83%85%E7%BB%AA%E6%8C%87%E6%95%B0/ChaiNext-Index%20Methodology-USDT%20Premium%20INDEX.pdf",
      "full_name_en": "usdt premium index",
      "full_name_zh": "USDT折溢价指数",
      "latest": 0.997759,
      "change_24h": -0.1912629255024928,
      "change_24h_abs": -0.0019120000000000248,
      "change_utc0": -0.273963018490754,
      "change_utc0_abs": -0.0027409999999999934,
      "datetime": 1534993118,
    }
}
```

## Sentiment Indices Performance <span id="v1/mood_index"> GET /mood_index

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | sentiment index CID | ||


Responce: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |date|      |

API access example1：https://api.chainext.io/v1/mood_index

Response example: 
```
{
  "code": 1000,
  "msg": "",
  "data": {
    "symbol": "usdt_usd",
    "CID": 90001,
    "intro_en": "USDT Premium Index is designed to measure the premium of USDT against USD in OTC market. If index is greater than 1, the USDT is traded at premium, otherwise the USDT is traded at discount.",
    "intro_zh": "USDT折溢价指数由ChaiNext根据USDT场外价格及离岸人民币汇率进行计算，反映了资金出入通证市场的拥挤程度。指数大于1表示USDT溢价，小于1则表示USDT折价。",
    "url": "https://chainext-doc.oss-cn-beijing.aliyuncs.com/%E6%83%85%E7%BB%AA%E6%8C%87%E6%95%B0/ChaiNext-Index%20Methodology-USDT%20Premium%20INDEX.pdf",
    "full_name_en": "usdt premium index",
    "full_name_zh": "USDT折溢价指数",
    "latest": 0.997759,
    "change_24h": -0.1912629255024928,
    "change_24h_abs": -0.0019120000000000248,
    "change_utc0": -0.273963018490754,
    "change_utc0_abs": -0.0027409999999999934,
    "datetime": 1534993118
  }
}
```
## Coin Indices List <span id="v1/coinlistt"> GET /coinlist
Request parameters: 

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| page       | true  | integer | page number | 1 |depending on number of indices|
| page_size       | true  | integer | rows per page  | 20 |depending on number of indices|
| price7       | false  | integer | Display 7 days' data or not  | 1 |0，1|

Responce: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |indices list data|      |
| updated_time| true | string |data updating time|      |

API access example1：https://api.chainext.io/v1/coinlist?page=1&page_size=10

Response example1: 
```
{
	"code": 1000,
	"msg": "",
	"data": {
		"total": 10,
		"current_page": 1,
		"data": [{
			"CID": 0,
			"symbol": "BTC",
			"cmc_symbol": "bitcoin",
			"latest": 6429.64119179315,
			"change_24h": 2.422936244366607,
			"change_24h_abs": 153.34800781297054,
			"change_utc0": -0.8133176664924541,
			"change_utc0_abs": -52.722206726400145,
			"marketcap": 111021578904.8711,
			"turnover_24h": 4345943880.98,
			"price7": [6193.00829910963, 6239.20066083109, 6313.31470854928, 6283.89114313655, 6329.01539070658, 6482.36339851955, 6557.90283812117]
		},
		......
		],
		"updated_time": 1536919458.3067229
	}
```
API access example2：https://api.chainext.io/v1/coinlist?page=1&page_size=10&price7=0

Response example2: 
```
{
	"code": 1000,
	"msg": "",
	"data": {
		"total": 10,
		"current_page": 1,
		"data": [{
			"CID": 0,
			"symbol": "BTC",
			"cmc_symbol": "bitcoin",
			"latest": 6429.64119179315,
			"change_24h": 2.422936244366607,
			"change_24h_abs": 153.34800781297054,
			"change_utc0": -0.8133176664924541,
			"change_utc0_abs": -52.722206726400145,
			"marketcap": 111021578904.8711,
			"turnover_24h": 4345943880.98,
		},
		......
		],
		"updated_time": 1536919458.3067229
	}
```



## Coin Indices Performance <span id="v1/coin_detail"> GET /coin_detail

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | integer | index CID | 1 |within coin indices|
| tstart       | false  | integer | start time | |Unix timestamp（unit：second，example：1530691531）|
| tend       | false  | integer | end time | |Unix timestamp（unit：second，example：1530691531）|

Responce: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |indice performance data|      |

API access example：https://api.chainext.io/v1/coin_detail?id=0

Response example: 
```
 {
	"code": 1000,
	"msg": "",
	"data": {
		"CID": 0,
		"symbol": "BTC",
		"cmc_symbol": "bitcoin",
		"latest": 6437.83077876688,
		"change_24h": 2.422936244366607,
		"change_24h_abs": 153.34800781297054,
		"change_utc0": -0.6869812291430708,
		"change_utc0_abs": -44.53261975267014,
		"marketcap": 111163150677.354,
		"turnover_24h": 4324973916.82,
		"price7": [6193.00829910963, 6239.20066083109, 6313.31470854928, 6283.89114313655, 6329.01539070658, 6482.36339851955, 6557.90283812117]
	}
}
```

## Last Coin Index  <span id="v1/coin_list_all"> GET /coin_list_all

Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | integer | indices CID | 1 |within coin indices|

Responce: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |last coin price data|      |

API access example：https://api.chainext.cn/v1/coin_list_all?id=0

Response example: 
```
 {
	"code": 1000,
	"msg": "",
	"data": [{
		"CID": 0,
		"symbol": "BTC",
		"cmc_symbol": "bitcoin",
		"latest": 6437.83077876688,
		“update": 1539571270
	}]
}
```

# Stable Coin Index <span id="v1/pegged"> GET /pegged


Request parameters:

| Name | Required  | Type     | Description  | Default   | Range  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| index_id       | false  | integer | indices CID | 13 |within coin indices|
| tstart       | false  | integer | start time | |Unix timestamp（unit：second，example：1530691531）|
| tend       | false  | integer | end time | |Unix timestamp（unit：second，example：1530691531）|

Responce: 

| Name | Required  | Type     | Description  | Range  |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | response result    |1000,1001,1002|
| msg     | true | string |related message|    |
| data   | true | object |last coin price data|      |

Avaliable Stable Coin

| Coin Symbol          | CID  |
| -------------------- | ---- |
| bitUSD               | 351  |
| Dai                  | 297  |
| Gemini Dollar        | 1929 |
| Paxos Standard Token | 1927 |
| sUSD                 | 1968 |
| Tether               | 13   |
| TrueUSD              | 481  |
| USD Coin             | 1928 |
| USDCoin              | 1969 |



API access example：https://vipapi.chainext.cn/v1/pegged?Fkey={apikey}&index_id=297&tstart=1558960800&tend=1559025600

please contact ChaiNext for authorization

Response example: 
```python
{
  "code": 1000,
  "msg": "",
  "data": [
    {
        "index_id": 297,
        "name": "DAI",
        "high": 1.00051,
        "open": 1.00051,
        "low": 0.998944,
        "close": 0.998944,
        "volume": 0.49833320384,
        "startTime": 1558960500,
        "endTime": 1558960800
    },
    {
        "index_id": 297,
        "name": "DAI",
        "high": 1.00055,
        "open": 1.00009,
        "low": 0.999812,
        "close": 1.00055,
        "volume": 0.38072716608,
        "startTime": 1558960800,
        "endTime": 1558961100
    }, ...
  ]
}


```
