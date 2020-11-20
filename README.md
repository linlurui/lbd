# LBD商户平台接口文档

## 更新日志
上传于2020-11-20

## 接口说明
本平台采用标准RESTFult协议、jwt鉴权，使用前请先开通商户，开通商户账号请联系：18565679771。

## 服务器信息
以下URL的IP与端口采用变量表示，{ip}=服务器IP，{port}=端口，服务器信息请与平台联系

## 调用步骤
### 1. 收款
### 2. 代还


## 接口详情
### 1. 登录
* URL：http://{ip}:{port}/api/login 
* 请求方式：POST
* URL参数：无
* Headers: 无
* 提交参数：
```javascript
{
  "username": "linlurui",    //用户名
  "password": "12345678"     //密码
}
```
* 响应参数：
```javascript
{
    "data": {
        "userId": 15,
        "username": "linlurui",
        "password": "******",
        "createOn": "2020-11-16 22:03",
        "createBy": 1,
        "modifyOn": "2020-11-16 22:03",
        "modifyBy": 1,
        "type": "",
        "token": "eyJhbG.ciOiJIU.zI1NiJ9"   //登录成功返回的{token}需要填到headers的Authorization对应的选项值中用于鉴权
    },
    "message": "OK",
    "status": 0,                          //状态：操作成功返回0
    "uuid": "658081ff-372c-458b-a11a-0c798d32a440"
}
```

### 2. 商户进件（新增子商户）
* URL：http://{ip}:{port}/api/lbd/user 
* 请求方式：PUT
* URL参数：无
* Headers: Authorization: {token}
* 提交参数：
```javascript
{
  "idNo":"420814435435345435345",         //身份证号码
  "idName":"张三",                        //身份证姓名
  "phoneNo":"18566666666"                 //手机号码
}
```

* 响应参数：
```javascript
{
    "data": {
        "mercCd": "10000000123456789001"  //子商户号
    },
    "message": "OK",
    "status": 0
}
```

### 2. 结算卡绑卡
* URL：http://{ip}:{port}/api/lbd/debitcard 
* 请求方式：PUT
* URL参数：无
* Headers: Authorization: {token}
* 提交参数：
```javascript
{
  "cardNo":"4208144354353454353",         //银行卡号
  "cardMobile":"18566666666"              //银行卡预留手机号码
}
```

* 响应参数：
```javascript
{
    "message": "OK",
    "status": 0
}
```

### 3. 支付卡绑卡
* URL：http://{ip}:{port}/api/lbd/creditcard 
* 请求方式：PUT
* URL参数：无
* Headers: Authorization: {token}
* 提交参数：
```javascript
{
  "cardNo":"4208144354353454353",         //银行卡号
  "cardMobile":"18566666666",             //银行卡预留手机号码
  "cnlCd": "K010"                         //类型，收款＝"K010", 代还＝"D010"
}
```

* 响应参数：
```javascript
{
    "data": {
      "outOrderNo": "kkkb1f1236aa4f008e00610bab81299a" //订单ID，用于确认绑卡时的{id}参数
    },
    "message": "OK",
    "status": 0
}
```

### 4. 支付卡绑卡确认
* URL：http://{ip}:{port}/api/lbd/creditcard/{id} 
* 请求方式：PUT
* URL参数：{id}为支付绑卡时返回的outOrderNo
* Headers: Authorization: {token}
* 提交参数：
```javascript
{
  "smsCode":"123456",         //短信验证码
}
```

* 响应参数：
```javascript
{
    "message": "OK",
    "status": 0
}
```

### 5. 支付
* URL：http://{ip}:{port}/api/lbd/trans 
* 请求方式：PUT
* URL参数：无
* Headers:  Authorization: {token}
* 提交参数：
```javascript
{
  "data": {
    "outOrderNo": "kkkb1f1236aa4f008e00610bab81299a" //订单ID，支付订单的唯一标识
  },
  "cardNo":"4208144354353454353",         //信用卡卡号
  "cnlCd": "K010",                        //类型，收款＝"K010", 代还＝"D010"
  "amount": "120",                        //金额，必须大于100
  "settleCardNo": "4208144354353453333"   //收款卡号，收款必填项，代还不用填
}
```

* 响应参数：
```javascript
{
    "message": "OK",
    "status": 0
}
```

### 6. 结算(还款)
* URL：http://{ip}:{port}/api/lbd/settle 
* 请求方式：PUT
* URL参数：无
* Headers:  Authorization: {token}
* 提交参数：
```javascript
{
  "data": {
    "outOrderNo": "kkkb1f1236aa4f008e00610bab81299a" //订单ID，支付订单的唯一标识
  },
  "cardNo":"4208144354353454353",         //信用卡卡号
  "cnlCd": "K010",                        //类型，收款＝"K010", 代还＝"D010"
  "amount": "120"                        //金额，必须大于100
}
```

* 响应参数：
```javascript
{
    "message": "OK",
    "status": 0
}
```

### 7. 支付查询
* URL：http://{ip}:{port}/api/lbd/trans/{id} 
* 请求方式：GET
* URL参数：{id}为支付时返回的outOrderNo
* Headers:  Authorization: {token}
* 提交参数：无
* 响应参数：
```javascript
{
    "data": {
        "feeRate": "0.60",                //费率         
        "fixAmt": "2.00",                 //结算手续费
        "orderAmt": "105.00",             //订单金额
        "outOrderNo": "3c4dc01e347d4e6aaab71bed71f3fcf4",     //订单ID
        "settleSts": "01",                //结算状态，00：结算中 01：结算成功 02：结算失败
        "tranSts": "01"                   //订单状态，00：支付中，01支付成功，02支付失败
    },
    "message": "OK",
    "status": 0
}
```

### 8. 结算查询
* URL：http://{ip}:{port}/api/lbd/settle/{id} 
* 请求方式：GET
* URL参数：{id}为支付时返回的outOrderNo
* Headers:  Authorization: {token}
* 提交参数：无
* 响应参数：
```javascript
{
    "data": {
        "tranSts": "01", //订单状态，00：支付中，01支付成功，02支付失败
        "orderNo": "2000091300031512823",
        "amoumt": 9.45,
        "errCode": "0000",
        "errCodeDesc": "处理完成",
        "outOrderNo": "d2020091300001",
        "cardNo": "4033********8888"
    },
    "message": "OK",
    "status": 0
}
```

### 9. 绑卡查询
* URL：http://{ip}:{port}/api/lbd/creditcard/{id}?cnlCd={cnlCd} 
* 请求方式：GET
* URL参数：{id}为支付时返回的outOrderNo，{cnlCd}类型，收款＝"K010", 代还＝"D010"，例子：?cnlCd="K010"
* Headers:  Authorization: {token}
* 提交参数：无
* 响应参数：
```javascript
{
    "data": {
        "tranSts": "0",
        "orderNo": "20000916144835533798",
        "outOrderNo": "11000000000",
        "cardNo": "4033********3850",
        "mercCd": "10000000916143600001"
    },
    "message": "OK",
    "status": 0
}
```

### 10. 绑卡列表查询
* URL：http://{ip}:{port}/api/lbd/creditcard
* 请求方式：POST
* URL参数：无
* Headers:  Authorization: {token}
* 提交参数：
```javascript
{
    "cnlCd": "D010"     //类型，收款＝"K010", 代还＝"D010"
}
```
* 响应参数：
```javascript
{
    "data": {
        "cardList": [
            {
                "acctName": "周一八",
                "cardNo": "6212264000032173000",
                "cardType": "1",
                "idNo": "420115199001010911",
                "payChannel": "R16",
                "phoneNo": "18672195279",
                "tranSts": "0"
            },
            {
                "acctName": "周一八",
                "cardNo": "4033910025893850",
                "cardType": "2",
                "idNo": "420115199001010911",
                "cnlCd": "R16",
                "phoneNo": "18672195279",
                "tranSts": "0"
            }
        ]
    },
    "message": "OK",
    "status": 0
}
```

### 11. 余额查询(注意：代还未结算的才能查到余额，收款的实时到账，不能查询余额)
* URL：http://{ip}:{port}/api/lbd/balance
* 请求方式：POST
* URL参数：无
* Headers:  Authorization: {token}
* POST参数：
```javascript
{
    "cnlCd": "D010"     //类型，收款＝"K010", 代还＝"D010"
}
```
* 响应参数：
```javascript
{
    "data": {"availBalance":"0"},
    "message": "OK",
    "status": 0
}
```
