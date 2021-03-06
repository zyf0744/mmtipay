# 接口介绍 {#接口介绍}

四码合一的条码支付接口， 本接口会根据条码自动选择支付方式并完成支付。

# 参数简介 {#参数简介}

| 参数名 | 参数类型 | 参数介绍 | 是否必填 | 是否参与签名 |
| :--- | :--- | :--- | :--- | :--- |
| command | String | 接口名，用于标识调用哪个接口，条码支付取值为：open.pay.barcode | 是 | 否 |
| operator\_id | String | 收银员的id，用于标识收款账户 | 是 | 是 |
| app | String | 接入商标识 | 是 | 是 |
| version | String | 接口版本号，默认1.0，当前值只能为1.0和1.1会影响返回值，详情请见返回值部分 | 是 | 否 |
| sign | String | 签名，详见签名规则 | 是 | 否 |
| local\_order\_no | String | 接入方的本地订单号，接入方请保证这个订单号的唯一性， 采宝不进行唯一性校验，如果订单号不唯一，会影响查询结果 | 是 | 是 |
| barcode | String | 用户微信或支付宝的付款码 | 是 | 是 |
| amount | Long | 订单总额，以分为单位 | 是 | 是 |
| un\_discount\_amount | Long | 不参与优惠金额，以分为单位 | 否 | 是 |
| timestamp | Long | 时间戳，值为当前时间距离19700101的毫秒数 | 是 | 是 |
| subject | String | 订单描述，小于20个汉字 | 否 | 是 |
| goods\_list | String | 商品列表 | 否 | 是 |

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

```
{
        "result": {
               "success": false,
                "errorCode":"10",
                "errorMsg": "command参数为空"
        }
        "data":{
                "localOrderNo":""##本地订单号，参与签名      
                ,"cbOrderNo":""##采宝的订单号，最长64位，参与签名
                ,"outOrderNo":"" ##支付宝、微信等的订单id，最长64位，参与签名
                ,"orderStatus":""##支付状态
                ,"totalAmount":""##订单金额，参与签名
                ,"receiveAmount":""## 收款金额
                ,"paymentChannel":"",##支付渠道，1支付宝，2微信，3百度钱包，4翼支付，参与签名
                ,"sign":"" ## 签名值
                ,"timestamp":"" ## 时间戳，参与签名
                ##===========以下字段只有version大于等于1.1时才会返回========
                ,"subject":"" ## 订单主题
                ,"discountAmount":""##优惠金额
                ,"paymentWay":""##付款方式
                ,"payTime":""##付款时间
        }
}

```

# js demo {#js-demo}

[http://openapi.caibaopay.com/test/api/barcode.htm](http://openapi.caibaopay.com/test/api/barcode.htm)

