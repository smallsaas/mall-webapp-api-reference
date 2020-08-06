## 钱包API

### 我的钱包

GET https://mall.smallsaas.cn/rest/wallet?phone=1380000001 

Param: 
- -phone: 可选，要查看的会员手机号码，管理员可以根据这个参数查看该用户的钱包

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "accumulative_amount": 0, //累计金额
        "accumulative_gift_amount": 0, //累计赠送
        "balance": 0, //余额
        "user_id": 1,
        "gift_balance": 0, //赠送余额
        "id": 1
    }
}
```

### 钱包充值

POST https://mall.smallsaas.cn/rest/wallet_charge 

> 充值后调用 支付 页面接口 /payment/wpay/:id?orderType=Wallet

Header: Authorization: token

Data:
```
{
    "id"; 1, // depoist package id
    "amount": 121, //充值金额
    "description": "xxyy" //描述
}
```

Return:
```
{
    "status_code": 0,
    "data": {
        "created_time": "2018-08-08",
        "wallet_id": 1,
        "amount": 121,
        "description": "xxyy",
        "id": 1,
        "gift_amount": 0,
        "status": "PAY_PENDING"
    }
}
```

### 钱包流水记录

GET https://mall.smallsaas.cn/rest/wallet_history?pageNumber=1&pageSize=30 

Header: Authorization: token

> amount 本次充值额。 balance 本次充值后账户的余额。 gift_amount: 本次充值赠送额 gift_balance: 充值后赠送帐户的余额。

Return:
```
{
    "status_code": 0,
    "data": []
}
```

### 使用钱包支付

POST https://mall.smallsaas.cn/rest/wallet_pay 

Header: Authorization: token

Data:
```
{
    "orderType": "Order",
    "orderNumber": "22334",
    "password": "134545" // 支付密码
}
```

Error Return:
```
{
    "status_code": 1,
    "message": "wallet.insufficient.balance"
}
```

Success Return:
```
{
    "status_code": 0,
    "message": "ok"
}
```

### PAD端使用钱包支付

POST https://mall.smallsaas.cn/rest/admin/wallet_pay 

>Pre-cond:
先调用发送短信验证码给会员手机。

Header: Authorization: token

Data:
```
{
    "orderType": "Order",
    "orderNumber": "22334",
    "phone": "1308888888",
    "captcha": "2345"
}
```

Error Return:
```
{
    "status_code": 1,
    "message": "wallet.insufficient.balance"
}
```

Success Return:
```
{
    "status_code": 0,
    "message": "ok"
}
```

### 重置钱包支付密码

POST https://mall.smallsaas.cn/rest/wallet_password 

Header: Authorization: token

Data:
```
{
    "oldPassword": "122222", //旧密码，第一次设置密码不用这个字段
    "password": "134545" // 支付密码
}
```

Success Return:
```
{
    "status_code": 0,
    "message": "ok"
}
```

### 验证钱包支付密码

POST https://mall.smallsaas.cn/rest/wallet_verify_password 

Header: Authorization: token

Data:
```
{
	"password": "134545" // 支付密码
}
```

Success Return:
```
{
    "status_code": 0,
    "message": "ok"
}
```

### 检查是否已设置支付密码

GET https://mall.smallsaas.cn/rest/wallet_password 

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Success Return:
```
{
"status_code": 0,
"data": true
}
```