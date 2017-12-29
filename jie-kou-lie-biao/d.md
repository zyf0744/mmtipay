# 接口介绍 {#接口介绍}

目前该接口仅支持微信官方通道收款，其他收款渠道（银行等），正在加紧研发中。

该接口对应着微信官方的公众号支付， 用于大家想自己在公众号里定制自己的收款页面（而不用经过我们的中间页，详情见H5支付）。

要想使用此接口，需要先在采宝开通微信官方通道收款，并联系客服小二配置支付关注紫的公众号。

# 参数简介 {#参数简介}

| 参数名 | 参数类型 | 参数介绍 | 是否必填 | 是否参与签名 |
| :--- | :--- | :--- | :--- | :--- |
| command | String | 接口名，用于标识调用哪个接口，条码支付取值为：open.pay.mp | 是 | 否 |
| operator\_id | String | 收银员的id，用于标识收款账户 | 是 | 是 |
| app | String | 接入商标识 | 是 | 是 |
| version | String | 接口版本号，默认值1.0 | 是 | 否 |
| sign | String | 签名，详见签名规则 | 是 | 否 |
| local\_order\_no | String | 接入方的本地订单号，接入方请保证这个订单号的唯一性， 采宝进行唯一性校验，如果订单号不唯一，会影响查询结果 | 否 | 是 |
| amount | Long | 订单总额，以分为单位 | 是 | 是 |
| un\_discount\_amount | Long | 不参与优惠金额，以分为单位 | 否 | 是 |
| timestamp | Long | 时间戳，值为当前时间距离19700101的毫秒数 | 是 | 是 |
| subject | String | 订单描述，小于20个汉字 | 否 | 是 |
| goods\_list | String | 商品列表 | 否 | 是 |
| notify\_url | String | 支付成功之后的回调地址，具体请参照：支付完成之后的通知 | 否 | 否 |
| sub\_app\_id | String | 配置的支付关注的公众号的app\_id | 是 | 是 |
| open\_id | String | 付款人在sub\_app\_id对应的公众号下的openId | 是 | 是 |
| device\_create\_ip | String | 发起支付服务器或终端IP地址，格式为8.8.8.8 | 否 | 是 |

# goods\_list 介绍 {#goodslist-介绍}

goods\_list是商品列表信息， 传入此值后会自动统计商品的销量等信息，并且会被放入订单中。 格式为json格式， 举例如下：

```
[
    {
        "goods_id":"", ## 商品id,可空
        "goods_num":"", ## 商品编号，这个值用于传入到微信、支付宝等， 用于支持单品券的核销，可空
        "goods_name":"", ## 商品名称，可空
        "sell_amount":"", ## 卖出数量，不可为空
        "goods_price":"",  ## 商品单价，不可为空
        "goods_sku_id":"" ## 卖出的sku的id，可空
    },
    {
        "goods_id":"", ## 商品id,可空
        "goods_num":"", ## 商品编号，这个值用于传入到微信、支付宝等， 用于支持单品券的核销，可空
        "goods_name":"", ## 商品名称，可空
        "sell_amount":"", ## 卖出数量，不可为空
        "goods_price":"",  ## 商品单价，不可为空
        "goods_sku_id":"" ## 卖出的sku的id，可空
    },
    {
        "goods_id":"", ## 商品id,可空
        "goods_num":"", ## 商品编号，这个值用于传入到微信、支付宝等， 用于支持单品券的核销，可空
        "goods_name":"", ## 商品名称，可空
        "sell_amount":"", ## 卖出数量，不可为空
        "goods_price":"",  ## 商品单价，不可为空
        "goods_sku_id":"" ## 卖出的sku的id，可空
    }
    ......
]

```

# 返回值说明 {#返回值说明}

返回值请参照：[https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7\_7&index=6](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_7&index=6)

```
{
        "result": {
               "success": false,
                "errorCode":"10",
                "errorMsg": "command参数为空"
        }
        "data":{
            "appId":"",##参与签名
            "timeStamp":"",##参与签名
            "nonceStr":"",##参与签名
            "package":"",##参与签名
            "signType":"",##参与签名
            "paySign":"",##参与签名
            "sign":"", ## 签名值
            "timestamp":"" ## 时间戳，参与签名
        }
}
```



