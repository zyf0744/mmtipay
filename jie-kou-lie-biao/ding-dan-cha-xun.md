# 接口介绍 {#接口介绍}

根据商户订单号或者采宝订单号来查询订单。

# 参数简介 {#参数简介}

| 参数名 | 参数类型 | 参数介绍 | 是否必填 | 是否参与签名 |
| :--- | :--- | :--- | :--- | :--- |
| command | String | 接口名，用于标识调用哪个接口，条码支付取值为：open.pay.query | 是 | 否 |
| operator\_id | String | 收银员的id，用于标识收款账户 | 是 | 是 |
| app | String | 接入商标识 | 是 | 是 |
| sign | String | 签名，详见签名规则 | 是 | 否 |
| local\_order\_no | String | 接入方的本地订单号 | 否，与order\_no二选一 | 是 |
| order\_no | String | 采宝订单号 | 否，与local\_order\_no二选一，优先级: order\_no &gt; local\_order\_no | 是 |
| timestamp | Long | 时间戳，值为当前时间距离19700101的毫秒数 | 是 | 是 |

# 返回值说明 {#返回值说明}

```
{
    "result": {
        "success": false,
        "errorCode":"10",
        "errorMsg": "command参数为空"
    }
    "data":{
        "localOrderNo":"",##本地订单号，参与签名
        "cbOrderNo":"",##采宝的订单号，参与签名
        "outOrderNo":"",##微信、支付宝、百度钱包、翼支付等服务商的订单号，参与签名
        "orderStatus":"", ## 订单状态
        "subject":"", ## 订单描述
        "paymentChannel":"", ##支付渠道，参与签名
        "paymentWay":"", ##支付方式，参与签名
        "payTime":"",## 支付方式
        "totalAmount":"",## 总额(分为单位)，参与签名
        "receiveAmount":"", ## 收到的金额（分为单位）
        "refundAmount":"",##退款金额
        "refundTime":""##退款时间
        ,"sign":"" ## 签名值
        ,"timestamp":"" ## 时间戳，参与签名
        ##===========以下字段只有version大于等于1.1时才会返回========
        ,"discountAmount":""##优惠金额
    }
}

```

# js demo {#js-demo}

[http://openapi.caibaopay.com/test/api/query.htm](http://openapi.caibaopay.com/test/api/query.htm)

