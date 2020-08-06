## 用户API

### 注册
  POST https://mall.smallsaas.cn/rest/register

  可使用用户名/手机 注册。 使用手机时，验证码是必选的。
  获取验证码的API见下面。
  
  Param:

   - invite_code: optional
  
  Data:
```json
 {
   "username": "abc",
   "password": "abc",
   "phone": "13800000001",
   "captcha": "123456",
   "invite_code": "xfaEfw" 
 }
```
 Successful Return:
```json
 {
   "message": "register.success",
   "status_code": 0
 }
```

### 获取手机验证码

POST https://mall.smallsaas.cn/rest/pub/sms

会发送短信到填写的手机上。

Param:

 - name: 指定不同的名字, 可以拿到相应模版的消息

Data:
```json
{
  "phone": "13800000001",
  "name": "verify"
}
```

Return:
```json
{
  "message": "ok",
  "status_code": 0
}
```

### 验证手机验证码

POST https://mall.smallsaas.cn/rest/pub/sms_verify

Data:
```json
{
  "phone": "13800000001",
  "captcha": "1234"
}
```
Return:
```json
{
  "message": "ok",
  "status_code": 0
}
```

### 登录

POST https://mall.smallsaas.cn/rest/login

可以根据需要组合，如:

  username + password,
  
  phone + password,
  
  phone + captcha

验证码获取API见上面。

Data:
```json
{
  "username": "abc",
  "password": "abc",
  "phone": "13800000001",
  "captcha": "134556"
}
```
Successful Return:
```json
{
  "status_code": 0,
  "data": {
    "access_token": "eyJ0b2tlbiI6IjU2MDlhMGJhOTBhZmFhMzI4NWZkZDk1ZjcxMTAyNjlmOGZmMGFiZDkiLCJsb2dpbl9uYW1lIjoiYWJjIn0="
  }
}
```

### 登出系统

GET https://mall.smallsaas.cn/rest/logout

Header: Authorization: token

Successful Return:
```json
{
  "message": "logout.success",
  "status_code": 0
}
```

### 修改密码

POST https://mall.smallsaas.cn/rest/password

Header: Authorization: token

Data:
```json
{
  "old_password": "abcdefg",
  "new_password": "123456"
}
```
Successful Return:
```json
{
  "message": "password.changed",
  "status_code": 0
}
```
Failure Return:
```json
{
  "message": "incorrect.old.password",
  "status_code": 1
}
```

### 忘记密码

POST https://mall.smallsaas.cn/rest/pub/forget_password

Header: Authorization: token

Data:
```json
{
  "phone": "13800000001",
  "captcha": "134566",
  "password": "123456"
}
```
Successful Return:
```json
{
  "message": "password.reset",
  "status_code": 0
}
```
Failure Return:
```json
{
  "message": "invalid.captcha",
  "status_code": 1
}
```

### 绑定手机

POST https://mall.smallsaas.cn/rest/phone>

Header: Authorization: token

Data:
```json
{
  "phone": "13800000001",
  "captcha": "123456"
}
```
Successful Return:
```json
{
  "message": "phone.updated",
  "status_code": 0
}
```
Failure Return:
```json
{
  "message": "captcha.invalid",
  "status_code": 1
}
```

### 移动应用的微信登录

POST https://mall.smallsaas.cn/rest/login_wxapp>

Param： 

 - code: app调起微信授权返回的code。

Data:
```json
{
  "code": "abcdefg"
}
```
Successful Return:
```json
{
  "status_code": 0,
  "data": {
    "access_token": "eyJsb2dpbl9uYW1lIjoiMTM5MjIxMTIxMzAiLCJ0b2tlbiI6ImNlODM5M2NlNDQ0ZTViMTA5YzMyOWU4N2UyNjg4Yzk0ZDFjYzY4MzIifQ==",
    "openid": "o0_gg0X2M7gnHmJUm71JzaKSYg8w",
    "unionid": "o-nTCtw8c18ZTyOmzgSNjhbbJ67c"
  }
}
```
Failure Return:
```json
{
  "status_code": 1,
  "data": {
    "openid": "o0_gg0X2M7gnHmJUm71JzaKSYg8w",
    "unionid": "o-nTCtw8c18ZTyOmzgSNjhbbJ67c"
  },
  "message": "user.not.found"
}
```

### 小程序登录

POST https://mall.smallsaas.cn/rest/login_wxa>

进入小程序时先调用这个接口，如果返回 错误码 user.not.found，
则弹出注册界面，让用户输入 手机/短信验证码，调用 /rest/register_wxa
接口进行注册。

Param： 

 - code: 小程序的wx.login返回的code。

Data:
```json
{
  "code": "abcdefg"
}
```
Successful Return:
```json
{
  "status_code": 0,
  "data": {
    "access_token": "eyJsb2dpbl9uYW1lIjoiMTM5MjIxMTIxMzAiLCJ0b2tlbiI6ImNlODM5M2NlNDQ0ZTViMTA5YzMyOWU4N2UyNjg4Yzk0ZDFjYzY4MzIifQ==",
    "openid": "o0_gg0X2M7gnHmJUm71JzaKSYg8w",
    "unionid": "o-nTCtw8c18ZTyOmzgSNjhbbJ67c"
  }
}
```
Failure Return:
```json
{
  "status_code": 1,
  "data": {
  "openid": "o0_gg0X2M7gnHmJUm71JzaKSYg8w",
  "unionid": "o-nTCtw8c18ZTyOmzgSNjhbbJ67c"
  },
  "message": "user.not.found"
}
```

### 小程序注册

POST https://mall.smallsaas.cn/rest/register_wxa>

Param： 

 - phone: 手机号

 - openid: login API返回的openid

 - captcha: 短信验证码

Data:
```json
{
  "phone": "13922112130",
  "openid": "o0_gg0X2M7gnHmJUm71JzaKSYg8w",
  "captcha":"123456"
}
```
Successful Return:
```json
{
  "status_code": 0,
  "data": {
    "access_token": "eyJsb2dpbl9uYW1lIjoiMTM5MjIxMTIxMzAiLCJ0b2tlbiI6ImNlODM5M2NlNDQ0ZTViMTA5YzMyOWU4N2UyNjg4Yzk0ZDFjYzY4MzIifQ==",
    "openid": "o0_gg0X2M7gnHmJUm71JzaKSYg8w"
  }
}
```
Failure Return:
```json
{
  "status_code": 1,
  "message": "phone.already.exist"
}
```

### 查看个人Profile

GET https://mall.smallsaas.cn/rest/profile

Header: Authorization: token

Param:

 - birthday: 生日

 - inviter_name: 邀请者名字

 - invitation_code: 我的邀请码

 - invitation_qrcode_url: 邀请码二维码图片url

 - invitation_qrcode: 我的邀请码URL

 - inviter_id: 邀请者ID

 - sex: 性别： 0 保密， 1 男， 2 女

 - avatar: 头像,默认使用微信的头像

 - followed: 是否关注公众号， 0 关注， 1 未关注

 - follow_time: 关注时间

Return:
```json
{
  "status_code": 0,
  "data": {
    "uid": "U00000069",
    "birthday": "1999-01-22", 
    "inviter_name": null, 
    "invitation_code": "ff705d15b67bba191f84943e4972d08a", 
    "invitation_qrcode_url": "http://host/image/abc.png",
    "invitation_qrcode": "http://www.kequandian.net/app/app?invite_code=ff705d15b67bba191f84943e4972d08a",
    "inviter_id": null, 
    "sex": 2, 
    "register_date": "2016-06-07 13:27:17",
    "avatar": null,
    "last_login_date": "2016-06-07 13:28:07",
    "login_name": "abc",
    "weixin": "abc",
    "token_expired_date": "2016-07-07 13:28:07",
    "phone": "1390000000",
    "name": "abc",
    "real_name": "Huang",
    "details": "sffffaaaa",
    "id": 2,
    "email": "h@a.com",
    "status": "NORMAL",
    "followed": 0, 
    "follow_time": "2016-06-04 21:00:00" 
  }
}
```

### 更新个人Profile

POST https://mall.smallsaas.cn/rest/profile

Header: Authorization: token

DATA:
```json
{
  "phone": "1390000000",
  "sex": 2,
  "details": "sffffaaaa",
  "birthday": "1999/01/22",
  "email": "h@a.com",
  "name": "axxvv",
  "real_name": "Huang"
}
```
Return:
```json
{
  "status_code": 0,
  "message": "profile.updated"
}
```
### 根据userID列表查看用户头像等信息

POST https://mall.smallsaas.cn/rest/pub/user_info

Data:
```json
{ "ids": [ 1, 2, 4 ] }
```
Return:
```json
{
  "status_code": 0,
  "data": [
    {
      "sex": 0,
      "name": "Administrator",
      "id": 1,
      "avatar": "http://abc.com/1.jpg"
    },
    {
      "sex": 0,
      "name": "Administrator2",
      "id": 2,
      "avatar": null
    },
    {
      "sex": 0,
      "name": "Administrator4",
      "id": 4,
      "avatar": null
    }
  ]
}
```

### 省市区数据

GET https://mall.smallsaas.cn/rest/pcd?all=true&province=广东&city=广州

Param:

 - all: optinal, 一次性返回所有的数据

 - province: optional, 返回该省下面所有的城市。

 - city: optional, 返回该市下面所有的区。

> 不带任何参数，则返回所有的省。

Header: Authorization: token

Return:
```json
{
  "status_code": 0,
  "data": [{
    "id": 30,
    "name": "广东",
    "type": "p",
    "parent_id": null
  }, {
    "id": 35,
    "name": "上海",
    "type": "p",
    "parent_id": null
  }]
}
```

有all参数时，return:
```json
{
  "status_code": 0,
  "data": [{
    "id": 2183,
    "area_list": [{
    "id": 2184,
    "area_list": [{
    "id": 2185,
    "name": "越秀区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2186,
    "name": "荔湾区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2187,
    "name": "海珠区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2188,
    "name": "天河区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2189,
    "name": "白云区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2190,
    "name": "黄埔区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2191,
    "name": "番禺区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2192,
    "name": "花都区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2193,
    "name": "南沙区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2194,
    "name": "萝岗区",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2195,
    "name": "增城市",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2196,
    "name": "从化市",
    "type": "d",
    "parent_id": 2184
  }, {
    "id": 2197,
    "name": "其他",
    "type": "d",
    "parent_id": 2184
  }],
    "name": "广州",
    "type": "c",
    "parent_id": 2183
  }],
    "name": "广东",
    "type": "p",
    "parent_id": null
  }]
}
```
