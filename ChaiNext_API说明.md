# ChaiNext API 接口说明文档
关于ChaiNext API 接口的使用说明文档。
## ChaiNext API 简介
ChaiNext为用户提供了一套行情查询的API接口，旨在帮助用户快速、高效地查询和了解实时行情，获取相关信息。

目前ChaiNext API提供以下功能：
* 获取CSI系列指数信息、指数基本行情以及指数表现
* 获取CSI系列指数中币种的权重系数
* 获取CSI系列指数K线图
* 获取CSI系列指数的CID与指数名称映射表
* 获取单币的CID与单币名称映射表
* 获取CSI系列指数每日播报
* 获取CSI系列指数整点播报
* 获取CSI系列指数分钟级监控信息
* 获取CSI系列指数小时级监控信息
* 获取代币大额转账报警信息

API访问地址：

国内用户请访问：[https://api.chainext.cn/v1](https://api.chainext.io/v1)

海外用户请访问：[https://api.chainext.io/v1](https://api.chainext.io/v1)


## API 接口说明
| 接口数据类型 | 请求方法 | 类型     | 描述  |
| ------------ | ----- | ------ | ----- |
|基本指数行情|[https://api.chainext.io/v1/index_basic](#v1/index_basic)|GET|获取指数的基本行情|
|权重|[https://api.chainext.io/v1/weight](#v1/weight)|GET|获取指数的权重信息|
|指数列表|[https://api.chainext.io/v1/index_list](#v1/index_list)|GET|获取指数列表信息|
|指数表现|[https://api.chainext.io/v1/index_detail](#v1/index_detail)|GET|获取指数在指定时段段内的表现相关信息|
|K线图|[https://api.chainext.io/v1/kchart](#v1/kchart)|GET|获取指数K线图|
|指数CID映射表|[https://api.chainext.io/v1/mapping_list](#v1/mapping_list)|GET|获取指数CID与指数名称的相关说明|
|单币CID映射表|[https://api.chainext.io/v1/coin_mapping_list](#v1/coin_mapping_list)|GET|获取单币CID与单币名称的相关说明|
|微信每日播报|[https://api.chainext.io/v1/wechat_broadcast](#v1/wechat_broadcast)|GET|获取每日播报信息|
|微信整点播报|[https://api.chainext.io/v1/wechat_hour_broadcast](#v1/wechat_hour_broadcast)|GET|获取整点播报信息|
|微信分钟级监控|[https://api.chainext.io/v1/wechat_monitor_min](#v1/wechat_monitor_min)|GET|获取指数分钟级监控信息|
|微信小时级监控|[https://api.chainext.io/v1/wechat_monitor_24h](#v1/wechat_monitor_24h)|GET|以utc0时间为基准，获取当日的CSI指数涨跌幅报警信息|
|代币大额转账报警|[https://api.chainext.io/v1/largement_alert](#v1/largement_alert)|GET|获取代币大额转账报警信息|



####<span id="v1/index_basic"> GET /index_basic 获取基本指数行情
请求参数: 

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | string | 指数CID或指数名称  | 1 |由指数CID范围决定|
响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |基本指数行情数据|      |
| updated_time| true | string |数据更新时间|      |

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

####<span id="v1/weight"> GET /weight 获取指数的权重信息
请求参数: 

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | string | 指数CID或指数名称  | 1 |由指数CID范围决定|

响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |指数权重数据|      |
| updated_time| true | string |数据更新时间|      |

接口访问示例：https://api.chainext.io/v1/weight?id=csi100

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

####<span id="v1/index_list"> GET /index_list 获取指数列表信息
请求参数: 

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| page       | true  | integer | 页码 | 1 |由指数数量决定|
| page_size       | true  | integer | 每页数量  | 20 |由指数数量决定|

响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |指数列表数据|      |
| updated_time| true | string |数据更新时间|      |

接口访问示例：https://api.chainext.io/v1/index_list?page=1&page_size=20

返回数据示例: 
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
####<span id="v1/index_detail"> GET /index_detail 获取指数表现相关信息

请求参数:

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | integer | 指数CID | 1 |指数范围内|
| tstart       | true  | integer | 开始时间 | |Unix时间戳（单位：秒，例如：1530691531）|
| tend       | true  | integer | 结束时间 | |Unix时间戳（单位：秒，例如：1530691531）|

响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |指数表现相关数据|      |

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
####<span id="v1/kchart"> GET /kchart 获取指数K线图

请求参数:

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id       | true  | integer | 指数CID | 1 |指数范围内|
| tstart       | true  | integer | 开始时间 | |Unix时间戳（单位：秒，例如：1530691531）|
| tend       | true  | integer | 结束时间 | |Unix时间戳（单位：秒，例如：1530691531）|
| grouping       | true  | string | 时间间隔 | |1min,5min,15min,30min,1H,1D,1w|

响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |指数K线图|      |

接口访问示例：https://api.chainext.io/v1/kchart?id=4&grouping=1H&tstart=1526798662&tend=1531983011

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
      ],  # 数据分别为unix时间戳，开盘价，收盘价，最高价，最低价，交易额    
      ...
    ]
  }
}
```
####<span id="v1/mapping_list"> GET /mapping_list 获取指数CID与指数名称的相关说明

请求参数:

无。

响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |指数CID与指数名称数据|      |

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
####<span id="v1/coin_mapping_list"> GET /coin_mapping_list 获取单币CID与单币名称的相关说明

请求参数:

无。

响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |单币CID与单币名称数据|      |

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

####<span id="v1/wechat_broadcast"> GET /wechat_broadcast 获取每日播报信息

请求参数:

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| date      | true  | string | 查询日期，格式 2018-07-24 | ||


响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |每日播报信息|      |

接口访问示例：https://api.chainext.io/v1/wechat_broadcast?date=2018-08-02

返回数据示例: 
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
####<span id="v1/wechat_hour_broadcast"> GET /wechat_hour_broadcast 获取整点播报信息

请求参数:

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | 指数CID或指数名称 | ||
| date      | true  | string | 查询日期，格式 2018-07-24 | ||


响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |整点播报信息|      |

接口访问示例：https://api.chainext.io/v1/wechat_hour_broadcast?id=11&date=2018-08-02

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
        "time": "2018-08-02 10:00:26",
        "content": 	"指数点位整点播报 北京时间2018年08月02日10:00，「CSI100」指数报1020.38点,全日涨跌幅为0.84%。成分币中77上涨，23下跌。涨幅居前为「WTC」(19.97%)、「PAY」(9.49%)、「ARDR」(5.51%)。\r\n\r\n「CSI100」：CSI系列指数中的\"上证综指\"，样本由规模和流动性排名前100的通证组成，市值覆盖率达96%，反映了通证市场整体走势。\r\n本信息由企业级数字货币指数服务商ChaiNext提供。\r\nhttps://chainext.io|微信公众号ChaiNext"
        }
      ]
    }
  ]
}
```
####<span id="v1/wechat_monitor_min"> GET /wechat_monitor_min 获取指数分钟级监控信息

请求参数:

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | 指数CID或指数名称 | ||
| date      | true  | string | 查询日期，格式 2018-07-24 | ||


响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |指数分钟级监控信息|      |

接口访问示例：https://api.chainext.io/v1/wechat_monitor_min?id=csi100&date=2018-08-02

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
        "time": "2018-08-02 10:00:26",
        "content": 	"CSI指数快速波动预警\r\n2018年08月02日06时09分-06时19分,CSI100指数10min快速上涨1.22%,目前报1005.17点。\r\n成分币中8上涨，92下跌。涨幅居前为「PPT」(9.45%)、「BCD」(3.84%)、「DOGE」(2.30%)。\r\n\r\n「CSI100」：CSI系列指数中的\"上证综指\"，样本由规模和流动性排名前100的通证组成，市值覆盖率达96%，反映了通证市场整体走势。\r\n\r\n本信息由企业级数字货币指数服务商ChaiNext提供。\r\nhttps://chainext.io|微信公众号ChaiNext"
        }
      ]
    }
  ]
}
```

####<span id="v1/wechat_monitor_24h"> GET /wechat_monitor_24h 以utc0时间为基准，获取当日的CSI指数涨跌幅报警信息

请求参数:

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | 指数CID或指数名称 | ||
| date      | true  | string | 查询日期，格式 2018-07-24 | ||


响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |CSI指数涨跌幅报警信息|      |

接口访问示例：https://api.chainext.io/v1/wechat_monitor_24h?id=csi100&date=2018-08-01

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
        "time": "2018-08-01 07:19:55",
        "content": "CSI指数行情大幅涨跌预警\r\n北京时间2018年08月01日07时19分,CSI100指数今日（UTC0起）累计下跌-5.49%,目前报1026.24点。\r\n其中,成分币中2上涨,98下跌。其中,涨幅居前为「BNB」(5.92%)。「XVG」(0.44%)。\r\n\r\n「CSI100」：CSI指数系列中的\"上证综指\"，样本由规模和流动性排名前100的通证组成，市值覆盖率达96%，反映了通证市场整体走势。\r\n\r\n本信息由企业级数字货币指数服务商ChaiNext提供。\r\nhttps://chainext.io|微信公众号ChaiNext"
        }
      ]
    }
  ]
}
```
####<span id="v1/largement_alert"> GET /largement_alert 获取代币大额转账报警信息

请求参数:

| 参数名称 | 是否必须  | 类型     | 描述  | 默认值   | 取值范围  |
| ------------ | ----- | ------ | ----- | ----- | ------- |
| id      | true  | integer | 见单币CID映射表 | ||
| date      | true  | string | 查询日期，格式 2018-07-24 | ||


响应数据: 

| 参数名称   | 是否必须 | 数据类型   | 描述   | 取值范围   |
| ------ | ---- | ------ | ----------- | ------ |
| code | true | string | 请求处理结果    |1000,1001,1002|
| msg     | true | string |相关处理信息|    |
| data   | true | object |代币大额转账报警信息|      |

接口访问示例1：https://api.chainext.io/v1/largement_alert?id=0&date=2018-07-31
接口访问示例1：https://api.chainext.io/v1/largement_alert

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
        "time": "2018-08-01 07:19:55",
        "content": "代币大额转账报警\r\n\r\nUTC0时间07月31日06时13分(北京时间07月31日14时13分)\r\n\r\nBTC发生数量为1297.95的大额转账交易（tx为8310336887225ae3248644201a406d23db0e7f8a7efa1c499b3fdc4079f6bcf2），转出方未知，转入方包含其他（共计1297.95个，100%）\r\n\r\n想了解更多详细信息，请登录ChaiNext官网https://chainext.io查询|微信公众号ChaiNext"
        }
      ]
    }
  ]
}
```
