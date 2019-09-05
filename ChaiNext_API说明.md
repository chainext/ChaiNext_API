# ChaiNext API 接口说明文档
关于ChaiNext API 接口的使用说明文档。
## ChaiNext API 简介
ChaiNext为用户提供了一套行情查询的API接口，旨在帮助用户快速、高效地查询和了解实时行情，获取相关信息。

目前ChaiNext API提供以下功能：
* 获取CSI系列指数信息、指数基本行情以及指数表现
* 获取CSI系列指数中币种的权重系数
* 在tradingview中直接调用chainext的指数行情
* 获取CSI系列指数K线图
* 获取CSI系列指数的CID与指数名称映射表
* 获取单币的CID与单币名称映射表
* 获取CSI系列指数每日播报
* 获取CSI系列指数整点播报
* 获取CSI系列指数快速涨跌异动监控信息
* 获取CSI系列指数大幅涨跌报警监控信息
* 获取代币大额转账报警信息
* 获取价格基准指数信息、指数基本行情以及指数表现
* 获取情绪指数信息、指数基本行情以及指数表现

API访问地址：



国内用户请访问：[https://api.chainext.cn/v1](https://api.chainext.io/v1)

海外用户请访问：[https://api.chainext.io/v1](https://api.chainext.io/v1)

* **上述api接口为为cdn转发接口，如需获取低延迟直连接口，请联系chainext**

媒体朋友想获取ChaiNext的原创文章可以使用rss，但是麻烦请标明转自ChaiNext哦！

RSS链接：https://doc.chainext.cn/feed/ 或者 https://doc.chainext.io/feed/

## API 接口说明
| 接口数据类型                    | 请求方法                                                                                                    | 类型  | 描述                                    |
|---------------------------|---------------------------------------------------------------------------------------------------------|-----|---------------------------------------|
| 基本指数行情                    | [https://api.chainext.io/v1/index_basic](#基本指数行情)                                                       | GET | 获取指数的基本行情                             |
| 权重                        | [https://api.chainext.io/v1/weight](#指数权重信息--get-weight-获取指数的权重信息)                                      | GET | 获取指数的权重信息                             |
| 通证指数列表                    | [https://api.chainext.io/v1/index_list](#通证指数列表信息--get-index_list-获取通证指数列表信息)                           | GET | 获取通证指数列表信息                            |
| 通证指数表现                    | [https://api.chainext.io/v1/index_detail](#通证指数表现相关信息--get-index_detail-获取指数表现相关信息)                     | GET | 获取通证指数在指定时段段内的表现相关信息                  |
| tradingview中调用chainext的K线 | [https://chainext.cn/tradingview](#直接调用chainext在tradingview上的数据)                                        | GET | 直接调用chainext在tradingview上的数据          |
| K线图                       | [https://api.chainext.io/v1/kchart](#指数k线图)                                                             | GET | 获取指数K线图                               |
| 指数CID映射表                  | [https://api.chainext.io/v1/mapping_list](#单币cid与指数名称对应表--get-coin_mapping_list-获取单币cid与单币名称的相关说明)      | GET | 获取指数CID与指数名称的相关说明                     |
| 单币CID映射表                  | [https://api.chainext.io/v1/coin_mapping_list](#单币cid与指数名称对应表--get-coin_mapping_list-获取单币cid与单币名称的相关说明) | GET | 获取单币CID与单币名称的相关说明                     |
| 代币大额转账报警                  | [https://api.chainext.io/v1/largement_alert](#代币大额转账报警信息--get-largement_alert-获取代币大额转账报警信息)             | GET | 获取代币大额转账报警信息                          |
| 单种代币大额转账详细信息              | [https://api.chainext.io/v1/largement_alert_new](#单种代币大额转账详细信息--get-largement_alert_new-单种代币大额转账详细信息)   | GET | 单种代币大额转账详细信息                          |
| 全部代币大额转账详细信息              | [https://api.chainext.io/v1/largement_alert_all](#全部代币大额转账详细信息--get-largement_alert_all-全部代币大额转账详细信息)   | GET | 全部代币大额转账详细信息                          |
| 情绪指数列表                    | [https://api.chainext.io/v1/mood_indices](#情绪指数列表--get-mood_indices-获取情绪指数列表)                           | GET | 获取情绪指数列表，目前包括BTC泡沫指数和USDT折溢价指数        |
| 情绪指数表现                    | [https://api.chainext.io/v1/mood_index](#情绪指数表现--get-mood_index-获取情绪指数表现)                               | GET | 获取情绪指数信息，目前包括BTC泡沫指数和USDT折溢价指数        |
| 价格基准指数列表                  | [https://api.chainext.io/v1/coinlist](#价格基准指数列表--get-coinlist-获取价格基准指数列表)                               | GET | 获取价格基准指数列表，目前包括市值排名前100的数字货币的价格基准指数列表 |
| 价格基准指数表现                  | [https://api.chainext.io/v1/coin_detail](#价格基准指数表现--get-coin_detail-获取价格基准指数表现)                         | GET | 获取价格基准指数信息，目前包括市值排名前100的数字货币的价格基准指数信息 |
| 单币最新价格列表                  | [https://api.chainext.cn/v1/coin_list_all](#单币最新价格列表--get-coin_list_all-获取单币最新价格列表)                     | GET | 获取数字货币的实时最新价格，有市场上大多数数字货币的实时最新价格      |
| 稳定币指数                     | [https://vipapi.chainext.cn/v1/pegged?Fkey={apikey}](#稳定币数据--get-pegged-获取稳定币数据)                        | GET | 获取稳定币历史数据                             |
| 指数最新数据列表                  | [https://api.chainext.cn/v1/index_realtime](#指数最新数据列表--get-index_realtime-获取所有指数最新数据)                   | GET | 获取指数最新数据                              |

### 基本指数行情 <span id="v1/index_basic"> GET /index_basic 获取基本指数行情
请求参数: 

| 参数名称 | 是否必须 | 类型     | 描述         | 默认值 | 取值范围       |
|------|------|--------|------------|-----|------------|
| id   | true | string | 指数CID或指数名称 | 1   | 由指数CID范围决定 |

响应数据: 

| 参数名称         | 是否必须 | 数据类型   | 描述       | 取值范围           |
|--------------|------|--------|----------|----------------|
| code         | true | string | 请求处理结果   | 1000,1001,1002 |
| msg          | true | string | 相关处理信息   |                |
| data         | true | object | 基本指数行情数据 |                |
| updated_time | true | string | 数据更新时间   |                |

接口访问示例：https://api.chainext.io/v1/index_basic?id=1

返回数据示例: 
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
请求参数: 

| 参数名称 | 是否必须 | 类型     | 描述         | 默认值 | 取值范围       |
|------|------|--------|------------|-----|------------|
| id   | true | string | 指数CID或指数名称 | 1   | 由指数CID范围决定 |

响应数据: 

| 参数名称         | 是否必须 | 数据类型   | 描述     | 取值范围           |
|--------------|------|--------|--------|----------------|
| code         | true | string | 请求处理结果 | 1000,1001,1002 |
| msg          | true | string | 相关处理信息 |                |
| data         | true | object | 指数权重数据 |                |
| updated_time | true | string | 数据更新时间 |                |

接口访问示例：https://api.chainext.io/v1/weight?id=4

返回数据示例: 
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






## 通证指数列表信息 <span id="v1/index_list"> GET /index_list 获取通证指数列表信息
请求参数: 

| 参数名称      | 是否必须  | 类型      | 描述       | 默认值 | 取值范围    |
|-----------|-------|---------|----------|-----|---------|
| page      | true  | integer | 页码       | 1   | 由指数数量决定 |
| page_size | true  | integer | 每页数量     | 20  | 由指数数量决定 |
| price7    | false | integer | 是否需要7日数据 | 1   | 0，1     |

响应数据: 

| 参数名称         | 是否必须 | 数据类型   | 描述     | 取值范围           |
|--------------|------|--------|--------|----------------|
| code         | true | string | 请求处理结果 | 1000,1001,1002 |
| msg          | true | string | 相关处理信息 |                |
| data         | true | object | 指数列表数据 |                |
| updated_time | true | string | 数据更新时间 |                |

接口访问示例1：https://api.chainext.io/v1/index_list?page=1&page_size=20

返回数据示例1: 
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
接口访问示例2：https://api.chainext.io/v1/index_list?page=1&page_size=20&price7=0

返回数据示例2: 
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
                "hot": 10000
              }
            ]
          }
        }
```



## 通证指数表现相关信息 <span id="v1/index_detail"> GET /index_detail 获取通证指数表现相关信息

请求参数:

| 参数名称   | 是否必须 | 类型      | 描述    | 默认值 | 取值范围                        |
|--------|------|---------|-------|-----|-----------------------------|
| id     | true | integer | 指数CID | 1   | 指数范围内                       |
| tstart | true | integer | 开始时间  |     | Unix时间戳（单位：秒，例如：1530691531） |
| tend   | true | integer | 结束时间  |     | Unix时间戳（单位：秒，例如：1530691531） |

响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述       | 取值范围           |
|------|------|--------|----------|----------------|
| code | true | string | 请求处理结果   | 1000,1001,1002 |
| msg  | true | string | 相关处理信息   |                |
| data | true | object | 指数表现相关数据 |                |

接口访问示例：https://api.chainext.io/v1/index_detail?id=1&tstart=1520091531&tend=1530687931

返回数据示例: 
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

## 直接调用chainext在tradingview上的数据


https://chainext.cn/tradingview  是我们CSI指数实现的标准UDF，您向tradingview获取到代码许可后，可直接在tradingview中轻松调用chainext的指数K线行情。

包含五个接口 

```
/config
/time
/search
/symbol
/history
```



## 指数K线图 <span id="v1/kchart"> GET /kchart 获取指数K线图

请求参数:

| 参数名称     | 是否必须 | 类型      | 描述    | 默认值 | 取值范围                                        |
|----------|------|---------|-------|-----|---------------------------------------------|
| id       | true | integer | 指数CID | 1   | 指数范围内                                       |
| tstart   | true | integer | 开始时间  |     | Unix时间戳（单位：秒，例如：1530691531）                 |
| tend     | true | integer | 结束时间  |     | Unix时间戳（单位：秒，例如：1530691531）                 |
| grouping | true | string  | 时间间隔  |     | 1min,5min,15min,30min,1H,4h,6h,12h,1D,1w,1m |

响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述     | 取值范围           |
|------|------|--------|--------|----------------|
| code | true | string | 请求处理结果 | 1000,1001,1002 |
| msg  | true | string | 相关处理信息 |                |
| data | true | object | 指数K线图  |                |

接口访问示例：https://api.chainext.io/v1/kchart?id=4&grouping=1D&tstart=1530316800&tend=1531983011

返回数据示例: 
```
  {
  "code": 1000,
  "msg": "",
  "data": {
    "success": true,
    "lines": [
      [
        "1529093700000, 0.075646, 0.076141, 0.075646, 0.076035, 356.9439"
      ],  # 数据分别为unix时间戳，开盘价，最高价，最低价，收盘价，交易额    
      ...
    ]
  }
}
```

## 指数CID与指数名称对应表 <span id="v1/mapping_list"> GET /mapping_list 获取指数CID与指数名称的相关说明

请求参数:

无。

响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述           | 取值范围           |
|------|------|--------|--------------|----------------|
| code | true | string | 请求处理结果       | 1000,1001,1002 |
| msg  | true | string | 相关处理信息       |                |
| data | true | object | 指数CID与指数名称数据 |                |

接口访问示例：https://api.chainext.io/v1/mapping_list

返回数据示例: 
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

请求参数:

无。

响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述           | 取值范围           |
|------|------|--------|--------------|----------------|
| code | true | string | 请求处理结果       | 1000,1001,1002 |
| msg  | true | string | 相关处理信息       |                |
| data | true | object | 单币CID与单币名称数据 |                |

接口访问示例：https://api.chainext.io/v1/coin_mapping_list

返回数据示例: 
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


## 代币大额转账报警信息 <span id="v1/largement_alert"> GET /largement_alert 获取代币大额转账报警信息

请求参数:

| 参数名称 | 是否必须 | 类型      | 描述                 | 默认值 | 取值范围 |
|------|------|---------|--------------------|-----|------|
| id   | true | integer | 见单币CID映射表          |     |      |
| date | true | string  | 查询日期，格式 2018-07-24 |     |      |


响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述         | 取值范围           |
|------|------|--------|------------|----------------|
| code | true | string | 请求处理结果     | 1000,1001,1002 |
| msg  | true | string | 相关处理信息     |                |
| data | true | object | 代币大额转账报警信息 |                |

接口访问示例1：https://api.chainext.io/v1/largement_alert?id=0

返回数据示例: 
```
  {
  "code": 1000,
  "msg": "",
  "data": [
    {
      "total": 100,
      "data": [
        {
        "title": "ChaiNext:WTC发生数量499089.0的大额转账",
        "time": "2018-08-01 07:19:55",
        "content": "代币大额转账报警\r\n\r\nUTC0时间07月31日06时13分(北京时间07月31日14时13分)\r\n\r\nBTC发生数量为1297.95的大额转账交易（tx为8310336887225ae3248644201a406d23db0e7f8a7efa1c499b3fdc4079f6bcf2），转出方未知，转入方包含其他（共计1297.95个，100%）\r\n\r\n想了解更多详细信息，请登录ChaiNext官网https://chainext.io查询|微信公众号ChaiNext"
        }
      ]
    }
  ]
}
```



## 单种代币大额转账详细信息 <span id="v1/largement_alert_new"> GET /largement_alert_new 单种代币大额转账详细信息

请求参数:

| 参数名称 | 是否必须  | 类型      | 描述        | 默认值 | 取值范围 |
|------|-------|---------|-----------|-----|------|
| id   | false | integer | 见单币CID映射表 | 0   |      |


响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述         | 取值范围           |
|------|------|--------|------------|----------------|
| code | true | string | 请求处理结果     | 1000,1001,1002 |
| msg  | true | string | 相关处理信息     |                |
| data | true | object | 代币大额转账报警信息 |                |

接口访问示例1：https://api.chainext.io/v1/largement_alert_new?id=0

返回数据示例: 
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



## 单种代币大额转账详细信息 <span id="v1/largement_alert_all"> GET /largement_alert_all 单种代币大额转账详细信息

请求参数:

| 参数名称 | 是否必须  | 类型      | 描述     | 默认值  | 取值范围 |
|------|-------|---------|--------|------|------|
| num  | false | integer | 返回信息数量 | 1000 |      |



响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述         | 取值范围           |
|------|------|--------|------------|----------------|
| code | true | string | 请求处理结果     | 1000,1001,1002 |
| msg  | true | string | 相关处理信息     |                |
| data | true | object | 代币大额转账报警信息 |                |

接口访问示例1：https://api.chainext.io/v1/largement_alert_all?num=1

返回数据示例: 
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


## 情绪指数列表 <span id="v1/mood_indices"> GET /mood_indices 获取情绪指数列表

请求参数:

| 参数名称   | 是否必须  | 类型      | 描述       | 默认值 | 取值范围 |
|--------|-------|---------|----------|-----|------|
| price7 | false | integer | 是否需要7日数据 | 1   | 0，1  |


响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述     | 取值范围           |
|------|------|--------|--------|----------------|
| code | true | string | 请求处理结果 | 1000,1001,1002 |
| msg  | true | string | 相关处理信息 |                |
| data | true | object | 情绪指数列表 |                |

接口访问示例1：https://api.chainext.io/v1/mood_indices


返回数据示例: 
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
接口访问示例2：https://api.chainext.io/v1/mood_indices?price7=0


返回数据示例: 
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

## 情绪指数表现<span id="v1/mood_index"> GET /mood_index 获取情绪指数表现

请求参数:

| 参数名称 | 是否必须 | 类型      | 描述      | 默认值 | 取值范围 |
|------|------|---------|---------|-----|------|
| id   | true | integer | 情绪指数CID |     |      |


响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述     | 取值范围           |
|------|------|--------|--------|----------------|
| code | true | string | 请求处理结果 | 1000,1001,1002 |
| msg  | true | string | 相关处理信息 |                |
| data | true | object | 日期     |                |

接口访问示例1：https://api.chainext.io/v1/mood_index

返回数据示例: 
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
## 价格基准指数列表 <span id="v1/coinlistt"> GET /coinlist获取价格基准指数列表
请求参数: 

| 参数名称      | 是否必须  | 类型      | 描述       | 默认值 | 取值范围    |
|-----------|-------|---------|----------|-----|---------|
| page      | true  | integer | 页码       | 1   | 由指数数量决定 |
| page_size | true  | integer | 每页数量     | 20  | 由指数数量决定 |
| price7    | false | integer | 是否需要7日数据 | 1   | 0，1     |

响应数据: 

| 参数名称         | 是否必须 | 数据类型   | 描述     | 取值范围           |
|--------------|------|--------|--------|----------------|
| code         | true | string | 请求处理结果 | 1000,1001,1002 |
| msg          | true | string | 相关处理信息 |                |
| data         | true | object | 指数列表数据 |                |
| updated_time | true | string | 数据更新时间 |                |

接口访问示例1：https://api.chainext.io/v1/coinlist?page=1&page_size=10

返回数据示例1: 
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
接口访问示例2：https://api.chainext.io/v1/coinlist?page=1&page_size=10&price7=0

返回数据示例2: 
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



## 价格基准指数表现 <span id="v1/coin_detail"> GET /coin_detail 获取价格基准指数表现

请求参数:

| 参数名称   | 是否必须  | 类型      | 描述    | 默认值 | 取值范围                        |
|--------|-------|---------|-------|-----|-----------------------------|
| id     | true  | integer | 指数CID | 1   | 指数范围内                       |
| tstart | false | integer | 开始时间  |     | Unix时间戳（单位：秒，例如：1530691531） |
| tend   | false | integer | 结束时间  |     | Unix时间戳（单位：秒，例如：1530691531） |

响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述       | 取值范围           |
|------|------|--------|----------|----------------|
| code | true | string | 请求处理结果   | 1000,1001,1002 |
| msg  | true | string | 相关处理信息   |                |
| data | true | object | 指数表现相关数据 |                |

接口访问示例：https://api.chainext.io/v1/coin_detail?id=0

返回数据示例: 
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

## 单币最新价格列表 <span id="v1/coin_list_all"> GET /coin_list_all 获取单币最新价格列表



请求参数:

| 参数名称 | 是否必须  | 类型      | 描述    | 默认值 | 取值范围  |
|------|-------|---------|-------|-----|-------|
| id   | false | integer | 指数CID |     | 指数范围内 |

响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述         | 取值范围           |
|------|------|--------|------------|----------------|
| code | true | string | 请求处理结果     | 1000,1001,1002 |
| msg  | true | string | 相关处理信息     |                |
| data | true | object | 单币最新价格相关数据 |                |

接口访问示例：https://api.chainext.cn/v1/coin_list_all?id=0

返回数据示例: 
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

## 稳定币数据 <span id="v1/pegged"> GET /pegged 获取稳定币数据


请求参数:

| 参数名称     | 是否必须  | 类型      | 描述    | 默认值        | 取值范围                        |
|----------|-------|---------|-------|------------|-----------------------------|
| index_id | false | integer | 指数CID | 13         | 指数范围内                       |
| tstart   | false | integer | 开始时间  | 当前时间       | Unix时间戳（单位：秒，例如：1530691531) |
| tend     | false | integer | 结束时间  | 当前时间 - 24h | Unix时间戳（单位：秒，例如：1530691531） |

响应数据: 

| 参数名称 | 是否必须 | 数据类型   | 描述         | 取值范围           |
|------|------|--------|------------|----------------|
| code | true | string | 请求处理结果     | 1000,1001,1002 |
| msg  | true | string | 相关处理信息     |                |
| data | true | object | 单币最新价格相关数据 |                |

接口访问示例：https://vipapi.chainext.cn/v1/pegged?Fkey={apikey}&index_id=297&tstart=1558960800&tend=1559025600

需要apikey请联系我们

现有稳定币

| 币种名称                 | CID  | 官网页面                        |
|----------------------|------|-----------------------------|
| bitUSD               | 351  | http://bit.ly/BitShares_USD |
| Dai                  | 297  | https://makerdao.com/       |
| Gemini Dollar        | 1929 | https://gemini.com/dollar/  |
| Paxos Standard Token | 1927 | https://www.paxos.com/pax/  |
| sUSD                 | 1968 | https://www.synthetix.io/   |
| Tether               | 13   | https://tether.to/          |
| TrueUSD              | 481  | https://www.trusttoken.com/ |
| USD Coin             | 1928 | https://www.centre.io/usdc  |
| USDCoin              | 1969 | https://www.usc.us/         |


返回数据示例: 
```
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



## 指数最新数据列表 <span id="v1/index_realtime"> GET /index_realtime 获取所有指数最新数据



请求参数:

无

响应数据: 

| 参数名称         | 是否必须 | 数据类型   | 描述         | 取值范围           |
|--------------|------|--------|------------|----------------|
| code         | true | string | 请求处理结果     | 1000,1001,1002 |
| msg          | true | string | 相关处理信息     |                |
| data         | true | object | 单币最新价格相关数据 |                |
| updated_time | true | string | 数据更新时间     |                |

接口访问示例：https://api.chainext.io/v1/index_realtime

返回数据示例: 
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

## code返回类型

| code | msg               | 含义     |
|------|-------------------|--------|
| :-:  | :-:               | :-:    |
| 1000 | ""                | 返回成功   |
| 1001 | "data not ready"  | 没有返回数据 |
| 1002 | "wrong parameter" | 输入参数有误 |
