# ChaiNext API 接口说明文档
关于ChaiNext API 接口的使用说明文档。
中文版：[ChaiNext_API说明](https://github.com/chainext/ChaiNext_API/blob/master/ChaiNext_API%E8%AF%B4%E6%98%8E.md)
english version：[ChaiNext_API_instruction.md](https://github.com/chainext/ChaiNext_API/blob/master/ChaiNext_API_instruction.md)

# API接入地址 api interface url
* normal
  * china mainland ：api.chainext.cn
  * others: api.chainext.io
* vipapi (direct connect, Low delay and high availability)
  * china mainland ：vipapi.chainext.cn
  * others: vipapi.chainext.io
  
**sent email to us if you want to use vipapi,  whuxuanyuanlei@gmail.com, or you can contact us by wechat, search lulumentor**


## 修订记录

* 2018-08-02 生成文档
* 2018-08-03 修订接口请求说明
* 2018-08-10 发布英文版本的api
* 2018-08-16 增加tradingview的接口
* 2018-09-16 [系列的接口升级](https://github.com/chainext/ChaiNext_API/blob/master/upgrade_records/20180916)
* 2018-10-15 增加coin_list_all的接口文档
* 2019-05-28 增加pegged的接口文档

## ChaiNext指数index_code字段修改公告

* ChaiNext计划于`2019年9月23日`，将指数index_code字段中所有"csi"改为为"ChaiNext"（例如：原‘csi5’将改为‘ChaiNext5’），请对接时使用了index_code处理逻辑的客户检查相关逻辑是否仍然生效，对于由此给您带来的不便我们深表歉意，敬请谅解。

* 所涉及的接口为
    * [/v1/index_basic](https://api.chainext.io/v1/index_basic)
    * [/v1/mapping_list](https://api.chainext.io/v1/mapping_list)
    * [/v1/index_realtime](https://api.chainext.io/v1/index_realtime)
    * [/v1/index_list (symbol字段)](https://api.chainext.io/v1/index_list)

> ps：ChaiNext建议对接指数时用index_id作为唯一标识处理逻辑，避免今后类似修改影响数据获取及处理逻辑。
