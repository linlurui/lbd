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
  "username": "linlurui",
  "password": "12345678"
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
* Headers: 无
** Authorization: {token}
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
* Headers: 
*** Authorization: {token}
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
* Headers: 
** Authorization: {token}
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
* Headers: 
** Authorization: {token}
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
* URL参数：{id}为支付绑卡时返回的outOrderNo
* Headers: 
** Authorization: {token}
* 提交参数：
```javascript
{
  "cardNo":"4208144354353454353",         //信用卡卡号
  "cnlCd": "K010",                        //类型，收款＝"K010", 代还＝"D010"
  "amount": "120",                        //金额，必须大于100
  
}
```

* 响应参数：
```javascript
{
    "message": "OK",
    "status": 0
}
```
