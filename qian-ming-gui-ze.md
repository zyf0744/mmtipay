## 签名方法 {#签名方法}

我们采用了MD5的签名方法。

## 签名规则 {#签名规则}

1. 构造待签名字符串。待签名字符的生成规则如下：
   1. 所有参与签名的请求参数都按照名称字符升序排列\(参数名称不允许相同\)
   2. 如果参数值带有中文， 需要制定字符集编码为UTF-8
   3. 如果参数值为空，那么该参数不参与签名
   4. 将采宝的合作秘钥作为最后一个参数， 参数名为：key, 参数值就是采宝的合作秘钥本身
   5. 将请求参数按上述顺序用\`
      &
      \`拼接起来
2. 用MD5算法，对待签名字符串进行加密， 生成的签名数据（32位小写字符）， 就是公共参数中
   `sign`
   的值。

## 签名示例 {#签名示例}

大家可以根据这个示例，来验证自己的签名结果是否正确。

现有如下参数参与签名：

| 参数名 | 参数值 |
| :--- | :--- |
| barcode | 123123123123 |
| local\_order\_no | localorderno123123123123 |
| app | zyptestapp |
| operator\_id | axgdfdafd34124 |
| amount | 100 |
| un\_discount\_amount |  |
| timestamp | 1460512556270 |
| subject | 这是一笔支付订单 |
|  | goods\_list |

那么生成的待签名字符串为（合作秘钥的值设为：thisistestkey）：

> amount=100&app=zyptestapp&barcode=123123123123&local\_order\_no=localorderno123123123123&operator\_id=axgdfdafd34124&subject=这是一笔支付订单&timestamp=1460512556270&key=thisistestkey

注：因为`un_discount_amount`和`goods_list`两个参数的值为空，所以没有参与签名

签名结果为:

> 37fd31004368f9e616f277c6436985eb

## md5签名方法示例\(java\) {#md5签名方法示例java}

```
/**
 * 使用md5算法进行加密
 *
 * @param target
 *            要加密的字符串
 * @param charset
 *            编码（请设置为UTF-8)
 * @return 加密后的字符串
 */
public static String encryptWithMD5(String target,String charset) {
    String md5Str = null;
    try {
        MessageDigest md5 = MessageDigest.getInstance("MD5");
        md5.reset();
        byte[] bytes = md5.digest(charset==null?target.getBytes():target.getBytes(charset));
        StringBuffer stringBuffer = new StringBuffer();
        for (byte b : bytes) {
            int bt = b 
&
 0xff;
            if (bt 
<
 16) {
                stringBuffer.append(0);
            }
            stringBuffer.append(Integer.toHexString(bt));
        }
        md5Str = stringBuffer.toString();
    } catch (Exception ex) {
        logger.error("encrypt error,target:" + target, ex);
    }
    return md5Str;
}

```

## 生成签名串并签名的方法示例 {#生成签名串并签名的方法示例}

```
/**
 * 对params中的参数进行排序后生成签名串
 * @param params 参与签名的参数map
 * @param key 签名要用到的加密串
 * @return
 */
String sign=null;
    StringBuffer sb = new StringBuffer();
    //排序
    List
<
Map.Entry
<
String, String
>
>
 infoIds =
            new ArrayList
<
Map.Entry
<
String, String
>
>
(params.entrySet());
    Collections.sort(infoIds, new Comparator
<
Map.Entry
<
String, String
>
>
() {
        public int compare(Map.Entry
<
String, String
>
 o1, Map.Entry
<
String, String
>
 o2) {
            return (o1.getKey()).toString().compareTo(o2.getKey());
        }
    });
    //对参数数组进行按key升序排列,然后拼接，最后调用5签名方法
    int size  = infoIds.size();
    for(int i = 0; i 
<
 size; i++) {
        if(CheckUtil.isNotEmpty(infoIds.get(i).getValue())) {//不为空，为空的不参与签名
            sb.append(infoIds.get(i).getKey() + "=" + infoIds.get(i).getValue() + "
&
");
        }
    }
    String newStrTemp = sb.toString()+"key="+key.trim();
    //获取sign_method

    sign = EncryptionUtil.encryptWithMD5(newStrTemp,"UTF-8");

    return sign;
```



