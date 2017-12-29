# 接口介绍 {#接口介绍}

退款接口。

# 参数简介 {#参数简介}

| 参数名 | 参数类型 | 参数介绍 | 是否必填 | 是否参与签名 |
| :--- | :--- | :--- | :--- | :--- |
| command | String | 接口名，用于标识调用哪个接口，条码支付取值为：open.pay.refund | 是 | 否 |
| operator\_id | String | 收银员的id，用于标识收款账户 | 是 | 是 |
| app | String | 接入商标识 | 是 | 是 |
| sign | String | 签名，详见签名规则 | 是 | 否 |
| local\_order\_no | String | 接入方的本地订单号 | 否，与order\_no二选一 | 是 |
| order\_no | String | 采宝订单号 | 否，与local\_order\_no二选一，优先级：order\_no &gt; local\_order\_no | 是 |
| timestamp | Long | 时间戳，值为当前时间距离19700101的毫秒数 | 是 | 是 |
| refund\_amount | Long | 退款金额，如果为空，那么默认全部退款 | 否 | 否 |
| reason | String | 退款原因 | 否 | 是 |

# 返回值说明 {#返回值说明}

```
{
    "result": {
        "success": false,
        "errorCode":"10",
        "errorMsg": "command参数为空"
    }    
    "data":{
        "refundStatus":"", ##退款状态，参与签名
        "localOrderNo":"",##本地退款订单号，参与签名
        "cbOrderNo":"",##采宝的订单号，参与签名
        "outOrderNo":"", ##支付宝，微信等的外部订单号，参与签名
        "refundAmount":"" ##退款金额，参与签名
        ,"sign":"" ## 签名值
        ,"timestamp":"" ## 时间戳，参与签名
    }
}

```

# js demo {#js-demo}

[http://openapi.caibaopay.com/test/api/refund.htm](http://openapi.caibaopay.com/test/api/refund.htm)

