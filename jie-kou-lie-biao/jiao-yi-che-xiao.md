# 接口介绍 {#接口介绍}

撤销接口。

# 参数简介 {#参数简介}

| 参数名 | 参数类型 | 参数介绍 | 是否必填 | 是否参与签名 |
| :--- | :--- | :--- | :--- | :--- |
| command | String | 接口名，用于标识调用哪个接口，条码支付取值为：open.pay.reverse | 是 | 否 |
| operator\_id | String | 收银员的id，用于标识收款账户 | 是 | 是 |
| app | String | 接入商标识 | 是 | 是 |
| sign | String | 签名，详见签名规则 | 是 | 否 |
| local\_order\_no | String | 接入方的本地订单号 | 否，与order\_no二选一 | 是 |
| order\_no | String | 采宝订单号 | 否，与local\_order\_no二选一，优先级：order\_no &gt; local\_order\_no | 是 |
| timestamp | Long | 时间戳，值为当前时间距离19700101的毫秒数 | 是 | 是 |

# 返回值说明 {#返回值说明}

```
{
    "result": {
        "success": false,
        "errorCode":"10",
        "errorMsg": "command参数为空"
    }, 
    "data":{
        "sign":"" ## 签名值
        ,"timestamp":"" ## 时间戳，参与签名
    }
}

```

# 特殊说明 {#特殊说明}

如下几种情况，撤销将会返回失败：

| 情形介绍 | errorMsg |
| :--- | :--- |
| 订单已经付款成功 | 当前订单已经收款成功，无法执行撤销。您可以使用刷新功能同步订单最新状态！ |
| 全额退款订单 | 当前订单已经全额退款，无法执行撤销！ |
| 交易失败的订单 | 交易失败的订单无法进行撤销！ |
| 非付款类型订单（例如退款） | 此订单不支持撤销操作，请查证（只有付款订单才可以撤销）！ |

# js demo {#js-demo}

[http://openapi.caibaopay.com/test/api/reverse.htm](http://openapi.caibaopay.com/test/api/reverse.htm)

