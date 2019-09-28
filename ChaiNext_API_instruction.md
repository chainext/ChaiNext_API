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


### V1 API

| Data Type                                         | Method                                                                                               | type | Description                                                                            |
|---------------------------------------------------|------------------------------------------------------------------------------------------------------|------|----------------------------------------------------------------------------------------|
| Basic indices market information                  | [https://api.chainext.io/v1/index_basic](#basic-index-performance--get-index_basic)                  | GET  | Get basic market information of indices                                                |
| Weight                                            | [https://api.chainext.io/v1/weight](##coin-weight-of-index--get-weight)                              | GET  | Get weight coefficient of coins in indices                                             |
| Index list                                        | [https://api.chainext.io/v1/index_list](#index-list--get-index_list)                                 | GET  | get index list                                                                         |
| Index performance                                 | [https://api.chainext.io/v1/index_detail](#index-performance--get-index_detail)                      | GET  | Get index performance under stated period of time                                      |
| get chainext k chart in tradingview               | [https://chainext.cn/tradingview](#get-chainext-k-chart-in-tradingview)                              | GET  | get chainext k chart in tradingview                                                    |
| Candlestick chart                                 | [https://api.chainext.io/v1/kchart](#index-candlestick-chart--get-kchart)                            | GET  | get candlestick chart of CSI indices                                                   |
| Mapping list                                      | [https://api.chainext.io/v1/mapping_list](#index-mapping-list--get-mapping_list)                     | GET  | Get mapping list between CSI indices' CID and their names                              |
| Coin mapping list                                 | [https://api.chainext.io/v1/coin_mapping_list](#coin-mapping-list--get-coin_mapping_list)            | GET  | Get mapping list between coins' CID and their names                                    |
| Coin transfer alert information                   | [https://api.chainext.io/v1/largement_alert](#coin-transfer-alert--get-largement_alert)              | GET  | get coin transfer alert information                                                    |
| Selected coin transfer alert detailed information | [https://api.chainext.io/v1/largement_alert_new](#Selected-coin-transfer-alert-detailed-information) | GET  | get the latest 100 pieces of detailed transfer alert information of selected coin      |
| All coins transfer alert detailed information     | [https://api.chainext.io/v1/largement_alert_all](#All-coins-transfer-alert-detailed-information)     | GET  | get detailed transfer alert information of all available coins                         |
| Sentiment Indices List                            | [https://api.chainext.io/v1/mood_indices](#sentiment-indices-list--get-mood_indices)                 | GET  | get sentiment indices list, currently including BTC Bubble Index and USDT Index        |
| Sentiment Indices Performance                     | [https://api.chainext.io/v1/mood_index](#sentiment-indices-performance--get-mood_index)              | GET  | get sentiment indices performance, currently including BTC Bubble Index and USDT Index |
| Coin Indices List                                 | [https://api.chainext.io/v1/coinlist](#coin-indices-list--get-coinlist)                              | GET  | get coin indices list, currently including top 100 cryptocurrencies                    |
| Coin Indices Performance                          | [https://api.chainext.io/v1/coin_detail](#coin-indices-performance--get-coin_detail)                 | GET  | get coin indices performance, currently including top 100 cryptocurrencies             |
| Last Coin Index                                   | [https://api.chainext.cn/v1/coin_list_all](#last-coin-index--get-coin_list_all)                      | GET  | get crypocurrencies realtime price, including most of the cryptocurrencies             |
| Stable Coin Index                                 | [https://vipapi.chainext.cn/v1/pegged?Fkey={apikey}](#stable-coin-index--get-pegged)                 | GET  | get stable currency price and volume history                                           |
| Last Index                                        | [https://api.chainext.io/v1/index_realtime](#last-index--get-index_realtime)                         | GET  | get index realtime data, including price, marketCap and turnover                       |

### V2 API

* All `'csi'` in  `'index_code'` of v2 API will be changed into `'ChaiNext'`


| Data Type                        | Method                                                                              | type | Description                                                      |
|----------------------------------|-------------------------------------------------------------------------------------|------|------------------------------------------------------------------|
| Basic indices market information | [https://api.chainext.io/v2/index_basic](#basic-index-performance--get-index_basic) | GET  | Get basic market information of indices                          |
| Mapping list                     | [https://api.chainext.io/v2/mapping_list](#index-mapping-list--get-mapping_list)    | GET  | Get mapping list between CSI indices' CID and their names        |
| Index list                       | [https://api.chainext.io/v2/index_list](#index-list--get-index_list)                | GET  | get index list                                                   |
| Last Index                       | [https://api.chainext.io/v2/index_realtime](#last-index--get-index_realtime)        | GET  | get index realtime data, including price, marketCap and turnover |


## Basic Index Performance <span id="v1/index_basic"> GET /index_basic
Request parameters: 

| Name | Required | Type   | Description             | Default | Range |
|------|----------|--------|-------------------------|---------|-------|
| id   | true     | string | index CID or index name | 1       |       |

Response: 

| Name         | Required | Type   | Description                  | Range          |
|--------------|----------|--------|------------------------------|----------------|
| code         | true     | string | response result              | 1000,1001,1002 |
| msg          | true     | string | related message              |                |
| data         | true     | object | basic index performance data |                |
| updated_time | true     | string | data update time             |                |

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

| Name | Required | Type   | Description             | Default | Range |
|------|----------|--------|-------------------------|---------|-------|
| id   | true     | string | index CID or index name | 1       |       |

Response: 

| Name         | Required | Type   | Description       | Range          |
|--------------|----------|--------|-------------------|----------------|
| code         | true     | string | response result   | 1000,1001,1002 |
| msg          | true     | string | related message   |                |
| data         | true     | object | index weight data |                |
| updated_time | true     | string | data update time  |                |

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

| Name      | Required | Type    | Description | Default | Range |
|-----------|----------|---------|-------------|---------|-------|
| page      | true     | integer | page        | 1       |       |
| page_size | true     | integer | page size   | 20      |       |

Response:

| Name         | Required | Type   | Description      | Range          |
|--------------|----------|--------|------------------|----------------|
| code         | true     | string | response result  | 1000,1001,1002 |
| msg          | true     | string | related message  |                |
| data         | true     | object | index list data  |                |
| updated_time | true     | string | data update time |                |

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

| Name   | Required | Type    | Description | Default | Range                           |
|--------|----------|---------|-------------|---------|---------------------------------|
| id     | true     | integer | index CID   | 1       |                                 |
| tstart | true     | integer | start time  |         | Unix timestamp（e.g. 1520691531） |
| tend   | true     | integer | end time    |         | Unix timestamp（e.g. 1530691531） |

Response: 

| Name | Required | Type   | Description            | Range          |
|------|----------|--------|------------------------|----------------|
| code | true     | string | response result        | 1000,1001,1002 |
| msg  | true     | string | related message        |                |
| data | true     | object | index performance data |                |

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

| Name     | Required | Type    | Description          | Default | Range                                                |
|----------|----------|---------|----------------------|---------|------------------------------------------------------|
| id       | true     | integer | index CID            | 1       |                                                      |
| tstart   | true     | integer | start time           |         | Unix timestamp（e.g. 1520691531）                      |
| tend     | true     | integer | end time             |         | Unix timestamp（e.g. 1530691531）                      |
| grouping | true     | string  | time grouping method |         | 1min, 5min,15min, 30min, 1H, 4h, 6h, 12h, 1D, 1w, 1m |

Response: 

| Name | Required | Type   | Description                  | Range          |
|------|----------|--------|------------------------------|----------------|
| code | true     | string | response result              | 1000,1001,1002 |
| msg  | true     | string | related message              |                |
| data | true     | object | index candlestick chart data |                |

API access example：https://api.chainext.io/v1/kchart?id=4&grouping=1D&tstart=1530316800&tend=1531983011

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

| Name | Required | Type   | Description              | Range          |
|------|----------|--------|--------------------------|----------------|
| code | true     | string | response result          | 1000,1001,1002 |
| msg  | true     | string | related message          |                |
| data | true     | object | index CID and index name |                |

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

| Name | Required | Type   | Description             | Range          |
|------|----------|--------|-------------------------|----------------|
| code | true     | string | response result         | 1000,1001,1002 |
| msg  | true     | string | related message         |                |
| data | true     | object | coin CID and index name |                |

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


## Coin Transfer Alert <span id="v1/largement_alert"> GET /largement_alert

Request parameters:

| Name | Required | Type    | Description                 | Default | Range |
|------|----------|---------|-----------------------------|---------|-------|
| id   | true     | integer | coin CID                    |         |       |
| date | true     | string  | query date, e.g. 2018-07-24 |         |       |


Response: 

| Name | Required | Type   | Description         | Range          |
|------|----------|--------|---------------------|----------------|
| code | true     | string | response result     | 1000,1001,1002 |
| msg  | true     | string | related message     |                |
| data | true     | object | coin transfer alert |                |

API access example 1：https://api.chainext.io/v1/largement_alert?id=0

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

## Detailed Selected Coin Transfer Alert<span id="v1/largement_alert_new"> GET /largement_alert_new 

Request parameters:

| Name | Required | Type    | Description | Default | Range |
|------|----------|---------|-------------|---------|-------|
| id   | false    | integer | coin CID    | 0       |       |


Response: 

| Name | Required | Type   | Description         | Range          |
|------|----------|--------|---------------------|----------------|
| code | true     | string | response result     | 1000,1001,1002 |
| msg  | true     | string | related message     |                |
| data | true     | object | coin transfer alert |                |

API access example 1：https://api.chainext.io/v1/largement_alert_new?id=0

Response example: 
```json
{
  "code": 1000,
  "msg": "",
  "data": [
    {
      "id": 596076,
      "date": "2019-09-05 10:02:21",
      "level": 2,
      "money": 2444.65,
      "fee": 0.00001892,
      "tx_add": "fe0fa5aa820e7da5a0e6ae644e74f1f26dc4b5cdb8cac29a3cd2cd115f277d25",
      "payer_owner": null,
      "payee_owner": [
        null
        ],
      "CID": 0,
      "is_con": 1,
      "tx_url": "https://www.blockchain.com/btc/tx/fe0fa5aa820e7da5a0e6ae644e74f1f26dc4b5cdb8cac29a3cd2cd115f277d25"
    }
  ]
}
```

## Detailed All Coin Transfer Alert <span id="v1/largement_alert_all"> GET /largement_alert_all 

Request parameters:

| Name | Required | Type    | Description                    | Default | Range |
|------|----------|---------|--------------------------------|---------|-------|
| num  | false    | integer | number of returned information | 1000    |       |

Response: 

| Name | Required | Type   | Description         | Range          |
|------|----------|--------|---------------------|----------------|
| code | true     | string | response result     | 1000,1001,1002 |
| msg  | true     | string | related message     |                |
| data | true     | object | coin transfer alert |                |

API access example 1：https://api.chainext.io/v1/largement_alert_all?num=1

Response example: 
```json
{
  "msg": "",
  "updated_time": 1567682554,
  "code": 1000,
  "data": [
    {
      "id": 596237,
      "date": "2019-09-05 11:18:29",
      "level": 2,
      "money": 747,
      "fee": 0.00183124,
      "tx_add": "0xbe6746e2c176f1bf713e7e4ba178292190acd51bba06e47f25b1bcd23e1e59ef",
      "payer_owner": "富豪榜排名:30",
      "payee_owner": [
        null
        ],
      "CID": 27,
      "is_con": 1
    }
  ]
}
```

## Sentiment Indices List <span id="v1/mood_indices"> GET /mood_indices

Request parameters:

| Name   | Required | Type    | Description                 | Default | Range |
|--------|----------|---------|-----------------------------|---------|-------|
| price7 | false    | integer | Display 7 days' data or not | 1       | 0，1   |


Response: 

| Name | Required | Type   | Description            | Range          |
|------|----------|--------|------------------------|----------------|
| code | true     | string | response result        | 1000,1001,1002 |
| msg  | true     | string | related message        |                |
| data | true     | object | sentiment indices list |                |

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

| Name | Required | Type    | Description         | Default | Range |
|------|----------|---------|---------------------|---------|-------|
| id   | true     | integer | sentiment index CID |         |       |


Responce: 

| Name | Required | Type   | Description     | Range          |
|------|----------|--------|-----------------|----------------|
| code | true     | string | response result | 1000,1001,1002 |
| msg  | true     | string | related message |                |
| data | true     | object | date            |                |

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

| Name      | Required | Type    | Description                 | Default | Range                          |
|-----------|----------|---------|-----------------------------|---------|--------------------------------|
| page      | true     | integer | page number                 | 1       | depending on number of indices |
| page_size | true     | integer | rows per page               | 20      | depending on number of indices |
| price7    | false    | integer | Display 7 days' data or not | 1       | 0，1                            |

Responce: 

| Name         | Required | Type   | Description        | Range          |
|--------------|----------|--------|--------------------|----------------|
| code         | true     | string | response result    | 1000,1001,1002 |
| msg          | true     | string | related message    |                |
| data         | true     | object | indices list data  |                |
| updated_time | true     | string | data updating time |                |

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

| Name   | Required | Type    | Description | Default | Range                                          |
|--------|----------|---------|-------------|---------|------------------------------------------------|
| id     | true     | integer | index CID   | 1       | within coin indices                            |
| tstart | false    | integer | start time  |         | Unix timestamp（unit：second，example：1530691531） |
| tend   | false    | integer | end time    |         | Unix timestamp（unit：second，example：1530691531） |

Responce: 

| Name | Required | Type   | Description             | Range          |
|------|----------|--------|-------------------------|----------------|
| code | true     | string | response result         | 1000,1001,1002 |
| msg  | true     | string | related message         |                |
| data | true     | object | indice performance data |                |

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

| Name | Required | Type    | Description | Default | Range               |
|------|----------|---------|-------------|---------|---------------------|
| id   | true     | integer | indices CID | 1       | within coin indices |

Responce: 

| Name | Required | Type   | Description          | Range          |
|------|----------|--------|----------------------|----------------|
| code | true     | string | response result      | 1000,1001,1002 |
| msg  | true     | string | related message      |                |
| data | true     | object | last coin price data |                |

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

| Name     | Required | Type    | Description | Default | Range                                          |
|----------|----------|---------|-------------|---------|------------------------------------------------|
| index_id | false    | integer | indices CID | 13      | within coin indices                            |
| tstart   | false    | integer | start time  |         | Unix timestamp（unit：second，example：1530691531） |
| tend     | false    | integer | end time    |         | Unix timestamp（unit：second，example：1530691531） |

Responce: 

| Name | Required | Type   | Description          | Range          |
|------|----------|--------|----------------------|----------------|
| code | true     | string | response result      | 1000,1001,1002 |
| msg  | true     | string | related message      |                |
| data | true     | object | last coin price data |                |

Avaliable Stable Coin

| Coin Symbol          | CID  |
|----------------------|------|
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


## Last Index  <span id="v1/index_realtime"> GET /index_realtime

Request parameters:

null

Responce: 

| Name         | Required | Type   | Description          | Range          |
|--------------|----------|--------|----------------------|----------------|
| code         | true     | string | response result      | 1000,1001,1002 |
| msg          | true     | string | related message      |                |
| data         | true     | object | last coin price data |                |
| updated_time | true     | string | data updating time   |                |

API access example：https://api.chainext.io/v1/index_realtime

Response example: 
```
{
  "msg": "",
  "updated_time": 1562214072,
  "code": 1000,
  "data": [
    {
      "indexId": 1,
      "indexCode": "csi10X",
      "lastPrice": "2946.522825168813849624789268",
      "marketCap": "82096273083.3017056",
      "turnover": "21128649724.115504",
      "updateTime": 1562214069
    },
    {
      "indexId": 2,
      "indexCode": "csi10",
      "lastPrice": "1107.532109466394737066796435",
      "marketCap": "293119075844.4470656",
      "turnover": "49807628976.405104",
      "updateTime": 1562214069
    },
    ...
  ]
}
```

## V2 API Introduction

## Basic Index Performance <span id="v2/index_basic"> GET /index_basic
Request parameters: 

| Name | Required | Type   | Description             | Default | Range |
|------|----------|--------|-------------------------|---------|-------|
| id   | true     | string | index CID or index name | 1       |       |

Response: 

| Name         | Required | Type   | Description                  | Range          |
|--------------|----------|--------|------------------------------|----------------|
| code         | true     | string | response result              | 1000,1001,1002 |
| msg          | true     | string | related message              |                |
| data         | true     | object | basic index performance data |                |
| updated_time | true     | string | data update time             |                |

API access example：https://api.chainext.io/v2/index_basic?id=1

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": {
    "download": [
        {
          "name": "编制方案",
          "url": "https://chainext.oss-cn-hongkong.aliyuncs.com/doc/20180626/BZFA.pdf"
        },
        {
          "name": "指数单张",
          "url": "https://chainext.oss-cn-hongkong.aliyuncs.com/doc/20180626/CSI10X_ZSDZ.pdf"
        }
    ],
    "related": [],
    "abstract": "CSI 10X指数由CSI 10指数样本剔除比特币后组成，反映除比特币以外的代币市场大盘币种的价格走势",
    "index_symbol": "ChaiNext10X",
    "latest": {
    "marketcap": 45660778158,
    "changes": 2.7559325955,
    "change_abs": 43.2737310555587,
    "turnover_24h": 14900829929.014524,
    "change_utc0": -0.0182570438,
    "lastprice": 1613.4765410035984,
    "change_abs_utc0": -0.294626908624
    }
  },
  "updated_time": 1530690774.3714838
}
```

## Index List <span id="v2/index_list"> GET /index_list
Request parameters:

| Name      | Required | Type    | Description | Default | Range |
|-----------|----------|---------|-------------|---------|-------|
| page      | true     | integer | page        | 1       |       |
| page_size | true     | integer | page size   | 20      |       |

Response:

| Name         | Required | Type   | Description      | Range          |
|--------------|----------|--------|------------------|----------------|
| code         | true     | string | response result  | 1000,1001,1002 |
| msg          | true     | string | related message  |                |
| data         | true     | object | index list data  |                |
| updated_time | true     | string | data update time |                |

API access example：https://api.chainext.io/v2/index_list?page=1&page_size=20

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
                "symbol": "ChaiNext10X",
                "id": "ChaiNext10X",
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

## Index Mapping List <span id="v2/mapping_list"> GET /mapping_list

Request parameters:

None.

Response: 

| Name | Required | Type   | Description              | Range          |
|------|----------|--------|--------------------------|----------------|
| code | true     | string | response result          | 1000,1001,1002 |
| msg  | true     | string | related message          |                |
| data | true     | object | index CID and index name |                |

API access example：https://api.chainext.io/v2/mapping_list

Response example: 
```
  {
  "code": 1000,
  "msg": "",
  "data": {
    "CID": {
      "index_CID": 1,
      "index_code": "ChaiNext10X",
      "index_name_ch": "ChaiNext大盘规模指数NoBTC"
    }
  }
```


## Last Index  <span id="v2/index_realtime"> GET /index_realtime

Request parameters:

null

Responce: 

| Name         | Required | Type   | Description          | Range          |
|--------------|----------|--------|----------------------|----------------|
| code         | true     | string | response result      | 1000,1001,1002 |
| msg          | true     | string | related message      |                |
| data         | true     | object | last coin price data |                |
| updated_time | true     | string | data updating time   |                |

API access example：https://api.chainext.io/v2/index_realtime

Response example: 
```
{
  "msg": "",
  "updated_time": 1562214072,
  "code": 1000,
  "data": [
    {
      "indexId": 1,
      "indexCode": "ChaiNext10X",
      "lastPrice": "2946.522825168813849624789268",
      "marketCap": "82096273083.3017056",
      "turnover": "21128649724.115504",
      "updateTime": 1562214069
    },
    {
      "indexId": 2,
      "indexCode": "ChaiNext10X",
      "lastPrice": "1107.532109466394737066796435",
      "marketCap": "293119075844.4470656",
      "turnover": "49807628976.405104",
      "updateTime": 1562214069
    },
    ...
  ]
}
```

## code return type

| code | msg               | type                                    |
| :-:  | :-:               | :-:                                     |
| 1000 | ""                | success                                 |
| 1001 | "data not ready"  | no data                                 |
| 1002 | "wrong parameter" | the parameter input has something wrong |
