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
        "token": "eyJhbGciOiJIUzI1NiJ9.eyJhbGciOiJIUzI1NiJ9.eyJhbGciOiJIUzI1NiJ9"   //登录成功返回的{token}需要填到headers的Authorization对应的选项值中用于鉴权
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
    "succ": true,                         //成功
    "returnCode": "0000",                 //成功返回0000
    "returnInfo": "商户进件成功",          //消息
    "returnData": {                       //返回数据节点
        "mercCd": "10000000123456789001"  //子商户号
    }
}
```

### 2. 结算卡绑卡（适用于K010）
* URL：http://{ip}:{port}/api/lbd/debitcard 
* 请求方式：PUT
* URL参数：无
* Headers: 
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
    "succ": true,                         //成功
    "returnCode": "0000",                 //成功返回0000
    "returnInfo": "商户进件成功",          //消息
    "returnData": {                       //返回数据节点
        "mercCd": "10000000123456789001"  //子商户号
    }
}
```

