# 接口介绍 {#接口介绍}

本接口用于支付成功之后的通知，支付完成后采宝会将如下参数post到相关地址。

收到本接口的回调数据后，请异步处理订单逻辑， 并返回\`success\`字符串（必须完全相同，不能有任何其他字符），否则采宝会尝试进行重试，重试时间会不断加长。

# 参数简介 {#参数简介}

| 参数名 | 参数介绍 |
| :--- | :--- |
| cbOrderNo | 采宝的订单号，最长64位 |
| appOrderNo | 调用方自己生成的订单号 |
| outOrderNo | 微信或支付宝产生的订单号 |
| orderStatus | 订单状态，详情参照：订单状态详解 |
| totalAmount | 订单总额，以分为单位 |
| receiveAmount | 实收金额，以分为单位 |
| paymentChannel | 支付渠道, 详情参照：支付渠道详解 |
| subject | 订单简介 |
| discountAmount | 优惠金额，以分为单位 |
| paymentWay | 支付方式，详情参照：支付方式详解 |
| payTime | 支付时间，数字格式，值为距离1970.1.1日的毫秒数 |
| sign | 签名 |

# 验签 {#验签}

为了保证接口的安全，请收到我们的的回调之后进行验签操作。

1. 签名数据由除
   `sign`
   之外的所有请求参数按以下规则拼接而成
   1. 所有参与签名的请求参数都按照名称字符升序排列\(参数名称不允许相同\)
   2. 某些请求参数的值是允许包含中文的,为了避免中文的编码问题,我们规定所有带中文的参数的值必须按照UTF-8格式进行编码。
   3. 如果参数值为空，那么则该参数不参与签名
   4. 将请求参数按上述顺序用 
      &
       拼接起来
2. 参数签名使用了
   `RSA2`
   [签名算法](https://doc.open.alipay.com/docs/doc.htm?spm=a219a.7629140.0.0.ox3SZM&treeId=291&articleId=106103&docType=1)
   ，采宝使用私钥进行了签名，请使用采宝的公钥进行验签。 采宝的公钥为：
   ```
   MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAq+iElxN5xzGpN81gjLSzTROPWvYw+06YPyjG5bufC2NHjoaiISbdw6AnYcdIAT8g5dOgYB4SyDPSxvfje2k9CTUFbmNTTm5humwwbCz94UVJf6XwAWT1432WtW1VtrC3tK3BTM5v1rY4Bt7yjQPD/ao4ZGe/RsVOYIT7KGD8g/eLLuWPMcCJmCA0P8Vl65ouS3ioReLMWdEFwTGUNeWfA14/ki9Z+p1ldSz1uq+YE1eoYF18kyF3nlQbIjHdBhk9bRhodLBLrHP0SndawDUy6cdO7YbCsP2utYGVkWTxrCezszPhtGDfP9Jvvtw1J1yKCPNtfbDOz1uczhBO/u6P6QIDAQAB

   ```

# 订单状态详解 {#订单状态详解}

| 状态值 | 解释 |
| :--- | :--- |
| WAIT\_PAY | 等待支付 |
| PAY\_SUC | 支付成功 |
| REFUNDING | 退款中 |
| PART\_REFUND | 部分退款 |
| ALL\_REFUND | 全部退款 |
| CANCEL | 已取消 |
| PAY\_FAIL | 付款失败 |

# 支付渠道详解 {#支付渠道详解}

| 状态值 | 解释 |
| :--- | :--- |
| ALIPAY | 支付宝 |
| WECHAT | 微信 |

# 支付方式详解 {#支付方式详解}

| 状态值 | 解释 |
| :--- | :--- |
| BARCODE | 条码支付 |
|  | QRCODE |



