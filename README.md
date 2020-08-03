### 用户API

  POST <http://112.74.26.228:10080/rest/register>

  可使用用户名/手机 注册。 使用手机时，验证码是必选的。
  获取验证码的API见下面。
```json
 {
    
 "username": "abc",

 "password": "abc",

 "phone": "13800000001",

 "captcha": "123456",

 "invite\_code": "xfaEfw" //optional

 }

 Successful Return:

 {

 "message": "register.success",

 "status\_code": 0

 }
```

2.  **获取手机验证码**

POST <http://112.74.26.228:10080/rest/pub/sms>

会发送短信到填写的手机上。

{

"phone": "13800000001",

"name": "verify" //指定不同的名字，可以拿到相应模版的消息

}

Return:

{

"message": "ok",

"status\_code": 0

}

3.  **验证手机验证码**

POST <http://112.74.26.228:10080/rest/pub/sms_verify>

{

"phone": "13800000001",

"captcha": "1234"

}

Return:

{

"message": "ok",

"status\_code": 0

}

4.  **登录**

POST <http://112.74.26.228:10080/rest/login>

可以根据需要组合，如:

username + password,

phone + password,

phone + captcha

验证码获取API见上面。

{

"username": "abc",

"password": "abc",

"phone": "13800000001",

"captcha": "134556"

}

Successful Return:

{

"status\_code": 0,

"data": {

"access\_token":
"eyJ0b2tlbiI6IjU2MDlhMGJhOTBhZmFhMzI4NWZkZDk1ZjcxMTAyNjlmOGZmMGFiZDkiLCJsb2dpbl9uYW1lIjoiYWJjIn0="

}

}

5.  **登出系统**

GET <http://112.74.26.228:10080/rest/logout>

Header: Authorization:
eyJ0b2tlbiI6IjU2MDlhMGJhOTBhZmFhMzI4NWZkZDk1ZjcxMTAyNjlmOGZmMGFiZDkiLCJsb2dpbl9uYW1lIjoiYWJjIn0=

Successful Return:

{

"message": "logout.success",

"status\_code": 0

}

6.  **修改密码**

POST <http://112.74.26.228:10080/rest/password>

Header: Authorization:
eyJ0b2tlbiI6IjU2MDlhMGJhOTBhZmFhMzI4NWZkZDk1ZjcxMTAyNjlmOGZmMGFiZDkiLCJsb2dpbl9uYW1lIjoiYWJjIn0=

Data:

{

"old\_password": "abcdefg",

"new\_password": "123456"

}

Successful Return:

{

"message": "password.changed",

"status\_code": 0

}

Failure Return:

{

"message": "incorrect.old.password",

"status\_code": 1

}

窗体顶端

编辑

窗体底端

7.  **忘记密码**

POST <http://112.74.26.228:10080/rest/pub/forget_password>

Header: Authorization:
eyJ0b2tlbiI6IjU2MDlhMGJhOTBhZmFhMzI4NWZkZDk1ZjcxMTAyNjlmOGZmMGFiZDkiLCJsb2dpbl9uYW1lIjoiYWJjIn0=

Data:

{

"phone": "13800000001",

"captcha": "134566",

"password": "123456"

}

Successful Return:

{

"message": "password.reset",

"status\_code": 0

}

Failure Return:

{

"message": "invalid.captcha",

"status\_code": 1

}

8.  **绑定手机**

POST <http://112.74.26.228:10080/rest/phone>

Header: Authorization:
eyJ0b2tlbiI6IjU2MDlhMGJhOTBhZmFhMzI4NWZkZDk1ZjcxMTAyNjlmOGZmMGFiZDkiLCJsb2dpbl9uYW1lIjoiYWJjIn0=

Data:

{

"phone": "13800000001",

"captcha": "123456"

}

Successful Return:

{

"message": "phone.updated",

"status\_code": 0

}

Failure Return:

{

"message": "captcha.invalid",

"status\_code": 1

}

窗体顶端

编辑

窗体底端

9.  **移动应用的微信登录**

POST <http://112.74.26.228:10080/rest/login_wxapp>

Param： code - app调起微信授权返回的code。

Data:

{

"code": "abcdefg"

}

Successful Return:

{

"status\_code": 0,

"data": {

"access\_token":
"eyJsb2dpbl9uYW1lIjoiMTM5MjIxMTIxMzAiLCJ0b2tlbiI6ImNlODM5M2NlNDQ0ZTViMTA5YzMyOWU4N2UyNjg4Yzk0ZDFjYzY4MzIifQ==",

"openid": "o0\_gg0X2M7gnHmJUm71JzaKSYg8w",

"unionid": "o-nTCtw8c18ZTyOmzgSNjhbbJ67c"

}

}

Failure Return:

{

"status\_code": 1,

"data": {

"openid": "o0\_gg0X2M7gnHmJUm71JzaKSYg8w",

"unionid": "o-nTCtw8c18ZTyOmzgSNjhbbJ67c"

},

"message": "user.not.found"

}

10. **小程序登录**

POST <http://112.74.26.228:10080/rest/login_wxa>

进入小程序时先调用这个接口，如果返回 错误码 user.not.found，
则弹出注册界面，让用户输入 手机/短信验证码，调用 /rest/register\_wxa
接口进行注册。

Param： code - 小程序的wx.login返回的code。

Data:

{

"code": "abcdefg"

}

Successful Return:

{

"status\_code": 0,

"data": {

"access\_token":
"eyJsb2dpbl9uYW1lIjoiMTM5MjIxMTIxMzAiLCJ0b2tlbiI6ImNlODM5M2NlNDQ0ZTViMTA5YzMyOWU4N2UyNjg4Yzk0ZDFjYzY4MzIifQ==",

"openid": "o0\_gg0X2M7gnHmJUm71JzaKSYg8w",

"unionid": "o-nTCtw8c18ZTyOmzgSNjhbbJ67c"

}

}

Failure Return:

{

"status\_code": 1,

"data": {

"openid": "o0\_gg0X2M7gnHmJUm71JzaKSYg8w",

"unionid": "o-nTCtw8c18ZTyOmzgSNjhbbJ67c"

},

"message": "user.not.found"

}

11. **小程序注册**

POST <http://112.74.26.228:10080/rest/register_wxa>

Param： phone - 手机号

openid - login API返回的openid

captcha - 短信验证码

Data:

{

"phone": "13922112130",

"openid": "o0\_gg0X2M7gnHmJUm71JzaKSYg8w",

"captcha":"123456"

}

Successful Return:

{

"status\_code": 0,

"data": {

"access\_token":
"eyJsb2dpbl9uYW1lIjoiMTM5MjIxMTIxMzAiLCJ0b2tlbiI6ImNlODM5M2NlNDQ0ZTViMTA5YzMyOWU4N2UyNjg4Yzk0ZDFjYzY4MzIifQ==",

"openid": "o0\_gg0X2M7gnHmJUm71JzaKSYg8w"

}

}

Failure Return:

{

"status\_code": 1,

"message": "phone.already.exist"

}

12. **查看个人Profile**

GET <http://112.74.26.228:10080/rest/profile>

Header: Authorization:
eyJ0b2tlbiI6IjU2MDlhMGJhOTBhZmFhMzI4NWZkZDk1ZjcxMTAyNjlmOGZmMGFiZDkiLCJsb2dpbl9uYW1lIjoiYWJjIn0=

Return:

{

"status\_code": 0,

"data": {

"uid": "U00000069",

"birthday": "1999-01-22", //生日

"inviter\_name": null, //邀请者名字

"invitation\_code": "ff705d15b67bba191f84943e4972d08a", //我的邀请码

"invitation\_qrcode\_url": "http://host/image/abc.png",
//邀请码二维码图片url

"invitation\_qrcode":
"http://www.kequandian.net/app/app?invite\_code=ff705d15b67bba191f84943e4972d08a",
//我的邀请码URL

"inviter\_id": null, //邀请者ID

"sex": 2, //性别： 0 保密， 1 男， 2 女

"register\_date": "2016-06-07 13:27:17",

"avatar": null,//头像,默认使用微信的头像

"last\_login\_date": "2016-06-07 13:28:07",

"login\_name": "abc",

"weixin": "abc",

"token\_expired\_date": "2016-07-07 13:28:07",

"phone": "1390000000",

"name": "abc",

"real\_name": "Huang",

"details": "sffffaaaa",

"id": 2,

"email": "h\@a.com",

"status": "NORMAL",

"followed": 0, //是否关注公众号， 0 关注， 1 未关注

"follow\_time": "2016-06-04 21:00:00" //关注时间

}

}

13. **更新个人Profile**

POST <http://112.74.26.228:10080/rest/profile>

Header: Authorization:
eyJ0b2tlbiI6IjU2MDlhMGJhOTBhZmFhMzI4NWZkZDk1ZjcxMTAyNjlmOGZmMGFiZDkiLCJsb2dpbl9uYW1lIjoiYWJjIn0=

DATA:

{

"phone": "1390000000",

"sex": 2,

"details": "sffffaaaa",

"birthday": "1999/01/22",

"email": "h\@a.com",

"name": "axxvv",

"real\_name": "Huang"

}

Return:

{

"status\_code": 0,

"message": "profile.updated"

}

14. **根据userID列表查看用户头像等信息**

POST <http://112.74.26.228:10080/rest/pub/user_info>

data:

{ "ids": \[ 1, 2, 4 \] }

Return:

{

"status\_code": 0,

"data": \[

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

\]

}

15. **省市区数据**

GET <http://112.74.26.228:10080/rest/pcd?all=true&province=>广东&city=广州

Para:

1.  all - optinal, 一次性返回所有的数据

2.  province - optional, 返回该省下面所有的城市。

3.  city - optional, 返回该市下面所有的区。

4.  不带任何参数，则返回所有的省。

Header: Authorization:
eyJ0b2tlbiI6IjU2MDlhMGJhOTBhZmFhMzI4NWZkZDk1ZjcxMTAyNjlmOGZmMGFiZDkiLCJsb2dpbl9uYW1lIjoiYWJjIn0=

Return:

{

"status\_code": 0,

"data": \[{

"id": 30,

"name": "广东",

"type": "p",

"parent\_id": null

}, {

"id": 35,

"name": "上海",

"type": "p",

"parent\_id": null

}\]

}

有all参数时，return:

{

"status\_code": 0,

"data": \[{

"id": 2183,

"area\_list": \[{

"id": 2184,

"area\_list": \[{

"id": 2185,

"name": "越秀区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2186,

"name": "荔湾区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2187,

"name": "海珠区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2188,

"name": "天河区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2189,

"name": "白云区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2190,

"name": "黄埔区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2191,

"name": "番禺区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2192,

"name": "花都区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2193,

"name": "南沙区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2194,

"name": "萝岗区",

"type": "d",

"parent\_id": 2184

}, {

"id": 2195,

"name": "增城市",

"type": "d",

"parent\_id": 2184

}, {

"id": 2196,

"name": "从化市",

"type": "d",

"parent\_id": 2184

}, {

"id": 2197,

"name": "其他",

"type": "d",

"parent\_id": 2184

}\],

"name": "广州",

"type": "c",

"parent\_id": 2183

}\],

"name": "广东",

"type": "p",

"parent\_id": null

}\]

}

16. **商城API**

17. **获取商城全局配置项**

GET <http://112.74.26.228:10080/rest/global_config>

Return:

{

"status\_code": 0,

"data": {

"point\_exchange\_rate": 100,

"auto\_select\_coupon": false,

"drawing\_condition": 100

}

}

18. **获取产品类别列表**

GET <http://112.74.26.228:10080/rest/product_category?promoted=true>

Parameter:

promoted - optional,
如果指定该参数，则在一级类别下面返回类别该类别（包括它子类别）下的推荐产品列表。

Return:

{

"status\_code": 0,

"data": \[{

"id": 1,

"cover": null,

"sub\_categories": \[{

"id": 2,

"cover":
"http://112.74.26.228:8000/p/fb61f7180cb48a0d1bcff2a4edab9780.png",

"sub\_categories": \[\],

"description": null,

"name": "瓶装2.5L",

"parent\_id": 1

}, {

"id": 5,

"cover":
"http://112.74.26.228:8000/p/aa92d03568a42607011ca55815d48368.png",

"sub\_categories": \[\],

"description": null,

"name": "旅行装(袋)",

"parent\_id": 1

}\],

"description": null,

"name": "超效洁净",

"parent\_id": null,

"is\_show\_products": 1,
//点击类别时是否进入该类别下第1个产品的详情页（1 是 0 否）,

"products": \[{ //如果指定promoted时返回。

"free\_shipping": 0,

"freight": 0.00,

"last\_modified\_date": "2016-10-10 19:51:55",

"promoted": 1,

"stock\_balance": 1000,

"sales": 0,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20161010195121988-gFvkrsAZ.jpeg",

"unit": "a",

"category\_id": 3,

"price": 33.00,

"suggested\_price": 33.00,

"name": "aaaa",

"short\_name": "aa",

"id": 1,

"created\_date": "2016-10-10 19:51:23",

"fare\_id": 1,

"sort\_order": 100,

"partner\_level\_zone": 1,

"barcode": null,

"view\_count": 0,

"store\_location": null,

"status": "ONSELL",

"cost\_price": 33.00,

"weight": 500, //重量， 单位克

"bulk": 100 //体积

}\]

}, {

"id": 3,

"cover": null,

"sub\_categories": \[\],

"description": null,

"name": "亮白增艳",

"parent\_id": null

}, {

"id": 4,

"cover": null,

"sub\_categories": \[\],

"description": null,

"name": "活氧清洁剂",

"parent\_id": null

}\]

}

19. **获取某类别下的产品列表**

只列出 ONSELL 状态的产品

GET <http://112.74.26.228:10080/rest/product_category/id?pageNumber=1&pageSize=50&orderByDesc=view_count&orderBy=price&orderBy=sales&promoted=true>

para:

id - 类别ID，如果指定-1 则返回所有产品

pageNumber - 当前页，默认1

pageSize - 每页记录数，默认50

orderBy - 排序列。如果同时指定了超过1个orderBy，则前者优先于后者

orderByDesc -
倒序排序列。如果同时指定了orderBy和orderByDesc，则orderBy优先于orderByDesc；

orderBy and orderByDesc 可以用的值有： view\_count : 人气， price :
价格， sales : 销量

promoted - optional, 如果指定该参数，则分页查询该类别下的推荐产品。

{

"status\_code": 0,

"data": {

"id": 2,

"cover":
"http://112.74.26.228:8000/p/fb61f7180cb48a0d1bcff2a4edab9780.png",

"description": null,

"name": "瓶装2.5L",

"is\_show\_products": 1,
//点击类别时是否进入该类别下第1个产品的详情页（1 是 0 否）,

"products": \[{

"created\_date": "2016-04-22 09:30:53",

"cost\_price": 20.00,

"status": "ONSELL",

"free\_shipping": 1,

"origin": "广东",

"suggested\_price": 50.00,

"category\_id": 2,

"stock\_balance": 10000,

"id": 1,

"unit": "件",

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"last\_modified\_date": "2016-04-23 12:27:59",

"price": 34.80,

"category\_name": "瓶装2.5L",

"promoted": 1,

"sales": 0,

"name": "超效洁净护理洗衣液2.5L【全国包邮】",

"freight": 0.00,

"brand": "大地",

"sort\_order": 100,

"weight": 500, //重量， 单位克

"bulk": 200 //体积

}, {

"created\_date": "2016-04-22 11:16:14",

"cost\_price": 70.00,

"status": "ONSELL",

"free\_shipping": 1,

"origin": "广州",

"suggested\_price": 88.00,

"category\_id": 2,

"stock\_balance": 600,

"id": 3,

"unit": "件",

"cover":
"http://112.74.26.228:8000/p/2b3edeb3c3ca2a12b06893cb12286710.png",

"last\_modified\_date": "2016-04-22 14:22:04",

"price": 69.60,

"category\_name": "瓶装2.5L",

"promoted": 0,

"sales": 0,

"name": "超效洁净护理洗衣液2.5Lx2瓶【全国包邮】",

"freight": 0.00,

"brand": "大陆",

"sort\_order": 100,

"weight": 500, //重量， 单位克

"bulk": 200 //体积

}\],

"parent\_id": 1

}

}

20. **产品热门关键字**

GET <http://112.74.26.228:10080/rest/product_hit_word>

return:

{

"status\_code": 0,

"data": \[

{

"id": 1,

"hit": 0,

"name": "皂液"

}

\]

}

21. **产品搜索**

GET <http://112.74.26.228:10080/rest/product_search?pageNumber=1&pageSize=20&name=abc&barCode=234234&orderByDesc=view_count&orderBy=price&orderBy=sales>

para: pageNumber - 当前页，默认1

pageSize - 每页记录数，默认50

name - 产品名称

barCode - 条形码

orderBy - 排序列

orderByDesc - 倒序排序列

orderBy and orderByDesc 可以用的值有： view\_count : 人气， price :
价格， sales : 销量

{

"status\_code": 0,

"data":\[

{

"created\_date": "2016-04-22 09:30:53",

"cost\_price": 20.00,

"status": "ONSELL",

"free\_shipping": 1,

"origin": "广东",

"suggested\_price": 50.00,

"category\_id": 2,

"stock\_balance": 10000,

"id": 1,

"unit": "件",

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"last\_modified\_date": "2016-04-23 12:27:59",

"price": 34.80,

"category\_name": "瓶装2.5L",

"promoted": 1,

"sales": 0,

"name": "超效洁净护理洗衣液2.5L【全国包邮】",

"short\_name": "aa",

"freight": 0.00,

"brand": "大地",

"sort\_order": 100,

"weight": 500, //重量， 单位克

"bulk": 200 //体积

}, {

"created\_date": "2016-04-22 11:16:14",

"cost\_price": 70.00,

"status": "ONSELL",

"free\_shipping": 1,

"origin": "广州",

"suggested\_price": 88.00,

"category\_id": 2,

"stock\_balance": 600,

"id": 3,

"unit": "件",

"cover":
"http://112.74.26.228:8000/p/2b3edeb3c3ca2a12b06893cb12286710.png",

"last\_modified\_date": "2016-04-22 14:22:04",

"price": 69.60,

"category\_name": "瓶装2.5L",

"promoted": 0,

"sales": 0,

"name": "超效洁净护理洗衣液2.5Lx2瓶【全国包邮】",

"freight": 0.00,

"brand": "大陆",

"sort\_order": 100,

"weight": 500, //重量， 单位克

"bulk": 200 //体积

}

\]

}

22. **获取所有产品列表**

只列出 ONSELL 状态的产品

GET <http://112.74.26.228:10080/rest/product?all=true>

参数： all - true 时查询所有产品列表。其他参数会忽略。

{

"status\_code": 0,

"data": \[{

"created\_date": "2016-04-22 09:30:53",

"cost\_price": 20.00,

"status": "ONSELL",

"free\_shipping": 1,

"origin": "广东",

"suggested\_price": 50.00,

"category\_id": 2,

"stock\_balance": 10000,

"id": 1,

"unit": "件",

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"last\_modified\_date": "2016-04-23 12:27:59",

"price": 34.80,

"category\_name": "瓶装2.5L",

"promoted": 1,

"sales": 0,

"name": "超效洁净护理洗衣液2.5L【全国包邮】",

"freight": 0.00,

"brand": "大地",

"sort\_order": 100,

"weight": 500, //重量， 单位克

"bulk": 200, //体积

"allow\_coupon": 0, //是否可以使用优惠券 0:不可以， 1:可以用

"credit": 0, // 可用积分数量

}\]

}

23. **获取推荐产品列表**

只列出 ONSELL 状态的产品

GET <http://112.74.26.228:10080/rest/product?pageNumber=1&pageSize=50&zone=1>

Para:

pageNumber - optional, 当前页，默认1

pageSize - optional, 每页记录数，默认50

zone - optional, 零元区／精品区／特价区
查询。如果不带这个参数，那么就查推荐产品。 零元区 1， 精品区 2， 特价区
3

orderBy - 排序列

orderByDesc - 倒序排序列

orderBy and orderByDesc 可以用的值有： view\_count : 人气， price :
价格， sales : 销量

{

"status\_code": 0,

"data": \[{

"created\_date": "2016-04-22 09:30:53",

"cost\_price": 20.00,

"status": "ONSELL",

"free\_shipping": 1,

"origin": "广东",

"suggested\_price": 50.00,

"category\_id": 2,

"stock\_balance": 10000,

"id": 1,

"unit": "件",

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"last\_modified\_date": "2016-04-23 12:27:59",

"price": 34.80,

"category\_name": "瓶装2.5L",

"promoted": 1,

"sales": 0,

"name": "超效洁净护理洗衣液2.5L【全国包邮】",

"freight": 0.00,

"brand": "大地",

"sort\_order": 100,

"weight": 500, //重量， 单位克

"bulk": 200 //体积

}\]

}

24. **查看产品详情**

GET <http://112.74.26.228:10080/rest/product/id>

{

"status\_code": 0,

"data": {

"created\_date": "2016-04-22 09:30:53",

"cost\_price": 20.00,

"status": "ONSELL",

"free\_shipping": 1,

"origin": "广东",

"suggested\_price": 50.00,

"category\_id": 2,

"stock\_balance": 10000,

"id": 1,

"unit": "件",

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"last\_modified\_date": "2016-04-23 18:26:39",

"price": 34.80,

"promoted": 1,

"sales": 0,

"description": "\<h1\>超优惠\<br/\>\</h1\>\<p\>\<img
src=\\"/upload/upload/image/20160601/1464767352927011775.png\\"
title=\\"1464767352927011775.png\\"
alt=\\"logo.png\\"/\>\</p\>\<p\>\<br/\>\</p\>",

"name": "超效洁净护理洗衣液2.5L【全国包邮】",

"freight": 0.00,

"images": \[\],

"brand": "大地",

"sort\_order": 100,

"weight": 500, //重量， 单位克

"bulk": 200, //体积

"properties": \[{

"value\_type": "STRING",

"product\_id": 1,

"id": 1,

"property\_value": "a1",

"display\_name": "a1",

"property\_id": 1

}, {

"value\_type": "STRING",

"product\_id": 1,

"id": 2,

"property\_value": "a2",

"display\_name": "a2",

"property\_id": 2

}\],

"covers": \[{

"product\_id": 1,

"id": 1,

"type": 0,

"url":
"http://localhost:9990/p/6255a9dd831b89aa92ec1df49054603a.jpeg"

}, {

"product\_id": 1,

"id": 2,

"type": 0,

"url":
"http://localhost:9990/p/3b316bb6c6b939eb64c36d047a6c9d6e.jpg"

}\],

"specifications":
\[{//产品规格，当购买产品时，弹出来的框提供的选择项。加入购物车和购买时需要把选择的项提交给后台，具体参考购物车和下单api的要求

"price": 140, //售价

"suggested\_price": 140,

"product\_id": 1,

"name": "a2", //规格名称

"id": 1,

"stock\_balance": 1000, //库存

"cost\_price": 100,

"weight": 500, //重量， 单位克

"bulk": 200 //体积

}, {

"price": 120,

"suggested\_price": 130,

"product\_id": 1,

"name": "a1",

"id": 2,

"stock\_balance": 1000,

"cost\_price": 90,

"weight": 500, //重量， 单位克

"bulk": 200 //体积

}\],

"fare\_template": {

"is\_incl\_postage\_by\_if": 0, // 1 条件包邮

"dispatch\_time": "24",

"is\_incl\_postage": 1, // 1 包邮

"name": "包邮",

"title": "［省钱优惠］",

"content": "满3KG更省钱哦。",

"shop\_addr": "广东-广州",

"last\_modified\_date": "2016-08-31 10:56:16",

"id": 1,

"valuation\_model": 0,

"incl\_postage\_provisoes": \[{ //条件包邮

"amount": 100.00, // 满100包邮

"bulk\_no": null,

"carry\_way": 0,

"id": 2,

"fare\_id": 2,

"region": null,

"type": 3,

"piece\_no": null,

"weight\_no": null

}\],

"carry\_modes": \[{

"second\_piece": 1,

"second\_amount": 0.00,

"first\_bulk": null,

"carry\_way": 0,

"is\_default": 0,

"first\_piece": 1,

"first\_weight": null,

"second\_bulk": null,

"second\_weight": null,

"id": 3,

"fare\_id": 2,

"region": "广东-广州\|广东-深圳", //这些地区的使用这个运费

"first\_amount": 8.00

}, {

"second\_piece": 1,

"second\_amount": 0.00, //续费

"first\_bulk": null,

"carry\_way": 0,

"is\_default": 1, //没有满足地区，使用这个默认运费

"first\_piece": 1,

"first\_weight": null,

"second\_bulk": null,

"second\_weight": null,

"id": 2,

"fare\_id": 2,

"region": null,

"first\_amount": 10.00 //首费

}\],

},

"purchase\_strategy": {

"id": 1,

"name": "关注公众号且限购1件",

"description": "请先关注公众号，关注后可以购买1件。"

}

}

}

25. **订单状态说明**

CREATED\_PAY\_PENDING － 待支付

CLOSED\_PAY\_TIMEOUT － 支付超时关闭

CLOSED\_CANCELED － 已取消

PAID\_CONFIRM\_PENDING － 已支付

CONFIRMED\_DELIVER\_PENDING － 待发货

DELIVERING － 发货中

DELIVERED\_CONFIRM\_PENDING－ 已发货

CANCELED\_RETURN\_PENDING － 待退货

CLOSED\_CONFIRMED － 已确认收货

CANCELED\_REFUND\_PENDING － 待退款

CLOSED\_REFUNDED － 已退款

CONFIRMED\_PICK\_PENDING - 待取货

26. **我的订单列表**

GET <http://112.74.26.228:10080/rest/order?pageNumber=1&pageSize=20&status=CREATED_PAY_PENDDING>

Para:

pageNumber - 页数，可空，默认1

pageSize - 每页记录数，可空，默认50

status - 订单状态, optional

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": \[{

"user\_id": 1,

"phone": "1380000000",

"contact\_user": "Mr Huang",

"province": "GD",

"city": "GZ",

"district": "Tiahne",

"street": "jianzhong road",

"detail": "6F",

"trade\_number": null,

"deal\_date": null,

"express\_number": "1232323",

"express\_code": "24234",

"express\_company": "abc",

"coupon\_info": null,

"zip": "510000",

"id": 3,

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"confirm\_date": null,

"description": "超效洁净护理洗衣液2.5L【全国包邮】 x 1. ",

"deliver\_date": null,

"created\_date": "2016-04-26 10:27:56",

"order\_number": "0000000101461637676506360",

"status": "CREATED\_PAY\_PENDING",

"remark": null,

"invoice": 1,

"invoice\_title": "ABC company",

"receiving\_time": "anytime",

"deliver\_order\_number": null,

"total\_price": 34.80,

"user\_name": "Administrator",

"freight": 0.00,

"pay\_date": null,

"payment\_type": "ALIPAY",

"point\_exchange\_rate": 100,

"pay\_expiry\_time": "2018-08-20 17:53:01",//
待支付订单支付的超时时间

"order\_items": \[

{

"quantity": 2,

"product\_specification\_id": null,

"weight": 500,

"product\_specification\_name": null,

"product\_name": "REJOICE飘柔家庭护理芦荟长效止痒滋润洗发露400ML",

"marketing\_description": null,

"cover": "http://images.10mup.com/20161104102243958-v499XJvA.jpg",

"marketing": null,

"final\_price": 25.8,

"price": 12.9,

"product\_id": 335,

"marketing\_id": null,

"id": 5920,

"bulk": 0,

"order\_id": 3290,

"partner\_level\_zone": 1,

"barcode": "6903148126660",

"store\_location": null,

"status": "CREATED",

"cost\_price": 10.21

}

\]

}\]

}

27. **我的退货退款订单列表**

GET <http://112.74.26.228:10080/rest/refund_order?pageNumber=1&pageSize=20>

Para:

pageNumber - 页数，可空，默认1

pageSize - 每页记录数，可空，默认50

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": \[

{

"trade\_number": "test\_trade\_num",

"pay\_date": "2016-12-14 13:42:33",

"deliver\_order\_number": null,

"order\_customer\_service": { //售后单信息

"reason": "AFSFSF",

"express\_code": null,

"service\_type": "REFUND",

"images": "\[\]",

"log": "\[{\\"time\\":\\"2016-12-14
01:42:47\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"afaf\\"}\]",

"refund\_fee": null, //退款金额

"id": 5,

"created\_date": "2016-12-14 13:42:47",

"express\_number": null,

"order\_id": 5,

"express\_company": null,

"status": "CREATED"

},

"city": "GZ",

"invoice\_title": "ABC company",

"receiving\_time": "anytime",

"user\_name": "Administrator",

"order\_number": "1612141342218661",

"freight": 0,

"description": "aaaa x 2. ",

"remark": null,

"express\_company": null,

"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",

"express\_code": null,

"is\_deleted": 0,

"province": "GD",

"street": "jianzhong road",

"is\_deliver\_reminder": 0,

"id": 5,

"express\_number": null,

"previous\_status": "CONFIRMED\_DELIVER\_PENDING",

"delivered\_date": null,

"zip": "510000",

"deal\_date": null,

"total\_price": 66,

"contact\_user": "Mr Huang",

"settled": 0,

"coupon\_info": null,

"payment\_type": "WECHAT",

"user\_id": 1,

"phone": "1380000000",

"point\_exchange\_rate": 100,

"deliver\_date": null,

"confirm\_date": "2016-12-14 13:42:33",

"district": "Tiahne",

"created\_date": "2016-12-14 13:42:21",

"invoice": 1,

"detail": "6F",

"status": "CANCELED\_REFUND\_PENDING"

},

{

"trade\_number": "test\_trade\_num",

"pay\_date": "2016-12-14 11:35:54",

"deliver\_order\_number": null,

"order\_customer\_service": {

"reason": "rrr",

"express\_code": null,

"service\_type": "RETURN",

"images": "\[\]",

"log": "\[{\\"time\\":\\"2016-12-14
11:36:32\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"yyy\\"},{\\"time\\":\\"2016-12-14
11:36:56\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"ok\\"},{\\"time\\":\\"2016-12-14
11:37:00\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"同意\\"},{\\"time\\":\\"2016-12-14
11:38:07\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"退货收到确认\\"},{\\"time\\":\\"2016-12-14
01:10:24\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"退款失败,
请稍后重试\\"},{\\"time\\":\\"2016-12-14
01:11:08\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"已完成退款\\"}\]",

"refund\_fee": 66,

"id": 4,

"created\_date": "2016-12-14 11:36:32",

"express\_number": null,

"order\_id": 4,

"express\_company": null,

"status": "REFUNDED"

},

"city": "GZ",

"invoice\_title": "ABC company",

"receiving\_time": "anytime",

"user\_name": "Administrator",

"order\_number": "1612141135416631",

"freight": 0,

"description": "aaaa x 2. ",

"remark": null,

"express\_company": "afa",

"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",

"express\_code": "afsd",

"is\_deleted": 0,

"province": "GD",

"street": "jianzhong road",

"is\_deliver\_reminder": 0,

"id": 4,

"express\_number": "rwrwe4",

"previous\_status": "DELIVERED\_CONFIRM\_PENDING",

"delivered\_date": "2016-12-14 11:36:05",

"zip": "510000",

"deal\_date": null,

"total\_price": 66,

"contact\_user": "Mr Huang",

"settled": 0,

"coupon\_info": null,

"payment\_type": "WECHAT",

"user\_id": 1,

"phone": "1380000000",

"point\_exchange\_rate": 100,

"deliver\_date": "2016-12-14 11:36:03",

"confirm\_date": "2016-12-14 11:35:54",

"district": "Tiahne",

"created\_date": "2016-12-14 11:35:41",

"invoice": 1,

"detail": "6F",

"status": "CLOSED\_REFUNDED"

},

{

"trade\_number": "test\_trade\_num",

"pay\_date": "2016-12-14 11:27:23",

"deliver\_order\_number": null,

"order\_customer\_service": {

"reason": "AFSFSF",

"express\_code": null,

"service\_type": "REFUND",

"images": "\[\]",

"log": "\[{\\"time\\":\\"2016-12-14
11:27:52\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"afaf\\"},{\\"time\\":\\"2016-12-14
11:31:17\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"ok\\"},{\\"time\\":\\"2016-12-14
11:31:19\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"同意\\"},{\\"time\\":\\"2016-12-14
11:32:14\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"更新退款金额为
58 元\\"},{\\"time\\":\\"2016-12-14
11:33:08\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"已完成退款\\"}\]",

"refund\_fee": 58,

"id": 3,

"created\_date": "2016-12-14 11:27:52",

"express\_number": null,

"order\_id": 3,

"express\_company": null,

"status": "REFUNDED"

},

"city": "GZ",

"invoice\_title": "ABC company",

"receiving\_time": "anytime",

"user\_name": "Administrator",

"order\_number": "1612141127143691",

"freight": 0,

"description": "aaaa x 2. ",

"remark": null,

"express\_company": null,

"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",

"express\_code": null,

"is\_deleted": 0,

"province": "GD",

"street": "jianzhong road",

"is\_deliver\_reminder": 0,

"id": 3,

"express\_number": null,

"previous\_status": "CONFIRMED\_DELIVER\_PENDING",

"delivered\_date": null,

"zip": "510000",

"deal\_date": null,

"total\_price": 66,

"contact\_user": "Mr Huang",

"settled": 0,

"coupon\_info": null,

"payment\_type": "WECHAT",

"user\_id": 1,

"phone": "1380000000",

"point\_exchange\_rate": 100,

"deliver\_date": null,

"confirm\_date": "2016-12-14 11:27:23",

"district": "Tiahne",

"created\_date": "2016-12-14 11:27:14",

"invoice": 1,

"detail": "6F",

"status": "CLOSED\_REFUNDED"

},

{

"trade\_number": "test\_trade\_num",

"pay\_date": "2016-12-13 15:35:06",

"deliver\_order\_number": null,

"order\_customer\_service": {

"reason": "AFSFSF",

"express\_code": null,

"service\_type": "RETURN",

"images": "\[\]",

"log": "\[{\\"time\\":\\"2016-12-13
03:35:30\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"afaf\\"},{\\"time\\":\\"2016-12-13
03:35:38\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"afd\\"},{\\"time\\":\\"2016-12-13
03:35:46\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"同意\\"},{\\"time\\":\\"2016-12-13
03:35:51\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"退货收到确认\\"},{\\"time\\":\\"2016-12-13
03:35:55\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"更新退款金额为
60 元\\"},{\\"time\\":\\"2016-12-13
03:37:12\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"更新退款金额为
61 元\\"},{\\"time\\":\\"2016-12-13
03:48:57\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"a\\"},{\\"time\\":\\"2016-12-13
03:52:01\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"com.jfeat.order.exception.RefundOrderException:
order.refund.failure\\"},{\\"time\\":\\"2016-12-13
03:52:55\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"java.lang.RuntimeException:
com.jfeat.order.exception.RefundOrderException:
order.refund.failure\\"},{\\"time\\":\\"2016-12-13
04:00:49\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"com.jfeat.order.exception.RefundOrderException:
order.refund.failure\\"},{\\"time\\":\\"2016-12-13
04:11:29\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"fsdas\\"},{\\"time\\":\\"2016-12-13
04:11:36\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"更新退款金额为
60 元\\"},{\\"time\\":\\"2016-12-13
04:11:41\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"退款失败,
请稍后重试\\"},{\\"time\\":\\"2016-12-13
05:18:40\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"退款失败,
请稍后重试\\"},{\\"time\\":\\"2016-12-14
11:26:17\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"已完成退款\\"}\]",

"refund\_fee": 60,

"id": 2,

"created\_date": "2016-12-13 15:35:30",

"express\_number": null,

"order\_id": 2,

"express\_company": null,

"status": "REFUNDED"

},

"city": "GZ",

"invoice\_title": "ABC company",

"receiving\_time": "anytime",

"user\_name": "Administrator",

"order\_number": "1612131532015531",

"freight": 0,

"description": "aaaa x 2. ",

"remark": "afafafafafafa",

"express\_company": "afa",

"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",

"express\_code": "afsd",

"is\_deleted": 0,

"province": "GD",

"street": "jianzhong road",

"is\_deliver\_reminder": 0,

"id": 2,

"express\_number": "234",

"previous\_status": "DELIVERED\_CONFIRM\_PENDING",

"delivered\_date": "2016-12-13 15:35:16",

"zip": "510000",

"deal\_date": null,

"total\_price": 66,

"contact\_user": "Mr Huang",

"settled": 0,

"coupon\_info": null,

"payment\_type": "WECHAT",

"user\_id": 1,

"phone": "1380000000",

"point\_exchange\_rate": 100,

"deliver\_date": "2016-12-13 15:35:14",

"confirm\_date": "2016-12-13 15:35:06",

"district": "Tiahne",

"created\_date": "2016-12-13 15:32:01",

"invoice": 1,

"detail": "6F",

"status": "CLOSED\_REFUNDED"

},

{

"trade\_number": "test\_trade\_num",

"pay\_date": "2016-12-13 14:01:47",

"deliver\_order\_number": null,

"order\_customer\_service": {

"reason": "AFSFSF",

"express\_code": null,

"service\_type": "RETURN",

"images": "\[\]",

"log": "\[{\\"time\\":\\"2016-12-13
02:03:26\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"afaf\\"},{\\"time\\":\\"2016-12-13
02:03:41\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"同意\\"},{\\"time\\":\\"2016-12-13
02:03:44\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"退货收到确认\\"},{\\"time\\":\\"2016-12-13
02:12:38\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"更新退款金额为
{0} 元\\"},{\\"time\\":\\"2016-12-13
02:13:42\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"更新退款金额为
62 元\\"},{\\"time\\":\\"2016-12-13
02:17:23\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"\\"},{\\"time\\":\\"2016-12-13
02:24:43\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"更新退款金额为
61 元\\"},{\\"time\\":\\"2016-12-13
02:33:33\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"\\"},{\\"time\\":\\"2016-12-13
02:34:49\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"更新退款金额为
60 元\\"},{\\"time\\":\\"2016-12-13
02:35:04\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"已完成退款\\"}\]",

"refund\_fee": 60,

"id": 1,

"created\_date": "2016-12-13 14:03:26",

"express\_number": null,

"order\_id": 1,

"express\_company": null,

"status": "REFUNDED"

},

"city": "GZ",

"invoice\_title": "ABC company",

"receiving\_time": "anytime",

"user\_name": "Administrator",

"order\_number": "1612131401365671",

"freight": 0,

"description": "aaaa x 2. ",

"remark": null,

"express\_company": "afa",

"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",

"express\_code": "afsd",

"is\_deleted": 0,

"province": "GD",

"street": "jianzhong road",

"is\_deliver\_reminder": 0,

"id": 1,

"express\_number": "324242",

"previous\_status": "DELIVERED\_CONFIRM\_PENDING",

"delivered\_date": "2016-12-13 14:02:41",

"zip": "510000",

"deal\_date": null,

"total\_price": 66,

"contact\_user": "Mr Huang",

"settled": 0,

"coupon\_info": null,

"payment\_type": "WECHAT",

"user\_id": 1,

"phone": "1380000000",

"point\_exchange\_rate": 100,

"deliver\_date": "2016-12-13 14:02:15",

"confirm\_date": "2016-12-13 14:01:47",

"district": "Tiahne",

"created\_date": "2016-12-13 14:01:36",

"invoice": 1,

"detail": "6F",

"status": "CLOSED\_REFUNDED"

}

\]

}

28. **我的订单详情**

GET <http://112.74.26.228:10080/rest/order/0000000401456137520088034>

Query Para: Order Number - 订单号

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": {

"detail": "6F",

"phone": "1380000000",

"contact\_user": "Mr Huang",

"remark": null,

"invoice": 1,

"street": "jianzhong road",

"trade\_number": null,

"deal\_date": null, //收货成交时间

"city": "GZ",

"id": 3,

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"confirm\_date": null, //平台确认时间

"description": "超效洁净护理洗衣液2.5L【全国包邮】 x 1. ",

"province": "GD",

"order\_items": \[{

"id": 5,

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"price": 34.80,

"cost\_price": 20.00,

"final\_price": 34.80,

"product\_id": 1,

"status": "CREATED",

"product\_name": "超效洁净护理洗衣液2.5L【全国包邮】",

"quantity": 1,

"order\_id": 3,

"product\_specification\_id": 2,

"product\_specification\_name": "a1" //用户选择的规格

}\],

"user\_id": 1,

"district": "Tiahne",

"deliver\_date": null, //开始发货时间

"delivered\_date": null, //完成发货时间

"created\_date": "2016-04-26 10:27:56", //创建时间

"order\_number": "0000000101461637676506360",

"zip": "510000",

"status": "CREATED\_PAY\_PENDING",

"invoice\_title": "ABC company",

"receiving\_time": "anytime",

"deliver\_order\_number": null,

"total\_price": 34.80,

"freight": 0.00,

"pay\_date": null, //支付时间

"payment\_type": "ALIPAY",

"point\_exchange\_rate": 100, //积分支付时的兑换率

"pay\_expiry\_time": "2018-08-20 17:53:01",//
待支付订单支付的超时时间

"order\_customer\_service": {

"reason": "afaf", //退货原因

"express\_code": null,

"service\_type": "RETURN", //售后类型： RETURN－退货退款，
REFUND－仅退款

"id": 1,

"created\_date": "2016-06-16 13:57:12",

"express\_number": "23234324", //快递单号

"order\_id": 1,

"express\_company": "ABC" //快递公司名

}

}

}

Error Return:

{

"message": "invalid.order.id",

"status\_code": 1

}

29. **我的订单数量统计**

GET <http://112.74.26.228:10080/rest/order_count>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data" {

"total": 12, // 总订单

"payPending": 2, //待支付

"delivering": 4, //待发货

"delivered": 2, //待收货

"commentPending": 2 //待评价

}

}

30. **提醒发货**

GET <http://112.74.26.228:10080/rest/order_deliver_reminder/0000000401456137520088034>

Query Para: Order Number - 订单号

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"message": "order.deliver.reminded",

"status\_code": 0

}

31. **订单评价**

PUT <http://112.74.26.228:10080/rest/order_comment/0000000401456137520088034>

Query Para: Order Number - 订单号

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{ "comment\_id": "12345" }

Return:

{

"message": "ok",

"status\_code": 0

}

32. **新建订单**

POST <http://112.74.26.228:10080/rest/order>

参考 下单前计算优惠信息 api 返回的优惠券，选择一个优惠劵进行下单。

到支付宝支付时，把order-number的值赋给out\_trade\_no进行支付。

微信支付 - WECHAT

积分支付 - POINT

钱包支付 - WALLET

/\*\*

\* 订单来源

\*/

public enum Origin {

//微信公众号(Wechat public account)

WPA,

//小程序

MINI\_PROGRAM,

//手机应用程序

APP\_ANDROID,

APP\_IOS,

//其他

OTHER

}

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

//配送方式：

//1.EXPRESS-快递（默认，当不传此参数或传递null时会使用此方式）

//2.
SELF\_PICK-自提（当使用此方式时，必须同时指定store\_id和store\_name）

//3.FLASH-极速送达（当使用此方式时，必须同时指定store\_id和store\_name)

//SELF\_PICK和FLASH方式的线上订单，需要店员登录ipad端处理

"delivery\_type": null,

//订单来源

//optional。default OTHER

//WPA（Wechat public account)-微信公众号 MINI-PROGRAM-小程序
APP-手机应用程序 OTHER-其他

"origin": "APP",

"pay\_credit": 120, //使用积分抵扣

"store\_id": "123", //门店id

"store\_name": "门店1", //门店名

"payment\_type": "WECHAT",

"remark": null,

"receiving\_time": "anytime", //收货时间

"invoice": 1, //是否开发票

"invoice\_title": "ABC company", //发票抬头

"contact": {

"contact\_user": "Mr Huang",

"phone": "1380000000",

"zip": "510000",

"province": "GD",

"city": "GZ",

"district": "Tiahne",

"street": "jianzhong road",

"detail": "6F"

},

"order\_items": \[{

"product\_id": 1,

"quantity": 2,

"product\_specification\_id": 1 //optional，
用户选择的产品规格，如果没有则不需要这个项

}\]

}

Return:

{

"status\_code": 0,

"data": {

"created\_date": "2016-04-25",

"order\_number": "0000000101461584134091428",

"status": "CREATED\_PAY\_PENDING",

"remark": null,

"total\_price": 290.00,

"id": 2,

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"description": "p1 x 2. ",

"freight": 0.00,

"province": "GD",

"city": "GZ",

"district": "LW",

"street": "AX",

"detail": null,

"zip": "510000",

"phone": "1390000000",

"contact\_user": "ABC",

"receiving\_time": "anytime",

"invoice": 1,

"invoice\_title": "ABC company",

"order\_items": \[{

"id": 1,

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"price": 145.00,

"final\_price": 290.00,

"cost\_price": 0.00,

"product\_id": 1,

"status": "CREATED",

"product\_name": "p1",

"quantity": 2,

"order\_id": 2，

"product\_specification\_id": 2,

"product\_specification\_name": "a1" //用户选择的产品规格

}\],

"user\_id": 1,

"payment\_type": null

}

}

33. **店员新建订单**

POST <http://112.74.26.228:10080/rest/store/order>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

//以下两个字段是店员新建订单api额外需要提供的

"store\_id": 123, //required 店铺id

"store\_name": "龙门客栈", //required 店铺名称

//其他需要提供的域同"新建订单api"

"payment\_type": "WECHAT",

// 使用积分抵扣

"pay\_credit": 120,

//订单来源

//optional。default OTHER

//WPA（Wechat public account)-微信公众号 MINI-PROGRAM-小程序
APP-手机应用程序 OTHER-其他

"origin": "APP",

"remark": null,

"receiving\_time": "anytime", //收货时间

"invoice": 1, //是否开发票

"invoice\_title": "ABC company", //发票抬头

"contact": {

"contact\_user": "Mr Huang",

"phone": "1380000000",

"zip": "510000",

"province": "GD",

"city": "GZ",

"district": "Tiahne",

"street": "jianzhong road",

"detail": "6F"

},

"order\_items": \[

{

"product\_id": 1, //required, 产品id

"product\_specification\_id": 1, //optional,产品规格id

"quantity": 2 //数量

}\]

}

Return: 同"新建订单api"

34. **店员更新订单状态**

PUT <http://112.74.26.228:10080/rest/store/order/>\<order-number\>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

注：店员操作的订单有两种：

1.线下订单。

收银员调用 \`店员创建订单API\`
下单，此API下单后会立刻返回此订单的信息，此订单的状态为"未支付"，配送方式为"自提"。

稍后收银员收到钱之后，认为交易完成了，可以执行"完成(complete)"操作
来完成交易。

当然客户可以随时取消交易，此时收银员需执行 "取消(cancel)"操作。

2.终端用户下的线上订单。这种订单又可分为3种：

（1）配送方式为"快递"的订单。这种是以前的方式。

（2）配送方式为"自提"的订单（delivery\_type:
SELF\_PICK)。这种方式的订单在下单时就指定了门店自提，即订单是关联一个店铺的。

对于这种订单，终端用户在下单并支付之后，订单的状态为"已支付待确认"（即待处理），此时店员可以在ipad端对此订单执行

"受理(accept)"操作,只能受理，受理后会关联结算店员，订单状态变为
CONFIRMED\_PICK\_PENDING 待取货。

"受理(accept)"后的自提单
(订单状态是CONFIRMED\_PICK\_PENDING)，如果用户上门取货了，店员可以"完成(complete)"此订单。

（3）配送方式为"极速送达"的订单（delivery\_type:
FLASH)。这种方式的订单在下单时就指定了极速送达（可能是用门店相关的物流系统），即订单也是关联一个店铺

的。

对于这种订单，终端用户在下单并支付之后，订单的状态为"已支付待确认"（即待处理），此时店员可以在ipad端对此订单执行

"受理(accept)"/"拒绝(reject)"操作。

拒绝通常是店员发现该店铺没货或其他原因导致本店铺不能处理该订单，这种情况下，api收到拒绝操作的请求，会把该订单所关联的店

铺清空，好让平台可以指定其他门店来处理此订单。

"受理(accept)"后的极速送达单处于待配送状态，如果店铺开始配送了，可以执行"开始配送delivering"操作。

开始配送的订单，在店铺把货物送达客户，店员就执行"完成(complete)"来完成订单，不需终端用户自己按完成。

注：不关联店铺的订单，店员是看不到的。比如上面介绍的本来是关联了一个店铺，但后来被店员拒绝的订单，拒绝之后，该订单就不关联此店

铺了，需要由平台自行重新指定这个订单关联的店铺。

Data:

{

"store\_id": "123", //required，店铺id

"action": "complete" //required, （complete-完成 cancel-取消
accept-受理 reject-拒绝 delivering-开始配送）

}

Return:

{

"status\_code": 0,

"message": "更新订单成功"

}

35. **店员查看门店订单列表（线上，线下订单都在这里查看）**

GET <http://112.74.26.228:10080/rest/store/order?pageNumber=1&pageSize=30&storeId=xxx&type=STORE_ORDER&status=CREATED_PAY_PENDING&status=PAID_CONFIRM_PENDING&contactUser=zhangsan&phone=111111&orderNumber=aaa&startTime=2018-05-01&endTime=2018-05-20>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Paras:

storeId: required，店铺id

type: required，订单类型（ORDER 线上订单 STORE\_ORDER 线下订单）

status: optional。可多个

contactUser: 联系人姓名

phone: 联系人电话

orderNumber: 订单号

startTime \~ endTime：返回的订单的创建时间在startTime \~ endTime之间

注意：

type：(1)STORE\_ORDER：线下订单（由店员下的单） （ipad端收银 →
历史订单页面需传type=STORE\_ORDER）

(2)ORDER：线上订单（由终端用户下的单）（分两种：1.配送方式为"快递"的单
2.配送方式为"自提"或"极速送达"的单，这样的单在下单时是关联了一个店铺的。

由于本api必须传递storeId，因此返回的订单只可能是"线下订单"或者"配送方式为自提或极速送达的线上订单"
（ipad端 → 线上待处理订单 → 全部订单需传type=ORDER）

Return:

{

"status\_code": 0,

"data": {

"totalRow": 1,

"pageNumber": 1,

"firstPage": true,

"lastPage": true,

"totalPage": 1,

"pageSize": 30,

"list": \[

{

"trade\_number": null,

"type": "STORE\_ORDER",

"express\_company": null,

"cover":
"http://120.79.77.207:8080/images/p/0ea3308197aaccd2635c4b7d31717537.jpeg",

"store\_user\_name": "user123",

"express\_code": null,

"province": "",

"delivery\_type": "SELF\_PICK",

"id": 1,

"previous\_status": null,

"delivered\_date": null,

"zip": "",

"deal\_date": null,

"pay\_credit": 0,

"contact\_user": "",

"settled": 0,

"coupon\_info": null,

"payment\_type": "STORE",

"store\_user\_id": "2",

"user\_id": 2,

"phone": "",

"point\_exchange\_rate": 100,

"deliver\_date": null,

"confirm\_date": null,

"district": "",

"detail": "",

"status": "CREATED\_PAY\_PENDING",

"pay\_date": null,

"deliver\_order\_number": null,

"city": "",

"invoice\_title": null,

"receiving\_time": "anytime",

"user\_name": "user123",

"order\_number": "1807181114341472",

"freight": 0,

"description": "测试1 x 8. ",

"mid": null,

"remark": "iPad 端收银界面",

"mname": null,

"is\_deleted": 0,

"street": "",

"store\_name": null,

"is\_deliver\_reminder": 0,

"express\_number": null,

"store\_id": null,

"total\_price": 8,

"marketing\_description": null,

"marketing": null,

"marketing\_id": null,

"created\_date": "2018-07-18 11:14:34",

"invoice": 0

}

\]

}

}

36. **店员查看门店订单详情**

GET <http://112.74.26.228:10080/rest/store/order/>\<order-number\>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": {

"trade\_number": null,

"type": "STORE\_ORDER",

"express\_company": null,

"cover":
"http://120.79.77.207:8080/images/p/0ea3308197aaccd2635c4b7d31717537.jpeg",

"store\_user\_name": "user123",

"express\_code": null,

"province": "",

"delivery\_type": "SELF\_PICK",

"id": 1,

"previous\_status": null,

"delivered\_date": null,

"order\_items": \[

{

"quantity": 8,

"product\_specification\_id": null,

"weight": 111,

"product\_specification\_name": null,

"product\_name": "测试1",

"marketing\_description": null,

"cover":
"http://120.79.77.207:8080/images/p/0ea3308197aaccd2635c4b7d31717537.jpeg",

"marketing": null,

"final\_price": 8,

"price": 1,

"product\_id": 1,

"marketing\_id": null,

"id": 1,

"bulk": null,

"order\_id": 1,

"partner\_level\_zone": 1,

"barcode": null,

"store\_location": null,

"status": "CREATED",

"cost\_price": 1

}

\],

"zip": "",

"deal\_date": null,

"pay\_credit": 0,

"contact\_user": "",

"settled": 0,

"coupon\_info": null,

"payment\_type": "STORE",

"store\_user\_id": "2",

"user\_id": 2,

"phone": "",

"point\_exchange\_rate": 100,

"deliver\_date": null,

"confirm\_date": null,

"district": "",

"detail": "",

"status": "CREATED\_PAY\_PENDING",

"pay\_date": null,

"deliver\_order\_number": null,

"order\_customer\_service": null,

"city": "",

"invoice\_title": null,

"receiving\_time": "anytime",

"order\_number": "1807181114341472",

"freight": 0,

"description": "测试1 x 8. ",

"mid": null,

"remark": "iPad 端收银界面",

"mname": null,

"is\_deleted": 0,

"street": "",

"store\_name": null,

"is\_deliver\_reminder": 0,

"express\_number": null,

"store\_id": null,

"total\_price": 8,

"marketing\_description": null,

"marketing": null,

"marketing\_id": null,

"created\_date": "2018-07-18 11:14:34",

"invoice": 0

}

}

37. **店员新建售后单**

POST <http://112.74.26.228:10080/rest/store/order_customer_service>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

"store\_id": "1", //required，店铺id

"store\_name": "总店", // required，店铺名

//退货单分为"有关联订单的退货单"和"没有关联订单的退货单"，换货单必须关联订单。因此对于没有关联订单的退货单，不需

//传递order\_number，对于其他两种，则必须传递order\_number

"order\_number": "2342323432432",

"service\_type": "RETURN", //required，REFUND-仅退款 RETURN-退货退款
EXCHANGE-换货

"reason": "AFSFSF", //required

"content": "afaf", //optional

"images": \["http://host/a.jpg", "http://host/b.jgp"\], //optional

"returns": \[ //退货项

{

"product\_id": 130,
//required（无论是否提供product\_specification\_id，都要提供product\_id）

"product\_specification\_id": 22, //optional

// 1.对于需要关联订单的退货单，不需要传递quantity，会使用其对应的order
item的quantity；

// 2.对于不需要关联订单的退货单，必须传递quantity

//
3.对于一定要关联订单的换货单，这种单据有两个清单（退货项清单和置换项清单）。无论是退货项还是置换项，

//都必须指定quantity

"quantity": 3,

//对于退货单的退货项，必须指定refund\_fee；

//对于换货单的退货项，无需指定refund\_fee，refund\_fee由

//"此换货单关联的订单对应的订单项的 price \* 传上来的退回数量" 决定

"refund\_fee": 40

}\],

"exchanges": \[ //置换项

{

"product\_id": 122, //required

"quantity": 2 //required

//refund\_fee无需提供

},

{

"product\_id": 130, //required

"product\_specification\_id": 22, //optional

// 1.对于需要关联订单的退货单，不需要传递quantity，会使用其对应的order
item的quantity；

// 2.对于不需要关联订单的退货单，必须传递quantity

//
3.对于一定要关联订单的换货单，这种单据有两个清单（退货项清单和置换项清单）。无论是退货项还是置换项，

//都必须指定quantity

"quantity": 3, //required

//refund\_fee无需提供

}\]

}

Return:

{

"status\_code": 0,

"message": "order.customer.service.created"

}

38. **店员查看单个售后单**

GET <http://112.74.26.228:10080/rest/store/order_customer_service/>\<service\_number\>

Para:

service\_number: 售后单号

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": {

"store\_id": "1",

"reason": "AFSFSF",

"images": "\[\\"http://host/a.jpg\\",\\"http://host/b.jgp\\"\]",

"log": "\[{\\"time\\":\\"2018-07-21
02:38:10\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"afaf\\"}\]",

"exchanges": \[ //置换项（置换清单）（仅换货单有此项）

{

"quantity": 2, //数量

"product\_specification\_id": null, //产品规格id

"weight": 111, //重量

//项类型（RETURN -
退货项（退货单的项和换货单中的退货清单的项都属于此类型） EXCHANGE -
置换项）

"type": "EXCHANGE",

"product\_specification\_name": null,

"order\_customer\_service\_id": 3, //售后单id

"product\_name": "水桶", //产品名

"marketing\_description": null, //营销活动描述

"cover": "/p/dbe108b7e5c0283013ebc956f2cc2f4b.jpg",

"marketing": null,

"final\_price": 22, //总价值

"price": 11, //价格

"refund\_fee": null, //置换项没有退回金额，此处必为null

"product\_id": 2, //产品id

"marketing\_id": null, //营销活动id

"id": 6,

"cost\_price": 1 //成本价

}

\],

"express\_company": null,

"store\_user\_name": "Administrator", //店员名

"express\_code": null, //快递单号

"service\_type": "EXCHANGE", //售后单类型（REFUND-仅退款
RETURN-退货退款 EXCHANGE-换货）

"store\_user\_id": "1", //店员id

//1.如果是退货单，此金额为此次退回应退回的金额。

//2.如果是换货单，且退回项总价值大于置换项总价值，则有refund\_fee；若小于，则有supplementary\_fee

"refund\_fee": 68, //退回金额

"supplementary\_fee": null, //补交金额

"store\_name": "总店", //店铺名

"returns": \[ //退货清单

{

"quantity": 3,

"product\_specification\_id": null,

"weight": 0,

//项类型（RETURN -
退货项（退货单的项和换货单中的退货清单的项都属于此类型） EXCHANGE -
置换项）

"type": "RETURN",

"product\_specification\_name": null,

"order\_customer\_service\_id": 3,

"product\_name": "IPHONE",

"marketing\_description": null,

"cover": null,

"marketing": null,

"final\_price": 90,

"price": 30,

"refund\_fee": 90, //退回金额

"product\_id": 1,

"marketing\_id": null,

"id": 5,

"cost\_price": 0

}

\],

"id": 3,

"created\_date": "2018-07-21 14:38:13",

"express\_number": null,

"service\_number": "180721143813797Administrator",

"order\_id": 1,

"status": "CREATED",

"order": {
//该售后单所关联的订单（如果售后单没有关联订单，则order不存在）

"trade\_number": null,

"type": "ORDER",

"express\_company": null,

"cover": null,

"store\_user\_name": null,

"express\_code": null,

"province": "广东",

"delivery\_type": "EXPRESS",

"id": 1,

"previous\_status": "DELIVERED\_CONFIRM\_PENDING",

"delivered\_date": "2018-07-20 12:58:40",

"zip": null,

"deal\_date": null,

"pay\_credit": 0,

"contact\_user": "admin",

"settled": 0,

"coupon\_info": null,

"payment\_type": "WECHAT",

"store\_user\_id": null,

"user\_id": 1,

"phone": "111",

"point\_exchange\_rate": 100,

"deliver\_date": "2018-07-20 12:58:36",

"confirm\_date": "2018-07-20 12:58:32",

"district": "荔湾区",

"detail": null,

"status": "CANCELED\_RETURN\_PENDING",

"pay\_date": "2018-07-21 12:58:23",

"deliver\_order\_number": "111",

"city": "广州",

"invoice\_title": null,

"receiving\_time": null,

"order\_number": "17072614522001811012",

"freight": 0,

"description": null,

"mid": null,

"remark": null,

"mname": null,

"is\_deleted": 0,

"street": null,

"store\_name": null,

"is\_deliver\_reminder": 0,

"express\_number": null,

"store\_id": null,

"total\_price": 500,

"marketing\_description": null,

"marketing": null,

"marketing\_id": null,

"created\_date": "2018-07-20 12:58:19",

"invoice": 0

},

"order\_items": \[ ////该售后单所关联的订单的订单项

{

"quantity": 3,

"product\_specification\_id": null,

"weight": 0,

"product\_specification\_name": null,

"product\_name": "IPHONE",

"marketing\_description": null,

"cover": null,

"marketing": null,

"final\_price": 90,

"price": 30,

"product\_id": 1,

"marketing\_id": null,

"id": 1,

"bulk": 0,

"order\_id": 1,

"partner\_level\_zone": null,

"barcode": null,

"store\_location": null,

"status": "CREATED",

"cost\_price": 0

}

\]

}

}

39. **店员查看订单数量统计**

GET <http://112.74.26.228:10080/rest/store/order_count?storeId=1>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Param:

storeId - 门店的ID

Return:

{

"status\_code": 0,

"data": {

"totalPrice": 14566, //订单总金额

"delivering": 0, // 配送中

"total": 6, //总订单数

"handlePending": 0, //待处理

"cancled": 0, //取消

"closed": 2, // 完成

"pickPending": 0, // 待取货

"deliverPending": 1 //待配送

}

}

40. **店员查看售后单列表**

GET <http://112.74.26.228:10080/rest/store/order_customer_service?pageNumber=1&pageSize=30&>

storeId=123&serviceType=RETURN&serviceNumber=1234&startTime=2018-01-01&endTime=2018-02-02

Para:

storeId: optional,门店id

service\_number: optional,售后单号

serviceType: optional, 售后单类型(REFUND-仅退款 RETURN-退货退款
EXCHANGE-换货）

startTime \~ endTime: 若同时提供，则返回创建时间在此范围内的售后单列表

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": {

"totalRow": 1,

"pageNumber": 1,

"lastPage": true,

"firstPage": true,

"totalPage": 1,

"pageSize": 30,

"list": \[

{

"store\_id": "1", //门店id

"reason": "AFSFSF", //原因

"images": "\[\\"http://host/a.jpg\\",\\"http://host/b.jgp\\"\]",

"log": "\[{\\"time\\":\\"2018-07-21
02:38:10\\",\\"user\\":\\"Administrator\\",\\"content\\":\\"afaf\\"}\]",

"user\_name": "Administrator", //订单用户id

"order\_number": "17072614522001811012", //订单号

"express\_company": null, //快递公司

"store\_user\_name": "Administrator", //店员名

"express\_code": null,

"service\_type": "EXCHANGE", //售后单类型（REFUND-仅退款
RETURN-退货退款 EXCHANGE-换货）

"store\_user\_id": "1", //店员id

"refund\_fee": 68, //退款金额

"supplementary\_fee": null, //补交金额

"store\_name": "总店", //门店名称

"id": 3,

"created\_date": "2018-07-21 14:38:13",

"express\_number": null, //快递单号

"service\_number": "180721143813797Administrator", //售后单单号

"order\_id": 1,

"status": "CREATED"

}

\]

}

}

41. **删除订单**

DELETE <http://112.74.26.228:10080/rest/order/>\<order-number\>

注意：

只有订单状态为一下四种时可以删除：

1\. CLOSED\_PAY\_TIMEOUT

2\. CLOSED\_CANCELED

3\. CLOSED\_CONFIRMED 同时 settled 字段是 1

4\. CLOSED\_REFUNDED

parameter:

order-number : 订单号

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"message": "order.delete.success"

}

42. **分享订单拿优惠券**

POST <http://112.74.26.228:10080/rest/order_share>

只有CLOSED\_CONFIRMED的订单才可以分享。

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data：

{

"order\_number": "2343243242"

}

Return:

{

"status\_code": 1,

"data": {

"code": "wrwfafef",
//分享code，用这个code去构建分享到朋友圈时的链接的参数。

"order\_number": "2343243242"

}

}

43. **查看售后原因列表**

GET <http://112.74.26.228:10080/rest/customer_service_type>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": \[

{

"name": "fasfa",

"id": 1

},

{

"name": "e34543kkk",

"id": 2

}

\]

}

44. **新建售后单**

POST <http://112.74.26.228:10080/rest/order_customer_service>

订单到达 DELIVERED\_CONFIRM\_PENDING (待收货） 可以发起退货申请

订单状态变成 CANCELED\_RETURN\_PENDING （待退货），订单项状态变为
退货中， 退货单状态为新建

后台通过后，退货单变为 待退货

后台收到退货后，变成 待退款

后台完成退款，订单状态变为 DELIVERED\_CONFIRM\_PENDING
（如果还有其他商品没有退货），变为 REFUNDED
（已退款，如果所有商品都退了），订单项状态变为 已退款，退货单状态变为
已退款。

退货单状态 ： 待处理（CREATED）， RETURN\_PENDING (待退货），
REFUND\_PENDING (待退款） REFUNDED （已退款）， CANCELED （取消/拒绝）

当订单状态是**CONFIRMED\_DELIVER\_PENDING** 或者**DELIVERED\_CONFIRM\_PENDING** 时，可以发起退款
（service\_type is REFUND) 请求。

当订单状态是**DELIVERED\_CONFIRM\_PENDING** 时，可以发起退货退款
（service\_type is RETURN) 请求 或 换货 （service\_type is EXCHANGE)
请求。

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

"order\_number": "2342323432432", //订单号

"service\_type": "RETURN", //RETURN: 退货退款, REFUND: 仅退款，
EXCHANGE: 换货

"reason": "AFSFSF", //原因

"content": "不要了。", //回复信息

"images": \["http://localhost/image/a.jpg",
"http://loalhost/image/b.jpg"\],

"returns": \[ 退货产品

{

"product\_id": 1,

"quantity": 2

},

{

"product\_id": 2,

"quantity": 2

}

\]

}

45. **查看售后单**

GET <http://112.74.26.228:10080/rest/order_customer_service/:id>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Parameter: id

售后单状态说明：

CREATED - 待处理

HANDLING - 处理中

RETURN\_PENDING - 等待货品寄回

DELIVING - 换货中

REFUND\_PENDING - 待退款

REFUNDED - 已退款

CANCELED - 已取消

EXCHANGED - 已换货

Return:

{

"status\_code": 0,

"data": {

"reason": "AFSFSF",

"express\_code": null,

"service\_type": "RETURN",

"images": \[

"http://o9ixtumvv.bkt.clouddn.com/20160729173227596-Vo1I7nGC.png",

"http://o9ixtumvv.bkt.clouddn.com/20160729173227596-Vo1I7nGC.png"

\],

"log": \[

{

"time": "2016-07-29 05:39:19",

"user": "Administrator",

"content": "不要了。"

}

\],

"id": 1,

"created\_date": "2016-07-29 17:39:19",

"express\_number": null,

"order\_id": 1,

"express\_company": null,

"status": "CREATED"

}

}

46. **更新售后单**

PUT <http://112.74.26.228:10080/rest/order_customer_service/:id>

对申请退货的订单更新物流信息.

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Parameter:

id

Data:

{

"express\_company": "ABC", //optional, 快递公司名称

"express\_number": "23234324", //optional, 快递单号

"content": "anymessage" //optional， 回复给平台的消息

}

47. **微信支付**

GET <http://www.kequandian.net/app/payment/wpay/>\<order-number\>

微商城专用支付URL。

注意： 这个URL不是API的地址，是app所在服务器的地址. 可以直接访问
/app/payment/wpay/\<order\_number\>

新建订单成功后，把order\_number作为参数调用这个URL，会发引微信支付请求。

48. **微信支付码生成**

POST <http://112.74.26.228:10080/rest/wx/push_order>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

PC商城/PAD端 用于生成支付二维码。

PC端应该根据返回的codeUrl生成二维码，给用户扫码

Data:

{

"order\_type": "Order",

"order\_number": "12346", //订单号

"type": "NATIVE" //type必须是NATIVE

}

Return:

{

"status\_code": 0,

"data": {

"timeStamp": "1533188289",

"codeUrl": "weixin://wxpay/bizpayurl?pr=bJ1XIh4",

"package": "prepay\_id=wx02133732079021563094f24c1615005248",

"paySign": "7EEC46D61249DD469759CF598284A0DC",

"totalFee": "11",

"appId": "wx117676b671891683",

"signType": "MD5",

"title": "DEMO",

"nonceStr": "1533188289855"

}

}

49. **确认订单**

PUT <http://112.74.26.228:10080/rest/order/0000000101455770560193531>

用户收货后确认订单。订单当前状态是 DELIVERED\_CONFIRM\_PENDING
时才可以确认。

parameter: ORDER-NUMBER

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

"status":"CLOSED\_CONFIRMED"

}

Return:

{

"message": "order.updated",

"status\_code": 0

}

Error Return:

{

"message": "order.status.transfer.error",

"status\_code": 1

}

50. **查看订单物流信息**

GET <http://112.74.26.228:10080/rest/express_info?order_number=0000000101455770560193531>

parameter:

order\_number - ORDER-NUMBER

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

state:

/\* 快递单当前的状态 ：　

0：在途，即货物处于运输过程中；

1：揽件，货物已由快递公司揽收并且产生了第一条跟踪信息；

2：疑难，货物寄送过程出了问题；

3：签收，收件人已签收；

4：退签，即货物由于用户拒签、超区等原因退回，而且发件人已经签收；

5：派件，即快递正在进行同城派件；

6：退回，货物正处于退回发件人的途中；

\*/

Return:

{

"com": "baishiwuliu",

"data": \[{

"context": "镇江市\|签收\|镇江市【新句容】，百世邻里下蜀代理点
已签收",

"time": "2016-06-19 18:12:40"

}, {

"context": "镇江市\|派件\|镇江市【新句容】，【下蜀
陈龙/18112812262】正在派件",

"time": "2016-06-19 11:26:05"

}, {

"context": "镇江市\|到件\|到镇江市【新句容】",

"time": "2016-06-19 07:20:20"

}, {

"context": "南京市\|发件\|南京市【南京转运中心】，正发往【新句容】",

"time": "2016-06-19 02:24:17"

}, {

"context": "南京市\|到件\|到南京市【南京转运中心】",

"time": "2016-06-19 01:31:20"

}, {

"context": "广州市\|到件\|到广州市【广州转运中心】",

"time": "2016-06-18 02:24:44"

}, {

"context":
"广州市\|发件\|广州市【广州白云石槎分部】，正发往【广州转运中心】",

"time": "2016-06-18 01:12:42"

}, {

"context":
"广州市\|收件\|广州市【广州白云石槎分部】，【田001/02036450972】已揽收",

"time": "2016-06-17 18:45:46"

}, {

"context":
"广州市\|发件\|广州市【广州转运中心】，正发往【南京转运中心】",

"time": "2016-06-10 04:13:25"

}\],

"comcontact": "400-8856-561",

"succeed": true,

"nu": "70534708088780",

"company": "baishiwuliu",

"state": "3",

"message": "ok",

"status": "1"

}

Failure Return:

{

"message": "cannot.find.express.info",

"status\_code": 1

}

51. **购物车列表**

GET <http://112.74.26.228:10080/rest/shopping_cart>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": \[{

"created\_date": "2016-04-25 19:15:45",

"id": 3,

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"price": null,
//price正常情况是有的，如果为null，则表示出错了，对应两种出错原因：1.由于用户未配置默认配

//送区域而不能计算价格；2.用户配置了默认配送区域，但对应的批发活动的区域价格定义中没有匹配

//的，也不能计算价格

"msg": "尚未配置默认配送区域，将不能计算价格", //如果price为

//null，则会提供该msg域，提示错误信息，有两种错误信息，分别对应上述两种出错原因

"marketing": "WHOLESALE", //营销活动 （WHOLESALE代表批发活动）

"marketing\_id": "1", //批发活动id

"product\_id": 1,

"fare\_id": 1, //运费模版ID

"product\_name": "超效洁净护理洗衣液2.5L【全国包邮】",

"quantity": 1,

"user\_id": 4,

"product\_specification\_name": "a1",//规格名称

"product\_specification\_id": 2 //规格ID，提交订单时用

},{

"created\_date": "2016-04-25 19:15:45",

"id": 3,

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"price": 34.80,

"product\_id": 1,

"fare\_id": 1, //运费模版ID

"product\_name": "超效洁净护理洗衣液2.5L【全国包邮】",

"quantity": 1,

"user\_id": 4,

"product\_specification\_name": "a1",//规格名称

"product\_specification\_id": 2 //规格ID，提交订单时用

}, {

"created\_date": "2016-04-25 19:15:45",

"id": 4,

"cover":
"http://112.74.26.228:8000/p/2b3edeb3c3ca2a12b06893cb12286710.png",

"price": 69.60,

"product\_id": 3,

"fare\_id": 1,

"product\_name": "超效洁净护理洗衣液2.5Lx2瓶【全国包邮】",

"quantity": 1,

"user\_id": 4

}\]

}

52. **添加到购物车**

POST <http://112.74.26.228:10080/rest/shopping_cart?increase=false>

如果已存在，则更新，如果quantity是0，则删除。

parameter:

increase - optional, default true.
如果为true则累加购物车数量，为false则替换数量。

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

\[{

"product\_id": 1,

"quantity": 1,

"product\_specification\_id": 1, //optional, 选择的产品规格ID

"marketing\_id": 1, //optional 营销活动id

"marketing": "WHOLESALE" //optional 营销活动(一般是批发
WHOLESALE,团购是直接下单的）

}, { //非批发产品不需要提供 marketing\_id 和 marketing 字段

"product\_id": 3,

"quantity": 1

}\]

Return 购物车列表:

{

"status\_code": 0,

"data": \[{

"created\_date": "2016-04-25 19:15:45",

"id": 3,

"cover":
"http://112.74.26.228:8000/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"price": 34.80,

"weight": 1000, // 重量

"bulk": 1000, //体积

"product\_id": 1,

"free\_shipping": 1,

"product\_name": "超效洁净护理洗衣液2.5L【全国包邮】",

"freight": 0.00,

"quantity": 1,

"product\_specification\_name": "a1",//规格名称

"user\_id": 4,

"marketing\_id": 1,

"marketing": "WHOLESALE"

}, {

"created\_date": "2016-04-25 19:15:45",

"id": 4,

"cover":
"http://112.74.26.228:8000/p/2b3edeb3c3ca2a12b06893cb12286710.png",

"price": 69.60,

"weight": 1000, // 重量

"bulk": 1000, //体积

"product\_id": 3,

"free\_shipping": 1,

"product\_name": "超效洁净护理洗衣液2.5Lx2瓶【全国包邮】",

"freight": 0.00,

"quantity": 1,

"user\_id": 4,

"marketing\_id": null

"marketing": null

}\]

}

53. **删除购物车**

清空购物车

DELETE <http://112.74.26.228:10080/rest/shopping_cart>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": "shopping\_cart.delete.success"

}

54. **我的地址列表**

GET <http://112.74.26.228:10080/rest/contact>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": \[{

"id": 3,

"zip": "510000",

"detail": "6F",

"phone": "1380000000",

"contact\_user": "Mr Huang",

"street": "jianzhong road",

"province": "GD",

"is\_default": 1,

"street\_number": "50",

"user\_id": 4,

"district": "Tiahne",

"city": "GZ"

}\]

}

55. **添加新地址**

POST <http://112.74.26.228:10080/rest/contact>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

"contact\_user": "Mr Huang",

"phone": "1380000000",

"zip": "510000",

"province": "GD",

"city": "GZ",

"district": "Tiahne",

"street": "jianzhong road",

"street\_number": "50",

"detail": "6F",

"is\_default": 1

}

Return:

{

"status\_code": 0,

"data": "contact.saved"

}

56. **更新地址**

PUT <http://112.74.26.228:10080/rest/contact/id>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

"contact\_user": "Mr Huang",

"phone": "1380000000",

"zip": "510000",

"province": "GD",

"city": "GZ",

"district": "Tiahne",

"street": "jianzhong road",

"street\_number": "50",

"detail": "6F",

"is\_default": 0

}

Return:

{

"status\_code": 0,

"data": {

"id": 1,

"contact\_user": "Mr Huang",

"phone": "1380000000",

"zip": "510000",

"province": "GD",

"city": "GZ",

"district": "Tiahne",

"street": "jianzhong road",

"street\_number": "50",

"detail": "6F"

"is\_default": 0,

"user\_id": 1

}

}

\</code\>

57. **删除地址**

DELETE <http://112.74.26.228:10080/rest/contact/id>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": "contact.deleted"

}

58. **得到默认地址**

GET <http://112.74.26.228:10080/rest/default_contact>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": {

"id": 73,

"zip": "510000",

"detail": "5F",

"phone": "1380000000",

"contact\_user": "Mr Huang",

"street": "jianzhong roadxxxxx",

"province": "广东省",

"is\_default": 1,

"street\_number": "50",

"user\_id": 4,

"district": "天河区",

"city": "广州市"

}

}

59. **更新默认地址**

PUT <http://112.74.26.228:10080/rest/default_contact/id>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"message": "contact.updated",

"status\_code": 0

}

60. **默认快递**

GET <http://112.74.26.228:10080/rest/default_express>

Return:

{

"status\_code": 0,

"data": {

"code": "ff",

"name": "天天快递",

"id": 2,

"is\_default": 1,

"enabled": 1

}

}

61. **运费计算**

POST <http://112.74.26.228:10080/rest/product_carriage>

Data:

{

"delivery\_type": "EXPRESS", //可选项：EXPRESS, SELF\_PICK, FLASH,
默认EXPRESS

"province": "广东",

"city": "广州",

"data":\[

{

"fare\_id": 1,

"price": 23.20,

"quantity": 4,

"weight": 500, //该产品的重量，从product可以拿到，单位是g

"bulk": 100 //该产品的体积， 可以忽略

}

\]

}

Return:

{

"status\_code": 0,

"data": {

"carriage": 4.00, //运费

"message": "付同样的运费,还可以拼单0.30KG哦.",

"delta": -180.00
//可忽略。距离满包邮的差额。注意：这是一个负数。只有是负数时才表示离满包邮有差额。

}

}

62. **查询产品限购**

GET <http://112.74.26.228:10080/rest/product_purchase_strategy?productId=234&quantity=2>

parameter:

productId - 产品ID

quantity - 购买数量

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

可以购买，

Return:

{

"status\_code": 0,

"message": "ok"

}

限购了， 不能购买，

Return:

{

"status\_code": 1,

"message": "超出购买限额, 限购2件, 你过去10天内已购买过1件. "

}

63. **拥金API**

64. **查看提现账号信息**

GET <http://112.74.26.228:10080/rest/withdraw_account>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": \[{

"id": 1,

"bank\_name": null,

"owner\_name": "Mr.A",

"account": "234234234324",

"user\_id": 1,

"type": "ALIPAY"

}\]

}

65. **添加提现账号信息**

POST <http://112.74.26.228:10080/rest/withdraw_account>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Type:

public enum Type {

ALIPAY, //支付宝

WECHAT, //微信

BANK //银行

}

Data:

{

"owner\_name": "Mr.A",

"type": "ALIPAY",

"account": "234234234324",

"bank\_name":"中国工商银行科韵路支行" //当type为BANK时需要

}

Return:

{

"message": "withdraw.account.created",

"status\_code": 0

}

66. **删除提现账号信息**

DELETE <http://112.74.26.228:10080/rest/withdraw_account/id>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Parameter:

id - 账户ID

Return:

{

"message": "withdraw.account.deleted",

"status\_code": 0

}

67. **查看余额**

GET <http://112.74.26.228:10080/rest/owner_balance>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Success Return:

{

"status\_code": 0,

"data": {

"total\_reward": 8, //总提成

"balance": 2, //可用余额

"is\_agent": true, //是否是代理商

"is\_seller": true, //是否是销售商

"is\_partner": true, //是否是经销商

"is\_crown": true, //是否皇冠

"is\_crown\_ship\_temp": true,
//是否为临时皇冠，临时皇冠不能进入线下门店

"is\_physical": true, //是否线下资格

"is\_copartner": true, //是否合伙人

"partner\_pool\_count": 9, //合伙人池人数

"partner\_level": { //如果不是经销商，那么就为null

"id": 1,

"level": 1, //表示该经销商的级别，1表示一星

"headcount\_quota": 3,

"name": "一星经销商"

},

"next\_partner\_level": { //如果没有下一级，那么就为null

"id": 2,

"level": 2, //下一级别

"headcount\_quota": 3, //下一星的人数

"name": "二星经销商"

},

}，

"msg":
"您现在是临时线下皇冠商，成为永久线下皇冠商需要在4小时内完成2000元的批发任务"
//如果是临时线下皇冠商，则会出现

//此提示

}

68. **申请提现**

POST <http://112.74.26.228:10080/rest/owner_balance>

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

"withdraw\_type": "Wallet", // optional, wallet为提现到零钱帐户

"withdraw\_account\_id": 1, // optional, 账户ID

"withdraw\_cash": 100.00 //提现金額

}

Success Return:

{

"message": "apply.success",

"status\_code": 1

}

Failure Return:

{

"message": "apply.failure",

"status\_code": 1

}

69. **查看提现历史记录**

GET <http://112.74.26.228:10080/rest/reward_cash>

Parameters:

page\_number - optional, 页码，default 1;

page\_size - optional, 每页记录数，default 30;

start\_date - optional, 开始时间， default 上个月;

end\_date - optional, 结束时间， default 今天。

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

状态：

public enum Status {

APPLYING,

REJECTED,

HANDLING,

COMPLETED

}

Return:

{

"status\_code": 0,

"data": \[

{

"id": 2,

"apply\_time": "2016-06-16 13:23:39",

"bank\_name": null,

"account\_number": "oXauMwcMqGeV6zdHGL\_1CcmjlQUg",

"status": "APPLYING",

"name": "Jacky.D.H",

"cash": 100,

"owner\_id": 62,

"complete\_time": null,

"reject\_time": null,

"account\_name": "Jacky.D.H",

"account\_type": "WECHAT"

}

\]

}

70. **查看分成订单汇总信息**

GET <http://112.74.26.228:10080/rest/order_item_reward>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

查询参数:

page\_number - optional, 页数

page\_size - optional, 每页记录数

start\_date - optional, 开始时间

end\_date - optional, 结束时间

默认查当月的数据。

分成类型：

public enum Type {

SELLER, //分销商

AGENT, //代理商

PLATFORM,//平台

PARTNER //合伙人

}

拥金状态：

public enum State {

PENDING\_SETTLEMENT, //待结算

SETTLED, //已结算， 只有已结算的拥金才会有余额里体现

REFUNDED //已退款， 表示该订单已发生退货退款，本分成无效。

}

resp:

{

"status\_code": 0,

"data": {

"order\_item\_rewards": \[

{

"reward": 2,

"created\_time": "2016-06-05 11:11:22",

"level": 1, //结合type一起使用，表示参与分成时的级别，比如type=SELLER,
level=1, 表示作为一级分销商参与分成

"owner\_id": 1,

"order\_number": "1234567890", //订单号

"order\_profit": 20, //整个订单项的利润,页面不应显示出来

"settled\_time": null,

"type": "AGENT", //分成的角色，AGENT：作为代理商分成

"percent": 10, //分成比例，前端ignore，页面不应显示出来

"withdrawn\_time": null,

"product\_name": "A", //产品名称

"product\_price": 20.00, //产品价格

"product\_quantity": 1, //产品数量

"order\_item\_id": 1,

"cover": "/assets/img/find\_user.png", //产品图片

"name": "Administrator",

"id": 4,

"state": "SETTLED", //分成状态

"order\_id": 1,

"payment\_type": "WECHAT",

"point\_exchange\_rate": 100

},

{

"reward": 2,

"created\_time": "2016-06-05 11:11:22",

"level": 3,

"owner\_id": 1,

"order\_number": "1234567890",

"order\_profit": 20,

"settled\_time": null,

"type": "PARTNER",

"percent": null,

"withdrawn\_time": null,

"product\_name": "A",

"order\_item\_id": 1,

"cover": "/assets/img/find\_user.png",

"name": "Administrator",

"id": 3,

"state": "PENDING\_SETTLEMENT",

"order\_id": 1,

"payment\_type": "WECHAT",

"point\_exchange\_rate": 100

},

{

"reward": 2,

"created\_time": "2016-06-05 11:11:22",

"level": 1,

"owner\_id": 1,

"order\_number": "1234567890",

"order\_profit": 20,

"settled\_time": null,

"type": "SELLER",

"percent": 10,

"withdrawn\_time": null,

"product\_name": "A",

"order\_item\_id": 1,

"cover": "/assets/img/find\_user.png",

"name": "Administrator",

"id": 2,

"state": "PENDING\_SETTLEMENT",

"order\_id": 1,

"payment\_type": "WECHAT",

"point\_exchange\_rate": 100

},

{

"reward": 2,

"created\_time": "2016-06-05 11:11:22",

"level": null,

"owner\_id": 1,

"order\_number": "1234567890",

"order\_profit": 20,

"settled\_time": null,

"type": "SELF",

"percent": 10,

"withdrawn\_time": null,

"product\_name": "A",

"order\_item\_id": 1,

"cover": "/assets/img/find\_user.png",

"name": "Administrator",

"id": 1,

"state": "PENDING\_SETTLEMENT",

"order\_id": 1,

"payment\_type": "WECHAT",

"point\_exchange\_rate": 100

}

\],

"pending\_reward": 6,

"settled\_reward": 2,

"total\_order\_count": 2,

"settled\_order\_count": 1,

"pending\_order\_count": 1

}

}

71. **查看产品分成**

GET <http://112.74.26.228:10080/rest/product_settlement?id=>\<product-id\>&marketingType=\<type\>&marketingId=\<id\>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

查询参数:

-   id - integer,required, 产品ID

-   marketingType - string, optional, 营销活动类型，如拼团为PIECE-GROUP

-   marketingId - integer, optinal, 营销活动ID

Return:

{

"status\_code": 0,

"data": 30.00

}

72. **分销API**

73. **我的分销商层次信息**

GET <http://112.74.26.228:10080/rest/seller_level>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status\_code": 0,

"data": {

"result": true,

"levels": \[2, 1, 0\], //各级的分销商总数

"max\_level": 3 //三级分销

}

}

74. **我的分销商信息**

GET <http://112.74.26.228:10080/rest/seller>

返回下一级的朋友

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status\_code": 0,

"data": {

"id": 1,

"user\_name": "Administrator",

"partner\_id": null, //合伙人ID

"level": 1,

"partner\_ship": 1, //是否是合伙人

"partner\_pool\_count": 9, //合伙人池人数

"seller\_ship\_time": "2016-04-28 13:08:35", //成为分销商时间

"partner\_ship\_time": "2016-04-28 13:08:35", //成为合伙人时间

"user\_id": 1,

"seller\_ship": 1, //是否是分销商

"parent\_id": null,

"followed": 1, //是否关注公众号

"follow\_time": "2016-05-06 12:00:00", //关注时间

"unfollowed\_children\_count": 0, //未关注的下级总数

"followed\_children\_count": 0, //已关注的下级总数

"agent\_ship": 1, //是否是代理商

"partner\_level": { //如果不是经销商，那么就为null

"id": 1,

"level": 1, //表示该经销商的级别，1表示一星

"headcount\_quota": 3,

"name": "一星经销商"

},

"next\_partner\_level": { //如果没有下一级，那么就为null

"id": 2,

"level": 2, //下一级别

"headcount\_quota": 3, //下一星的人数

"name": "二星经销商"

},

"children": \[{

"seller\_ship\_time": null,

"level": 2, //没用，忽略

"partner\_ship\_time": null,

"user\_name": "abc", //用户名

"avatar": null, //头像URL

"sa\_level": 1,
//属于该分销商的第几级分销商.只有type=all时才有这个属性。

"partner\_id": null,

"user\_id": 3,

"partner\_ship": 0,

"parent\_id": 1,

"id": 3,

"seller\_id": 3,

"seller\_ship": 0,

"followed": 1, //是否关注公众号

"follow\_time": "2016-05-06 12:00:00", //关注时间

"agent\_ship": 1, //是否是代理商

"register\_date": "2018-10-11", //注册时间

"grade": "1" // VIP系统的会员级别ID

}, {

"seller\_ship\_time": null,

"level": 2,

"partner\_ship\_time": null,

"user\_name": "xyz",

"avatar": null,

"sa\_level": 1,

"partner\_id": null,

"user\_id": 9,

"partner\_ship": 0,

"parent\_id": 1,

"id": 9,

"seller\_id": 9,

"seller\_ship": 0,

"followed": 1, //是否关注公众号

"follow\_time": "2016-05-06 12:00:00", //关注时间

"agent\_ship": 0 //是否是代理商

}, {

"seller\_ship\_time": null,

"level": 3,

"partner\_ship\_time": null,

"user\_name": "a",

"avatar": null,

"sa\_level": 2,

"partner\_id": null,

"user\_id": 4,

"partner\_ship": 0,

"parent\_id": 3,

"id": 4,

"seller\_id": 4,

"seller\_ship": 0,

"followed": 1, //是否关注公众号

"follow\_time": "2016-05-06 12:00:00", //关注时间

"agent\_ship": 0 //是否是代理商

}, {

"seller\_ship\_time": null,

"level": 3,

"partner\_ship\_time": null,

"user\_name": "b",

"avatar": null,

"sa\_level": 2,

"partner\_id": null,

"user\_id": 5,

"partner\_ship": 0,

"parent\_id": 3,

"id": 5,

"seller\_id": 5,

"seller\_ship": 0,

"followed": 1, //是否关注公众号

"follow\_time": "2016-05-06 12:00:00", //关注时间

"agent\_ship": 1 //是否是代理商

}\]

}

}

75. **下级分销商信息**

GET <http://112.74.26.228:10080/rest/seller/seller_id>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Parameter: seller\_id - 下级分销商ID

Return:

{

"status\_code": 0,

"data": {

"id": 2,

"user\_name": "a",

"partner\_id": 1,

"level": 2,

"partner\_ship": 0,

"seller\_ship\_time": null,

"partner\_ship\_time": null,

"followed": 1, //是否关注公众号

"follow\_time": "2016-05-06 12:00:00", //关注时间

"children": \[{

"id": 4,

"user\_name": "a1",

"partner\_id": 1,

"level": 3,

"partner\_ship": 0,

"seller\_ship\_time": null,

"partner\_ship\_time": null,

"user\_id": 4,

"seller\_ship": 0,

"parent\_id": 2,

"followed": 1, //是否关注公众号

"follow\_time": "2016-05-06 12:00:00" //关注时间

}, {

"id": 5,

"user\_name": "a2",

"partner\_id": 1,

"level": 3,

"partner\_ship": 0,

"seller\_ship\_time": null,

"partner\_ship\_time": null,

"user\_id": 5,

"seller\_ship": 0,

"parent\_id": 2,

"followed": 1, //是否关注公众号

"follow\_time": "2016-05-06 12:00:00"//关注时间

}\],

"user\_id": 2,

"seller\_ship": 0,

"parent\_id": 1

}

}

76. **申请成为分销商**

POST <http://112.74.26.228:10080/rest/seller>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

申请成为皇冠商时的前提：申请成为皇冠商开关已打开

Data:

{

"real\_name": "Huang",

"phone": "1308888899",

"type": "CROWN" //申请类型，默认不填则为申请 分销商 资格。
CROWN为申请线下皇冠商资格。

}

Return:

{

"status\_code": 0,

"data": {

"seller\_ship": 1

}

}

77. **以扫码方式申请成为某皇冠商的"线下经销商"或"线下皇冠商"**

POST <http://112.74.26.228:10080/rest/physical_seller>

成为皇冠商前提：以扫码方式申请成为皇冠商的开关已经打开

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Tips:

1.若申请人是一个Seller，申请内容是线下经销商，则递交成为线下经销商的申请

2.若申请人本身是一个线下经销商，申请内容是皇冠商，此时会根据自动审核皇冠商机制来自动给予皇冠商资格

3.若申请人是一个Seller,申请内容是线下皇冠，此时会先申请成为线下并自动通过，然后申请成为皇冠，根据自动审核皇冠商机制来自动给予皇冠商资格

Req:

{

"uid": "U00001", //required,推荐人的UID

"real\_name": "黄", //required,申请人真实姓名，用于更新个人信息

"phone": "13800000000", //required,申请人手机，用于更新个人信息

"type": "CROWN",
//optional，省略表示申请成为线下经销商，CROWN表示申请成为线下皇冠商

"province": "广东", //required

"city": "广州", //required

"district": "荔湾区" //required

}

Success Resp:

{

"status\_code": 0,

"message": "apply.success"

}

Error Return:

{

"status\_code": 1,

"message": "user.is.not.crownship"

}

{

"status\_code": 1,

"message": "invalid.user"

}

{

"status\_code": 1,

"message": "invalid.phone"

}

{

"status\_code": 1,

"message": "cannot.apply.yourself"

}

78. **线下经销商查看线下信息**

GET <http://112.74.26.228:10080/rest/physical_seller>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status\_code": 0,

"data": {

"parent\_seller\_id": null,

"parent": null,

"city": null,

"children\_count": 2, //physical\_seller\_children\_count,
physical\_seller\_children 只有具

//有皇冠商资格时才返回。

"user\_name": "Administrator",

"total\_settled\_amount": 0,

"avatar": null,

"uid": "U00000001",

"province": null,

"total\_amount": 0,

"children": \[\], //星级经销商下线列表

"crown\_children": \[ //皇冠商下线列表（包含下级和下下级皇冠商）

{

"parent\_seller\_id": 1,

"city": null,

"level": 1, //1.下级皇冠商 2.下下级皇冠商

"user\_name": "user123",

"total\_settled\_amount": 0,

"crown\_ship": 1,

"real\_name": "user123",

"avatar": null,

"followed": 1,

"uid": "U011707251055190003",

"follow\_time": null,

"province": null,

"total\_amount": 0,

"phone": null,

"district": null,

"latest\_bonus\_date": null,

"id": 182,

"created\_date": "2017-09-19 10:59:06",

"seller\_id": 11014

},

{

"parent\_seller\_id": 11014,

"city": null,

"level": 2,

"user\_name": "关应康",

"total\_settled\_amount": 0,

"crown\_ship": 1,

"real\_name": null,

"avatar":
"http://wx.qlogo.cn/mmopen/vi\_32/AWrNt30IeSoibiaaicZafBbkw39icOzMibCfDSMhQH9uRYxRLQMzUp4hJBHtvYMZn9FwXMkpibM47C0OW94nJU0lyOjw/0",

"followed": 1,

"uid": "U011707271136230002",

"follow\_time": null,

"province": null,

"total\_amount": 0,

"phone": null,

"district": null,

"latest\_bonus\_date": null,

"id": 181,

"created\_date": "2017-09-19 10:58:36",

"seller\_id": 11019

}

\],

"district": null,

"crown\_children\_count": 1,
//只有具有皇冠商资格时才返回。下级皇冠商数量

"crown\_children\_count\_lv2": 1, // 只有具有皇冠商资格时才返回。
下下级皇冠商数量

"latest\_bonus\_date": null,

"id": 179,

"created\_date": "2017-08-09 12:03:07",

"seller\_id": 1

}

}

79. **线下皇冠商查看进货结算明细**

GET <http://112.74.26.228:10080/rest/physical_purchase_summary?month=2017-06>

Parameter:

month - optional,
要查询的月份，格式yyyy-MM,如果不传该参数，则返回所有月份的记录，用于'结算记录'UI。如果传了参数，则返回该月的明细，用于'我的推荐'UI。

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status\_code": 0,

"data": \[

{

"transferred": 0, //是否已转积分系统

"statistic\_month": "2017-09-01", //统计月份

"monthly\_amount": 5600, //本月进货

"total\_settled\_amount": 848, //累计总提成. 当有month参数时才返回该项

"monthly\_settled\_amount": 848, //提成金额

"monthly\_expected\_settled\_amount": 0, //上级期望提成（前端用不到）

"monthly\_expected\_settled\_amount\_lv2": 0,
//上上级期望提成（前端用不到）

"my\_recommended\_sellers": \[ //我的推荐线下经销商.
当有month参数时才返回该项（包含两级，下级排前面，下下级排

//后面）

{

"transferred": 0,

"level": 1, //1.下级 2.下下级

"user\_name": "user123",

"statistic\_month": "2017-09-01",

"monthly\_amount": 3200,

"avatar": null,

"monthly\_settled\_amount": 960,

"monthly\_expected\_settled\_amount\_lv2": 0,

"uid": "U011707251055190003",

"transferred\_amount": 0,

"monthly\_expected\_settled\_amount": 728,

"settlement\_proportion": 100,

"id": 192,

"seller\_id": 11014

},

{

"transferred": 0,

"level": 2,

"user\_name": "关应康",

"statistic\_month": "2017-09-01",

"monthly\_amount": 6000,

"avatar":
"http://wx.qlogo.cn/mmopen/vi\_32/AWrNt30IeSoibiaaicZafBbkw39icOzMibCfDSMhQH9uRYxRLQMzUp4hJBHtvYMZn9FwXMkpibM47C0OW94nJU0lyOjw/0",

"monthly\_settled\_amount": 0,

"monthly\_expected\_settled\_amount\_lv2": 120,

"uid": "U011707271136230002",

"transferred\_amount": 0,

"monthly\_expected\_settled\_amount": 960,

"settlement\_proportion": 100,

"id": 191,

"seller\_id": 11019

}

\],

"transferred\_amount": 0,

"total\_amount": 5600,

"settlement\_proportion": 100,

"id": 193,

"seller\_id": 1

}

\]

}

80. **线下代理商查看进货结算明细**

GET <http://112.74.26.228:10080/rest/agent_summary?month=2017-08>

Parameter:

month - optional,
要查询的月份，格式yyyy-MM,如果不传该参数，则返回所有月份的记录，用于'结算记录'UI。如果传了参数，则返回该月的明细。

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Tips:
1.对于每个线下代理，其最后一次生成年终奖的时间假设为2016-08-04，则程序会于2017-08-04生成他的年终奖（如果从来未生成过年终奖，则把他成为线下的日期作为最后一次生成年终奖时间）。
因此在2017-08-04之前访问此api将会看不到由2016-08-04\~2017-08-04的年终奖。
2.为简单起见，只有生成年终奖的月份才会看到年终奖。

Return:

{

"status\_code": 0,

"data": \[

{

"amount": 2600, //进货额

"transferred": 0, //是否已转积分系统

"pcd\_name": "广东", //地区名称

"bonus": { //年终奖金

"settled\_amount": 11969,

"amount": 23938,

"transferred": 0,

"transferred\_amount": 0,

"statistic\_month": "2017-07-25",

"pcd\_id": 2147,

"year\_statistic\_amount": 0, //奖金项没有"年累计订单额"

"settlement\_proportion": 50,

"id": 19,

"end\_month": "2018-07-25",
//代表从statistic\_month到end\_month的年终奖金

"seller\_id": 11014

},

"statistic\_month": "2017-10-01", //开始月份

"pcd\_id": 2147,

"year\_statistic\_amount": 2600, //年累计订单额

"settled\_amount": 7.8, //提成额

"transferred\_amount": 0, //已转积分

"agentPurchaseJournals": \[ //根据产品，提成比例来汇总的订单明细

{

"sum\_settled\_amount": 6, //本月提成

"sum\_final\_price": 2000, //进货金额

"product\_id": 149, //产品id

"agent\_proportion\_percentage": "0.30", //提成比例（0.30表示0.30%）

"product\_name": "碧丽雅超效洁净手洗专用洗衣液1.25L\*10瓶/箱"
//产品名称

},

{

"sum\_settled\_amount": 12,

"sum\_final\_price": 4000,

"product\_id": 673,

"agent\_proportion\_percentage": "0.30",

"product\_name": "十美优品净澈水润型沐浴露600ml\*4瓶/箱"

},

{

"sum\_settled\_amount": 1.3,

"sum\_final\_price": 432,

"product\_id": 675,

"agent\_proportion\_percentage": "0.30",

"product\_name": "十美优品滋养修护型护发素600ml\*4瓶/箱"

}

\],

"settlement\_proportion": 0, //提成比例

"id": 39,

"end\_month": null, //结束月份

"seller\_id": 11014

},

{

"amount": 2600,

"transferred": 0,

"pcd\_name": "广东-广州",

"bonus": {

"settled\_amount": 212.16,

"amount": 10608,

"transferred": 0,

"transferred\_amount": 0,

"statistic\_month": "2017-07-25",

"pcd\_id": 2148,

"year\_statistic\_amount": 0,

"settlement\_proportion": 2,

"id": 22,

"end\_month": "2018-07-25",

"seller\_id": 11014

},

"statistic\_month": "2017-10-01",

"pcd\_id": 2148,

"year\_statistic\_amount": 2600,

"settled\_amount": 7.8,

"transferred\_amount": 0,

"agentPurchaseJournals": \[

{

"order\_user\_id": 11019,

"agent\_proportion": 3,

"quantity": 20,

"pcd\_name": "广州",

"pcd\_id": 2148,

"product\_specification\_name": null,

"product\_name": "十美优品净澈水润型沐浴露600ml\*4瓶/箱",

"order\_item\_id": 5529,

"settled\_amount": 4.8,

"order\_user\_name": "关应康",

"final\_price": 1600,

"price": 80,

"product\_id": 673,

"percentage": 10,

"marketing\_name": "十美优品净澈水润型沐浴露600ml\*4瓶/箱",

"marketing\_id": 14,

"id": 7,

"create\_date": "2017-10-09 11:21:34",

"seller\_id": 11014,

"product\_cover":
"http://images.10mup.com/20170708154457918-gkpUE7r4.jpg"

},

{

"order\_user\_id": 11019,

"agent\_proportion": 3,

"quantity": 10,

"pcd\_name": "广州",

"pcd\_id": 2148,

"product\_specification\_name": null,

"product\_name": "碧丽雅超效洁净手洗专用洗衣液1.25L\*10瓶/箱",

"order\_item\_id": 5530,

"settled\_amount": 3,

"order\_user\_name": "关应康",

"final\_price": 1000,

"price": 100,

"product\_id": 149,

"percentage": 10,

"marketing\_name": "碧丽雅超效洁净手洗专用洗衣液1.25L\*10瓶/箱",

"marketing\_id": 11,

"id": 8,

"create\_date": "2017-10-09 11:21:34",

"seller\_id": 11014,

"product\_cover":
"http://images.10mup.com/20160914142106802-oFWNcqv1.jpg"

}

\],

"settlement\_proportion": 0,

"id": 42,

"end\_month": null,

"seller\_id": 11014

}

\]

}

81. **线下代理商查看年终奖励对照表**

GET <http://112.74.26.228:10080/rest/physical_agent_bonus?pcd_id=1>

Paras:

pcd\_id: required，地区id

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

{

"status\_code": 0,

"data": \[

{

"id": 1,

"percentage": 10, //奖金比例 （当min\_amount\<销售额\<=max\_amount
，应用此percentage）

"min\_amount": 0, //销售额下限

"max\_amount": 1000, //销售额上限

"pcd\_id": 1

},

{

"id": 2,

"percentage": 20,

"min\_amount": 1000,

"max\_amount": -1, //-1表示无上限

"pcd\_id": 1

}

\]

}

82. **线下皇冠商查看被推荐人的进货明细列表**

GET <http://112.74.26.228:10080/rest/physical_purchase_journal/:seller_id?month=2017-06>

Req Para:

seller\_id: required，被推荐人的seller\_id

month: optional，省略则列出所有月份的进货明细，格式为yyyy-MM

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Resp:

{

"status\_code": 0,

"data": \[

{

"order\_number": "123456xxx", //订单号

"created\_date": "2017-06-12 13:53:00",

"amount": 1000,
//进货额（不是指该订单的进货额，而是该订单其中1个订单项的进货额）

"id": 2,

"order\_item\_id": 1, //订单项id

"product\_name": "油条", //产品名称

"seller\_id": 2, //被推荐人的seller\_id（即传过来的）

"order\_id": 1, //订单id

"product\_settlement\_proportion": 20, //产品提成比例

"expected\_reward": 30, //预期提成金额，不是真正的提成金额

"note": null

},

{

"order\_number": "123456xxx",

"created\_date": "2017-06-12 13:53:20",

"amount": 3000,

"id": 1,

"order\_item\_id": 2,

"product\_name": "飞机",

"seller\_id": 2,

"order\_id": 1,

"product\_settlement\_proportion": 30,

"expected\_reward": 50,

"note": null

}

\]

}

83. **线下分成比例对照表**

GET <http://112.74.26.228:10080/rest/physical_proportion>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Resp:

{

"status\_code": 0,

"data": \[

{

"id": 1,

"percentage": 2, //分成比例（%）

"min\_amount": 1000, //最小进货额

"max\_amount": 5000 //最大进货额

},

{

"id": 2,

"percentage": 5,

"min\_amount": 5001,

"max\_amount": 10000

},

{

"id": 3,

"percentage": 6,

"min\_amount": 10001,

"max\_amount": 50000

},

{

"id": 4,

"percentage": 8,

"min\_amount": 50001,

"max\_amount": -1

}

\]

}

84. **皇冠经销商,星级经销商申请需知**

GET <http://112.74.26.228:10080/rest/physical_apply_tips?type=CROWN>

para:

type: required，（CROWN 皇冠经销商， STAR星级经销商, ANNOUNCE
线下门店系统公告)

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Resp:

{

"status\_code": 0,

"data": {

"created\_date": null,

"content": "\<p\>内容。。。。\</p\>",

"type": "CROWN",

"id": 1,

"enabled": 1, //是否启用

"last\_modified\_date": "2017-06-23 12:26:50", //最后一次的修改时间

"name": "皇冠需知"

}

}

85. **申请成为合伙人**

POST <http://112.74.26.228:10080/rest/copartner>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"phone": "13900000001",

"name": "黄小二",

"address": "广东广州荔湾区周门路16号"

}

Success Resp:

{

"status\_code": 0,

"message": "ok"

}

Failure Resp:

{

"status\_code": 1,

"message": "already.copartner"

}

86. **合伙人查看团队列表**

GET <http://112.74.26.228:10080/rest/copartner>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Success Resp:

{

"status\_code": 0,

"data": {

"create\_time": "2018-08-23 11:52:14",

"children\_count": 1,

"children": \[

{

"uid": "U011808231159370001",

"follow\_time": null,

"create\_time": "2018-08-23 12:32:15",

"phone": "13800000000",

"user\_name": "13922112131",

"real\_name": "黄",

"avatar": null,

"followed": 0,

"seller\_id": 3

}

\],

"id": 2,

"seller\_id": 2,

"status": "NORMAL"

}

}

Failure Resp:

{

"status\_code": 1,

"message": "not.a.copartner"

}

87. **合伙人查看分成**

GET <http://112.74.26.228:10080/rest/copartner_settlement?month=2018-08>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Success Resp:

{

"status\_code": 0,

"data": {

"settlement\_proportion": 4, //分成比例

"total\_settlement\_amount": 0, //总分成

"total\_amount": 0, //总进货量

"monthly\_amount": 0, //当月进货量

"monthly\_settlement\_amount": 0, //当月提成

"create\_time": "2018-08-23 11:52:14",

"children": \[

{

"seller\_ship\_time": "2018-08-23 11:59:37",

"create\_time": "2018-08-23 12:32:15",

"level": 1,

"partner\_ship\_time": "2018-08-23 12:32:15",

"crown\_id": null,

"user\_name": "13922112131",

"crown\_ship": 1,

"crown\_apply\_failure\_times": 0,

"real\_name": "黄",

"avatar": null,

"followed": 0,

"uid": "U011808231159370001",

"follow\_time": null,

"crown\_ship\_temp": 1,

"partner\_id": null,

"user\_id": 3,

"partner\_ship": 1,

"crown\_ship\_time": "2018-08-23 12:32:55",

"phone": "13800000000",

"parent\_id": null,

"id": 3,

"seller\_ship": 1,

"seller\_id": 3,

"partner\_level\_id": 1,

"monthly\_amount": 0, //当月进货量

"monthly\_settlement\_amount": 0 //当月提成

}

\],

"id": 2,

"seller\_id": 2,

"status": "NORMAL"

}

}

88. **合伙人查看结算记录**

GET <http://112.74.26.228:10080/rest/copartner_settlement>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Success Resp:

{

"status\_code": 0,

"data": \[

{

"statistic\_month": "2018-02",

"settled\_amount": 100, //分成

"transferred\_amount": 10000 //转积分

}

\]

}

89. **合伙人查看团队成员的进货提成明细**

GET <http://112.74.26.228:10080/rest/copartner_settlement/:sellerid?month=2018-08>

Param: sellerId - 团队成员的sellerid

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Success Resp:

{

"status\_code": 0,

"data": \[

{

"product\_name": "洗衣液",

"amount": 100, //进货量

"reward": 10, //提成

"settlement\_proportion": 10 //提成比例

}

\]

}

90. **会员API**

91. **会员级别列表**

GET <http://112.74.26.228:10080/rest/member_level>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

resp:

{

"status\_code": 0,

"data": \[{

"id": 1,

"point": 1000,

"description": null,

"name": "Level 1"

}, {

"id": 2,

"point": 2000,

"description": null,

"name": "Level 2"

}, {

"id": 3,

"point": 5000,

"description": null,

"name": "Level 3"

}, {

"id": 4,

"point": 10000,

"description": null,

"name": "Level 4"

}\]

}

92. **会员信息**

GET <http://112.74.26.228:10080/rest/member>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

resp:

{

"status\_code": 0,

"data": {

"id": 3,

"point": 0,

"birthday": null,

"sex": null,

"address": null,

"description": null,

"name": "abc",

"user\_id": 4,

"level\_id": 1,

"mobile": null

}

}

93. **更新会员信息**

PUT <http://112.74.26.228:10080/rest/member>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

data:

{

"birthday": "1999-10-10",

"sex": 1,

"address": "GZ liwan",

"description": "xxvv",

"name": "abc",

"mobile": "138000000"

}

resp:

{

"message": "member.updated",

"status\_code": 0

}

94. **优惠券列表**

GET <http://112.74.26.228:10080/rest/coupon?status=ACTIVATION&pageNumber=1&pageSize=10>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

查询参数： status - optional, 状态， 默认返回 ACTIVATION 状态的。

pageNumber - optional, 分页页数

pageSize - optional, 每页记录数

状态类型：

public enum Status {

NON\_ACTIVATION, //未激活

ACTIVATION, //已激活

OVERDUE, //已过期

USED //已使用

}

resp:

如果discount不是0，那么就是折扣券，比如"discount": 60, 表示打六折。

如果money不是0， 那么就是代金券。

{

"status\_code": 0,

"data": {

"ACTIVATION": 1,

"USED": 0,

"NON\_ACTIVATION": 1,

"OVERDUE": 0,

"coupons": \[

{

"code": "9e0f38da-8a05-4243-a338-c1d373b2943d",

"discount": 0,

"description": null,

"type": "ORDER",

"display\_name": "a",

"cond": "

\<rule-set name=\\"getFinalPrice\\" \>

\<mvel-rule id=\\"step1\\" multipleTimes=\\"false\\"
exclusive=\\"true\\" valid=\\"true\\"\>

\<condition\>\<!\[CDATA\[true\]\]\>\</condition\>

\<action\>\<!\[CDATA\[finalPrice=totalPrice-4\]\]\>\</action\>

\</mvel-rule\>

\</rule-set\>

",

"valid\_date": "2017-01-13 18:01:44",

"money": 4,

"user\_id": 1,

"name": "q",

"id": 1,

"created\_date": "2017-01-11 18:01:44",

"attribute": "{\\"source\\":\\"SYSTEM\\"}",

"auto\_give": 0,

"status": "ACTIVATION"

}

\]

}

}

95. **点击分享链接领取优惠券**

POST <http://112.74.26.228:10080/rest/coupon>

用户须关注公众号才可以激活优惠券。

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"code": "werwqerweqfaf" //分享码

}

Success resp:

{

"status\_code": 0,

"data": {

"coupon\_taken\_records": \[ //该分享被领取的记录

{

"share\_id": 1,

"user\_id": 1,

"name": "Administrator",

"created\_date": "2016-11-28 10:43:08",

"message": "又有券可用了。",

"coupon\_value": 6

}

\],

"coupons": \[
//该用户领取的优惠券列表，对于第一次点击链接领取时才有这个属性。

{

"code": "1982dbcf-442a-4111-923f-6b20b67eb31e",

"description": null,

"type": "ORDER",

"display\_name": "式",

"valid\_date": "2016-12-01",

"money": 4,

"user\_id": 1,

"name": "aaaa",

"created\_date": "2016-11-28",

"id": 1,

"status": "ACTIVATION"

},

{

"code": "0d0cf6c8-58c4-4df7-91e3-a14e74046b97",

"description": null,

"type": "ORDER",

"display\_name": "33",

"valid\_date": "2016-12-02",

"money": 2,

"user\_id": 1,

"name": "发啊发",

"created\_date": "2016-11-28",

"id": 2,

"status": "ACTIVATION"

}

\],

"coupon\_value": 6 //领取的优惠券价值

}

}

96. **激活优惠券**

PUT <http://112.74.26.228:10080/rest/coupon/id>

领取（激活）优惠券, 用户须关注公众号才可以激活优惠券。

parameter:

id - integer, 优惠券ID

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"status": "ACTIVATION"

}

Failure Resp：

{

"status\_code": 1,

"message": "user.must.be.followed"

}

Success resp:

{

"status\_code": 0,

"message": "activate.success"

}

97. **删除优惠券**

DELETE <http://112.74.26.228:10080/rest/coupon/id>

parameter:

id - integer, 优惠券ID

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Success resp:

{

"status\_code": 0,

"message": "delete.success"

}

98. **用户优惠券通知**

GET <http://112.74.26.228:10080/rest/coupon_notify>

如果还没通知过用户，那么首页可以弹出红包框。

如果 'has\_unread\_coupon\' 为true，那么需要对'个人中心，优惠券'
添加红点 提示用户。

notify为总开关，只有notify为true时才需要弹出红包。

当notify为true时：

如果new\_user为true，则显示'新用户红包'，否则就是显示'恭喜您获得X张优惠券'。

如果is\_user\_followed为true，则显示点击关注领取， 否则显示点击查看。

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Success resp:

{

"status\_code": 1,

"data": {

"notify": true, //需要弹出红包通知用户

"new\_user": true, //是否是新注册用户

"coupon\_count": 2, //当notify为true时才返回

"coupon\_value": 34, //当notify为true时才返回

"is\_user\_followed": true, //用户是否关注公众号

"has\_unread\_coupon": true, //表示用户有未读优惠券,
这时\'个人中心\'需要显示红点

"activation\_coupons": \[

{

"id": 1,

"name": "拼团免单券",

"type": "MARKETING\_PIECE\_GROUP", //
类型为MARKETING\_PIECE\_GROUP表示拼团券

"status": "ACTIVATION"

}

\]

}

}

99. **下单前计算优惠信息**

POST <http://112.74.26.228:10080/rest/coupon_calculation?phone=13800000001>

Para:

phone - optional， 用户手机号，查询该用户的优惠券优惠信息,pad端用

传入订单的产品和价格列表，返回该用户的优惠券对这个订单优惠后的信息

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

\[

{

"product\_id": 1,

"price": 20
//该产品的总价格，注意：不是单价，比如买啦2件，那这里的值应该是单价＊2

},

{

"product\_id": 2,

"price": 39.9

}

\]

Return:

\[

{

"coupon\_id": 1,

"coupon\_name": "全单8折",

"valid\_date"："2016-11-30 11:11:11", //有效时间

"final\_price": 47.92 //这个订单使用这个优惠劵后的总价格

},

{

"coupon\_id": 2,

"coupon\_name": "单品买立减8元",

"valid\_date"："2016-11-30 11:11:11", //有效时间

"final\_price": 51.9

},

{

"coupon\_id": 3,

"coupon\_name": "满50立减5元",

"valid\_date"："2016-11-30 11:11:11", //有效时间

"final\_price": 55.9

}

\]

100. **查看我的优惠券分享信息**

GET <http://112.74.26.228:10080/rest/coupon_share>

下单完成后用户对红包进行了分享，这个api可以查看分享过的列表。

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status\_code": 0,

"data": \[

{

"valid\_date": "2016-12-06 12:18:43",

"code": "e58a9055-f966-4b59-b36d-b8de66bbfc25",

"user\_id": 1,

"order\_number": "12345",

"share\_date": "2016-12-01 12:18:43",

"link":
"http://www.kequandian.net/app/app/coupon?share\_code=e58a9055-f966-4b59-b36d-b8de66bbfc25&invite\_code=a1b2c3",

"id": 1

}

\]

}

101. **我的钱包**

GET <http://112.74.26.228:10080/rest/wallet?phone=1380000001>

Param: phone -
可选，要查看的会员手机号码，管理员可以根据这个参数查看该用户的钱包

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status\_code": 0,

"data": {

"accumulative\_amount": 0, //累计金额

"accumulative\_gift\_amount": 0, //累计赠送

"balance": 0, //余额

"user\_id": 1,

"gift\_balance": 0, //赠送余额

"id": 1

}

}

102. **钱包充值**

POST <http://112.74.26.228:10080/rest/wallet_charge>

充值后调用 支付 页面接口 /payment/wpay/:id?orderType=Wallet

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"id"; 1, // depoist package id

"amount": 121, //充值金额

"description": "xxyy" //描述

}

\</codde\>

Return:

\<code\>

{

"status\_code": 0,

"data": {

"created\_time": "2018-08-08",

"wallet\_id": 1,

"amount": 121,

"description": "xxyy",

"id": 1,

"gift\_amount": 0,

"status": "PAY\_PENDING"

}

}

103. **钱包流水记录**

GET <http://112.74.26.228:10080/rest/wallet_history?pageNumber=1&pageSize=30>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

amount 本次充值额。 balance 本次充值后账户的余额。 gift\_amount:
本次充值赠送额 gift\_balance: 充值后赠送帐户的余额。

Return:

{

"status\_code": 0,

"data": \[\]

}

104. **使用钱包支付**

POST <http://112.74.26.228:10080/rest/wallet_pay>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"orderType": "Order",

"orderNumber": "22334",

"password": "134545" // 支付密码

}

Error Return:

{

"status\_code": 1,

"message": "wallet.insufficient.balance"

}

Success Return:

{

"status\_code": 0,

"message": "ok"

}

105. **PAD端使用钱包支付**

POST <http://112.74.26.228:10080/rest/admin/wallet_pay>

Pre-cond:

先调用发送短信验证码给会员手机。

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"orderType": "Order",

"orderNumber": "22334",

"phone": "1308888888",

"captcha": "2345"

}

Error Return:

{

"status\_code": 1,

"message": "wallet.insufficient.balance"

}

Success Return:

{

"status\_code": 0,

"message": "ok"

}

106. **重置钱包支付密码**

POST <http://112.74.26.228:10080/rest/wallet_password>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"oldPassword": "122222", //旧密码，第一次设置密码不用这个字段

"password": "134545" // 支付密码

}

Success Return:

{

"status\_code": 0,

"message": "ok"

}

107. **验证钱包支付密码**

POST <http://112.74.26.228:10080/rest/wallet_verify_password>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"password": "134545" // 支付密码

}

Success Return:

{

"status\_code": 0,

"message": "ok"

}

108. **检查是否已设置支付密码**

GET <http://112.74.26.228:10080/rest/wallet_password>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Success Return:

{

"status\_code": 0,

"data": true

}

窗体顶端

编辑

窗体底端

109. **优惠券类型列表**

GET <http://localhost:8080/rest/admin/coupon_type>

Return:

110. **后台赠送优惠券**

POST <http://localhost:8080/rest/admin/coupon>

Data:

{

"phone": "1390000000",

"couponTypeIds": \[ 1, 2, 3 \]

}

REturn:

{

"status\_code": 1,

"message": "ok"

}

111. **营销API**

112. **拼团列表**

GET <http://112.74.26.228:10080/rest/piece_group_purchase?pageNumber=1&pageSize=0&masterFree=1>

Req Paras:

pageNumber: optional, 页码, default 1

pageSize: optional, 每页记录数, default 30

masterFree: optional, 是否团长免单 （1列出团长免单的活动
0列出非团长免单活动）

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Resp:

{

"status\_code": 0,

"data": {

"pageNumber": 1,

"pageSize": 30,

"totalPage": 1,

"totalRow": 1,

"list": \[{

"id": 4, //拼团活动id

"product\_id": 1, //拼团活动所关联的产品id

"payment\_type": "POINT\|WECHAT",
//该拼团活动支持的支付方式。(WECHAT微信支付 POINT 积分 若两

//种都支持，则用"\|"分隔。如 WECHAT\|POINT）

"marketing\_name": "活动1", //拼团活动名称

"status": "ONSELL", //拼团活动状态。INIT/ONSELL/OFFSELL/LOCK
（LOCK不允许开团，但已开的团

//仍然生效 （成员仍能加入已开的团） OFFSELL：不允许开团，已开的团若已

//拼团成功，则继续生效（但成员不能再加入已开的团了），若拼团未成功，则到时

//间就退款）

"free\_shipping": 0, //是否包邮。 default 1（0
根据产品定义的邮费计算，1 包邮）

"suggested\_price": 1000, //市场价（元）

"sale": 0, //已团件数

"min\_participator\_count": 2, //最小成团人数，default 2

"duration": 118800, //活动有效时间，单位秒。

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170510152514628-dssIB8U8.jpg",
//活动封面

"price": 1134, //团购价（元）

"coupon\_usage": 0, //优惠券使用。default 0（0 不能用优惠券；1
可以用专用优惠券；

//2 可以用系统 优惠券）

"master\_free": 1, //团长是否免单。default 0（0 非免单活动, 1
可以使用免单优惠券）

"description": null //描述

}\],

"promoted\_master": {
//这是随机抽取出来的一位"被推荐"且"已支付"的团长

"id": 1,
//团长id（当团员要入团时，需要指定要加入哪个团长的团，此时用到团长id）

"product\_id": 1, //产品id

"payment\_type": "POINT\|WECHAT",
//该拼团活动支持的支付方式。(WECHAT微信支付 POINT 积分 若两

//种都支持，则用"\|"分隔。如 WECHAT\|POINT）

"marketing\_name": "活动1", //拼团活动名称

"marketing\_short\_name": "活动1缩略名",

"free\_shipping": 0, //是否包邮。 default 1（0
根据产品定义的邮费计算，1 包邮）

"suggested\_price": 1000, //市场价（元）

"piece\_group\_purchase\_status": "ONSELL",
//拼团活动状态。INIT/ONSELL/OFFSELL/LOCK

//（LOCK 不允许开团，但已开的团仍然生效（成员仍

//能加入已开的团） OFFSELL： 不允许开团，已开的

//团若已拼团成功，则继续生效（但成员不能再加入已

//开的团了），若拼团未成功，则到时间就退款）

"sale": 0, //已团件数

"min\_participator\_count": 2, //最小成团人数，default 2

"user\_name": "aaa", //该团长的用户名

"duration": 118800, //活动有效时间，单位秒

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170510152514628-dssIB8U8.jpg",
//活动封面

"price": 1134, //团购价（元）

"coupon\_usage": 0, //优惠券使用。default 0（0 不能用优惠券；1
可以用专用优惠券；

//2 可以用系统 优惠券）

"master\_free": 1, //团长是否免单。default 0（0 非免单活动, 1
可以使用免单优惠券）

"end\_time": "2017-05-12 09:52:28", //结束时间

"description": null,

"promoted": 1, //推荐进入活动详情页方便其他用户参团, 0 不推荐, 1 推荐,
当免单开团的时候该团

//为不推荐,需要团长自己拉人参团

"start\_time": "2017-05-12 09:49:49", //开团时间

"piece\_group\_purchase\_master\_status": "OPENING",
//拼团状态（OPENING正在开团/DEAL拼团

//成功/FAIL拼团失败）

"member\_status": "PAID", //该团长的支付状态（PAID/UNPAID/REFUND）

"piece\_group\_purchase\_id": 4, //拼团活动id

"user\_id": 2, //该团长的user\_id

"user\_avatar": null //该团长的头像

}

}

}

113. **拼团详情**

GET <http://112.74.26.228:10080/rest/piece_group_purchase/:id>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Req Paras:

id: required, 活动id

Resp：

{

"status\_code": 0,

"data": {

"id": 1,

"marketing\_name": "活动1", //拼团活动名称

"marketing\_short\_name": "活动1缩略名",

"product\_id": 1,

"payment\_type": "WECHAT",
//该拼团活动支持的支付方式。(WECHAT微信支付 POINT 积分 若两种都支持，

//则用"\|"分隔。如 WECHAT\|POINT）

"status": "ONSELL", //状态。INIT/ONSELL/OFFSELL/LOCK
（LOCK不允许开团，但已开的团仍然生效

//（成员仍能加入已开的团） OFFSELL：不允许开
团，已开的团若已拼团成功，则

//继续生效（但成员不能再加入已开的团了），若拼团未成功，则到时间就退款）

"min\_participator\_count": 2, //最小成团人数，default 2

"price": 50.00, //团购价（元）

"suggested\_price": 233.00, //市场价（元）

"sale": 0, //已团件数

"coupon\_usage": 1, //优惠券使用。default 0（0 不能用优惠券；1
可以用专用优惠券；2 可以用系统优惠券）

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170511111002449-3OUYLBt6.jpg",
//活动封面

"duration": 7200, //有效时间，单位秒。比如有效时间为
3600秒，某用户在01:00:00开团，则该团的结束时间

//为02:00:00

"free\_shipping": 0, //是否包邮。 default 1（0
根据产品定义的邮费计算，1 包邮）

"master\_free": 1, //团长是否免单。default 0（0 非免单活动, 1
可以使用免单优惠券）

"description": null,

"product": { //参考产品api的说明

"free\_shipping": 0,

"freight": 0.00,

"last\_modified\_date": "2017-05-11 11:09:40",

"promoted": 0,

"specifications": \[\],

"sales": 0,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170511110938953-VIdliaE0.jpg",

"category\_id": 1,

"price": 233.00,

"id": 1,

"sort\_order": 100,

"barcode": null,

"store\_location": null,

"cost\_price": 33.00,

"covers":
\["http://o9ixtumvv.bkt.clouddn.com/20170511110938953-VIdliaE0.jpg"\],

"weight": 33,

"stock\_balance": 1000,

"brand\_id": null,

"unit": "件",

"suggested\_price": 3333.00,

"name": "产品1",

"short\_name": "缩略名1",

"created\_date": "2017-05-11 11:09:39",

"fare\_id": 1,

"bulk": null,

"partner\_level\_zone": 1,

"view\_count": 0,

"status": "ONSELL",

"description": "产品描述"

},

"promoted\_masters": \[{
//这是由该拼团活动所有"被推荐"且"已支付"的团长组成的列表

"id": 1,
//团长id（当团员要入团时，需要指定要加入哪个团长的团，此时用到团长id）

"members\_count": 2, //目前参团人数

"paid\_members\_count": 1, //目前已支付人数

"status": "OPENING",

"member\_status": "PAID", //该团长的支付状态（PAID/UNPAID/REFUND）

"end\_time": "2017-05-12 20:52:25", //结束时间

"promoted": 1, //推荐进入活动详情页方便其他用户参团, 0 不推荐, 1 推荐,
当免单开团的时候该团

//为不推荐,需要团长自己拉人参团

"start\_time": "2017-05-12 18:08:44", //开团时间

"user\_id": 1,

"user\_name": "张三", //团长名

"user\_avatar": null, //团长头像

"piece\_group\_purchase\_id": 1 //拼团活动id

},{

"id": 2,

"members\_count": 2, //目前参团人数

"paid\_members\_count": 1, //目前已支付人数

"status": "OPENING",

"member\_status": "PAID", //该团长的支付状态（PAID/UNPAID/REFUND）

"end\_time": "2017-05-12 11:52:28",

"promoted": 1,

"start\_time": "2017-05-12 09:49:49",

"user\_id": 2,

"user\_name": "张三", //团长名

"user\_avatar": null, //团长头像

"piece\_group\_purchase\_id": 1

}\]

}

}

Error Resp

{

"status\_code": 1,

"message": "pieceGroupPurchase.not.found"

}

114. **我的拼团列表**

GET <http://112.74.26.228:10080/rest/my_piece_group_purchase?pageNumber=1&pageSize=10&status=OPENING>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Req Paras:

pageNumber: optional,default 1

pageSize: optional,default 30

status: optional, 拼团状态（OPENING正在开团/DEAL拼团成功/FAIL拼团失败）

Resp:

{

"status\_code": 0,

"data": {

"pageNumber": 1,

"pageSize": 30,

"totalPage": 1,

"totalRow": 1,

"list": \[{

"order\_number": "order\_number1",

"total\_members\_count": 2, //拼团成员总数

"paid\_members\_count": 1, //已支付的成员总数

"product\_id": 1,

"status": "PAID", //支付状态（UNPAID未支付/PAID已支付/REFUND已退款）

"marketing\_name": "活动1", //拼团活动名称

"marketing\_short\_name": "活动1缩略名",

"payment\_type": "POINT" //该用户支付订单的方式

"free\_shipping": 0, //是否包邮。 default 1（0
根据产品定义的邮费计算，1 包邮）

"suggested\_price": 1000, //市场价（元）

"piece\_group\_purchase\_status": "ONSELL",
//拼团活动状态。INIT/ONSELL/OFFSELL/LOCK （

//LOCK不允许开团，但已开的团仍然生效（成员仍能加入已

//开的团） OFFSELL：不允许开 团，已开的团若已拼团成

//功，则继续生效（但成员不能再加入已开的团了），若拼团

//未成功，则到时间就退款）

"sale": 0, //已团件数

"min\_participator\_count": 2, //最小成团人数，default 2

"duration": 118800, //有效时间，单位秒。比如有效时间为
3600秒，某用户在01:00:00开团，则该团

//的结束时间为02:00:00

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170510152514628-dssIB8U8.jpg",
//活动封面

"price": 1134, //团购价（元）

"coupon\_usage": 0, //优惠券使用。default 0（0 不能用优惠券；1
可以用专用优惠券；2 可以用系

//统优惠券）

"master\_free": 1, //团长是否免单。default 0（0 非免单活动, 1
可以使用免单优惠券）

"end\_time": "2017-05-12 09:52:25", //结束时间

"description": null,

"promoted": 1, //推荐进入活动详情页方便其他用户参团, 0 不推荐, 1 推荐,
当免单开团的时候该团

//为不推荐,需要团长自己拉人参团

"start\_time": "2017-05-10 18:08:44", //开团时间

"piece\_group\_purchase\_master\_status": "OPENING",
//拼团状态（OPENING正在开团/DEAL拼团

//成功/FAIL拼团失败）

"user\_id": 1,

"piece\_group\_purchase\_id": 4, //拼团活动id

"created\_time": "2017-05-12 11:31:09" //加入该拼团的时间

}\]

}

}

115. **我的拼团详情**

GET <http://112.74.26.228:10080/rest/my_piece_group_purchase/:id>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Req Paras:

id: required, 拼团活动id

Resp Paras：

同我的拼团列表API。

Resp:

{

"status\_code": 0,

"data": {

"id": 1,

"marketing\_name": "活动1",

"marketing\_short\_name": "活动1缩略名",

"payment\_type": "POINT" //该用户支付订单的方式

"product\_id": 1,

"piece\_group\_purchase\_status": "ONSELL",

"min\_participator\_count": 2,

"price": 200.00,

"suggested\_price": 233.00,

"sale": 50,

"coupon\_usage": 1,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170511111002449-3OUYLBt6.jpg",

"duration": 7200,

"free\_shipping": 0,

"master\_free": 1,

"description": "描述1",

"start\_time": "2017-05-11 12:22:57",

"end\_time": "2017-05-25 12:22:59",

"piece\_group\_purchase\_id": 1,

"promoted": 1,

"piece\_group\_purchase\_master\_status": "OPENING",

"total\_members\_count": 2,

"paid\_members\_count": 1,

"created\_time": "2017-05-10 17:05:07",

"user\_id": 1,

"order\_number": "order\_number1",

"piece\_group\_purchase\_member\_status": "PAID",

"order": { //订单 请参考订单api

"detail": null,

"phone": "13155555555",

"is\_deliver\_reminder": 0,

"contact\_user": "张三",

"remark": "备注1",

"invoice": 0,

"street": null,

"trade\_number": null,

"express\_number": null,

"deal\_date": null,

"express\_company": null,

"city": "广州市",

"id": 1,

"cover": null,

"confirm\_date": null,

"description": "描述1",

"province": "广东省",

"user\_id": 1,

"coupon\_info": null,

"express\_code": null,

"district": "荔湾区",

"deliver\_date": null,

"delivered\_date": null,

"created\_date": "2017-06-05 15:01:13",

"order\_number": "xxx",

"zip": null,

"point\_exchange\_rate": 100,

"marketing": null,

"status": "DELIVERING",

"invoice\_title": null,

"marketing\_description": null,

"receiving\_time": null,

"deliver\_order\_number": null,

"total\_price": 1000,

"previous\_status": null,

"is\_deleted": 0,

"marketing\_id": null,

"settled": 0,

"freight": 500,

"pay\_date": "2017-06-05 15:01:15",

"payment\_type": "POINT"

},

}

}

Error Resp 1：

{

"status\_code": 1,

"message": "pieceGroupPurchase.not.found"

}

Error Resp 1：

{

"status\_code": 1,

"message": "not.your.pieceGroupPurchase"

}

116. **团长详情**

GET <http://112.74.26.228:10080/rest/piece_group_purchase_master/:id>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Req para: id: 团长id

Return:

{

"status\_code": 0,

"data": {

"id": 1, //团长id

"user\_id": 1, //团长的user id

"piece\_group\_purchase\_id": 1, //拼团活动id

"start\_time": "2017-05-27 09:28:19", //创团时间

"end\_time": "2017-05-28 09:28:21", //结束时间

"promoted": 1, //是否为推荐团长

"piece\_group\_purchase\_status": "ONSELL",
//状态。INIT/ONSELL/OFFSELL/LOCK （LOCK不允许开团，但已开的团仍

//然生效（成员仍能加入已开的团） OFFSELL：不允许开 团，已开的团

//若已拼团成功，则继续生效（但成员不能再加入已开的团了），若拼团未成功，

//则到时间就退款）

"piece\_group\_purchase\_master\_status": "OPENING",
//拼团状态（OPENING正在开团/DEAL拼团成功/FAIL拼团失败）

"marketing\_name": "活动1", //拼团活动名称

"marketing\_short\_name": "活动1缩略名",

"min\_participator\_count": 2, //最小成团人数，default 2

"price": 800, //团购价（元）

"suggested\_price": 1000, //市场价（元）

"sale": 0, //已团件数

"coupon\_usage": 0, //优惠券使用。default 0（0 不能用优惠券；1
可以用专用优惠券；2 可以用系统优惠券）

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170526143343912-37RImHeW.jpg",
//活动封面

"duration": 7200, //有效时间，单位秒。比如有效时间为
3600秒，某用户在01:00:00开团，则该团的结束时间

//为02:00:00

"free\_shipping": 1, //是否包邮。 default 1（0
根据产品定义的邮费计算，1 包邮）

"payment\_type": "WECHAT",
//该拼团活动支持的支付方式。(WECHAT微信支付 POINT 积分 若两种都支持，

//则用"\|"分隔。如 WECHAT\|POINT）

"master\_free": 1, //团长是否免单。default 0（0 非免单活动, 1
可以使用免单优惠券）

"description": null,

"product": { //参考产品api的说明

"weight": 10,

"partner\_level\_zone": 1,

"stock\_balance": 1000,

"fare\_id": 1,

"id": 1,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170526142339324-YHykFlst.jpg",

"sales": 0,

"promoted": 0,

"name": "产品1",

"created\_date": "2017-05-26 14:23:40",

"cost\_price": 500,

"status": "ONSELL",

"free\_shipping": 0,

"brand\_id": null,

"category\_id": 1,

"suggested\_price": 2000,

"barcode": null,

"short\_name": "缩略名1",

"bulk": null,

"specifications": \[\],

"unit": "个",

"last\_modified\_date": "2017-05-26 14:23:42",

"price": 1000,

"covers": \[

"http://o9ixtumvv.bkt.clouddn.com/20170526142339324-YHykFlst.jpg"

\],

"freight": 0,

"store\_location": null,

"sort\_order": 100,

"view\_count": 0,

"description": "产品描述"

}

}

}

117. **开团**

POST <http://112.74.26.228:10080/rest/order>

参考 下单前计算优惠信息 api 返回的优惠券，选择一个优惠劵进行下单。

到支付宝支付时，把order-number的值赋给out\_trade\_no进行支付。

微信支付 - WECHAT

积分支付 - POINT

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

//这两个是 "新建订单api" 新增的域

"marketing": "PIECE-GROUP", //required。开团必须是PIECE-GROUP

"order\_items": \[

{

"product\_id": 1,

"product\_specification\_id": 1,

"quantity": 2,

"marketing\_id": 1, //required。拼团活动的ID,
即piece\_group\_purchase的id

}

\...其他需要提供的域同"新建订单api"

}

Return: 同"新建订单api"

118. **参团**

POST <http://112.74.26.228:10080/rest/order>

参考 下单前计算优惠信息 api 返回的优惠券，选择一个优惠劵进行下单。

到支付宝支付时，把order-number的值赋给out\_trade\_no进行支付。

微信支付 - WECHAT

积分支付 - POINT

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

//这两个是 "新建订单api" 新增的域

"marketing": "PIECE-GROUP-JOINT", //required。参团必须是
PIECE-GROUP-JOINT

"order\_items": \[

{

"product\_id": 1,

"product\_specification\_id": 1,

"quantity": 2,

"marketing\_id": 1, //required。所参加拼团的团长ID,
即piece\_group\_purchase\_master的id

}

\...其他需要提供的域同"新建订单api"

}

Return: 同"新建订单api"

119. **批发类别列表**

GET <http://112.74.26.228:10080/rest/wholesale_category>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Returns:

{

"status\_code": 0,

"data": {

"contact": { //用户默认配送地区

"id": 1,

"zip": null,

"detail": null,

"phone": "1234567",

"contact\_user": "张三",

"street": null,

"province": "广东",

"is\_default": 1,

"street\_number": null,

"user\_id": 1,

"district": "荔湾区",

"city": "广州"

},

"categories": \[

{

"id": 2,

"name": "批发类别2", //类别名

"sort\_order": 5 //排序，小的在前面

},

{

"id": 1,

"name": "批发类别1",

"sort\_order": 100

}

\]

}

}

120. **批发列表**

GET <http://112.74.26.228:10080/rest/wholesale?categoryId=1>

Tips：如果用户没有设置默认配送地区，则此api不返回批发列表。如果有设置，则只返回配送到用户的默认配送地区的批发列表。

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Req Raras:

categoryId: optional, 批发活动类别id （如提供则列出该类别的批发活动）

Return:

{

"status\_code": 0,

"data": {

"totalRow": 1,

"pageNumber": 1,

"firstPage": true,

"lastPage": true,

"totalPage": 1,

"pageSize": 10,

"list": \[{

"category\_id": 1,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170525151147892-Koka1giH.jpg",//批发活动封面

"sale": 0, //已售个数

"product": { //参考产品api

"free\_shipping": 0,

"freight": 0.00,

"last\_modified\_date": "2017-05-25 15:09:29",

"promoted": 0,

"specifications": \[{ //产品规格列表

"price": 10000.00,

"suggested\_price": 20000.00,

"product\_id": 1,

"name": "红色",

"weight": 20,

"id": 1,

"bulk": 0,

"stock\_balance": 1000,

"cost\_price": 100.00

}, {

"price": 3000.00,

"suggested\_price": 10000.00,

"product\_id": 1,

"name": "银色",

"weight": 10,

"id": 2,

"bulk": 0,

"stock\_balance": 1000,

"cost\_price": 100.00

}\],

"sales": 0,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170525103606389-6Vu95yiR.jpg", //

//产品默认的封面图

"price": 1000.00,

"id": 1,

"sort\_order": 100,

"barcode": null,

"store\_location": null,

"cost\_price": 10.00,

"covers":
\["http://o9ixtumvv.bkt.clouddn.com/20170525153019061-qsQ1cWAF.jpg",

"http://o9ixtumvv.bkt.clouddn.com/20170525153019363-kLyFRGJS.jpg"

\], //产品的封面图列表

"weight": 200,

"stock\_balance": 1000,

"brand\_id": null,

"unit": "台",

"suggested\_price": 2000.00,

"name": "诺基亚",

"short\_name": "诺基亚缩略名",

"created\_date": "2017-05-25 10:36:06",

"fare\_id": 1,

"bulk": null,

"partner\_level\_zone": 1,

"view\_count": 0,

"status": "ONSELL"

},

"pricing": { //与用户默认配送地区相匹配的价格项

"suggested\_retail\_price": 22,

"region": "辽宁",

"id": 8,

"enabled": 1,

"price": 11,

"is\_default": 0,

"wholesale\_id": 1,

"suggested\_wholesale\_price": 44

},

"product\_id": 1, //产品id

"marketing\_name": "批发1", //批发活动名称

"marketing\_short\_name": "活动1缩略名",

"description": "机会难得！！！", //描述

"id": 1,

"status": "ONSELL" //状态。INIT/ONSELL/OFFSELL

"settlement\_proportion": 30, //分成比例

"agent\_proportion": 20, //代理分成比例

"unit": 件 //单位

}\]

}

}

121. **批发详情**

GET <http://112.74.26.228:10080/rest/wholesale/:id>

Tips：如果用户没有设置默认配送地区，则此api不返回指定的批发详情。

Para:

id: required,批发活动id

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": {

"category\_id": 1,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170525151147892-Koka1giH.jpg",
//批发活动封面

"sale": 0, //已售个数

"pricings": \[{ //价格列表。不同地区的批发价格不同。

//1.is\_default为1的价格项表示该价格适合于所有地区（不含专门设置的地区）

//
enabled若为1，则所有地区都配送（除去is\_default为0且enabled为0的价格项）；

//
enabled若为0，则所有地区都不配送（除去is\_default为0且enabled为1的价格项）

//2.is\_default为0的价格项表示专门设置的地区对应的价格（优先于默认价格项），

// enabled若为1，则覆盖默认价格项；

// enabled若为0，则该地区不配送

//3.某些地区不设置，则不配送到该地区。例如
pricings的返回结果为空数组\[\]，则表示

// 所有地区都不配送。

"region": null,

"id": 47,

"price": 900,

"is\_default": 1,

"enabled": 1,

"wholesale\_id": 1,

"suggested\_retail\_price": 1000,

"suggested\_whole\_price": 800,

},{

"region": "江苏-苏州\|江苏-南通",

"id": 48,

"price": 1100,

"is\_default": 0,

"enabled": 0,

"wholesale\_id": 1,

"suggested\_retail\_price": 850, //产品在该地区的线下建议零售价

"suggested\_whole\_price": 800 //产品在该地区的星级经销价

}\],

"product": { //参考产品api

"free\_shipping": 0,

"freight": 0.00,

"last\_modified\_date": "2017-05-25 15:30:19",

"promoted": 0,

"specifications": \[{

"price": 10000.00,

"suggested\_price": 20000.00,

"product\_id": 1,

"name": "红色",

"weight": 20,

"id": 1,

"bulk": 0,

"stock\_balance": 1000,

"cost\_price": 100.00

}, {

"price": 3000.00,

"suggested\_price": 10000.00,

"product\_id": 1,

"name": "银色",

"weight": 10,

"id": 2,

"bulk": 0,

"stock\_balance": 1000,

"cost\_price": 100.00

}\],

"sales": 0,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20170525153019061-qsQ1cWAF.jpg",

"category\_id": 1,

"price": 1000.00,

"id": 1,

"sort\_order": 100,

"barcode": null,

"store\_location": null,

"cost\_price": 10.00,

"covers":
\["http://o9ixtumvv.bkt.clouddn.com/20170525153019061-qsQ1cWAF.jpg",
"http://o9ixtumvv.bkt.clouddn.com/20170525153019363-kLyFRGJS.jpg"\],

"weight": 200,

"stock\_balance": 1000,

"brand\_id": null,

"unit": "台",

"suggested\_price": 2000.00,

"name": "诺基亚",

"short\_name": "诺基亚缩略名",

"created\_date": "2017-05-25 10:36:06",

"fare\_id": 1,

"bulk": null,

"partner\_level\_zone": 1,

"view\_count": 0,

"status": "ONSELL"

},

"pricing": { //与用户默认配送地区相匹配的价格项

"suggested\_retail\_price": 22,

"region": "辽宁",

"id": 8,

"enabled": 1,

"price": 11,

"is\_default": 0,

"wholesale\_id": 1,

"suggested\_wholesale\_price": 44

},

"product\_id": 1, //产品id

"marketing\_name": "批发1", //批发活动名称

"marketing\_short\_name": "批发1缩略名",

"description": "\<p\>机会难得！！！\<br/\>\</p\>", //描述

"id": 1, //活动id

"status": "ONSELL" //活动状态（INIT/ONSELL/OFFSELL）,

"settlement\_proportion": 30, //分成比例

"agent\_proportion": 44, //代理分成比例

"proportionLv1": 24, //下级线下皇冠批发产品时的分成比例 =
分成比例\*下级线下皇冠分成比例

"proportionLv2": 6, //下下级线下皇冠批发产品时的分成比例 =
分成比例\*下下级线下皇冠分成比例

"unit": 件 //单位

}

}

122. **新建批发订单**

POST <http://112.74.26.228:10080/rest/order>

参考 下单前计算优惠信息 api 返回的优惠券，选择一个优惠劵进行下单。

到支付宝支付时，把order-number的值赋给out\_trade\_no进行支付。

微信支付 - WECHAT

积分支付 - POINT

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

//这两个是 "新建订单api" 新增的域

"marketing": "WHOLESALE", //required。新建批发订单必须是WHOLESALE

"order\_items": \[

{

"product\_id": 1,

"product\_specification\_id": 1,

"quantity": 2,

"marketing\_id": 1, //required。批发活动的ID, 即wholesale的id

}

\...其他需要提供的域同"新建订单api"

}

Return: 同"新建订单api"

123. **试用装列表**

GET <http://112.74.26.228:10080/rest/trial>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": \[

{

"short\_note": "洗发水试用",

"note": null,

"end\_time": null,

"shipping\_type": 0,

"index": 100,

"version": 1,

"enabled": 1,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20180709182906045-hyEDbt5L.jpeg",

"start\_time": null,

"payment\_type": null,

"price": 0,

"product\_id": 335,

"name": "洗发水试用-免费",

"id": 1,

"partaken": true //已经参加过

}

\]

}

124. **试用装详情**

GET <http://112.74.26.228:10080/rest/trial/:id>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status\_code": 0,

"data": {

"short\_note": "洗发水试用",

"note": null,

"product": {

"free\_shipping": 0,

"freight": 0,

"last\_modified\_date": "2016-12-22 10:10:36",

"mid": null,

"promoted": 1,

"sales": 9,

"cover": "http://images.10mup.com/20161104102243958-v499XJvA.jpg",

"category\_id": 83,

"price": 12.9,

"sku\_name": null,

"id": 335,

"sort\_order": 1,

"barcode": "6903148126660",

"store\_location": null,

"cost\_price": 10.21,

"weight": 500,

"sku\_id": null,

"stock\_balance": 13,

"brand\_id": null,

"unit": "瓶",

"suggested\_price": 20,

"name": "REJOICE飘柔家庭护理芦荟长效止痒滋润洗发露400ML",

"bar\_code": null,

"short\_name": "止痒滋润洗发露",

"created\_date": "2016-10-07 14:11:51",

"fare\_id": 4,

"bulk": 0,

"partner\_level\_zone": 1,

"sku\_code": null,

"view\_count": 2172,

"status": "ONSELL"

},

"end\_time": null,

"shipping\_type": 0,

"index": 100,

"version": 2,

"enabled": 1,

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20180709182906045-hyEDbt5L.jpeg",

"start\_time": null,

"payment\_type": null,

"price": 0,

"product\_id": 335,

"name": "洗发水试用-免费",

"id": 1,

"partaken": true,

"covers": \[

{

"product\_id": 335,

"id": 1298,

"type": 0,

"sort\_order": 1,

"url": "http://images.10mup.com/20161104102243958-v499XJvA.jpg"

},

{

"product\_id": 335,

"id": 1299,

"type": 0,

"sort\_order": 2,

"url": "http://images.10mup.com/20161104102242227-T17IgsG8.jpg"

},

{

"product\_id": 335,

"id": 1300,

"type": 0,

"sort\_order": 3,

"url": "http://images.10mup.com/20161104102241687-lfedAC1r.jpg"

}

\]

}

}

125. **新建试用装申请订单**

POST <http://112.74.26.228:10080/rest/order>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

//这两个是 "新建订单api" 新增的域

"marketing": "TRIAL", //required。新建试用装订单必须是TRIAL

"order\_items": \[

{

"product\_id": 1, // 该试用装的产品ID

"product\_specification\_id": 1, //规格号，如果有就带上

"quantity": 1, //数量，必须是1

"marketing\_id": 1, //required。批发活动的ID, 即trial的id

}

\...其他需要提供的域同"新建订单api"

}

Return: 同"新建订单api"

126. **我的试用装申请列表**

GET <http://112.74.26.228:10080/rest/trial/application?pageNumber=1&pageSize=30>

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

public static enum Status {

APPLYING, //申请中

AUDITING, //审核中

DELIVERING, //发货中

DELIVERED, //已发货

REJECTED //未获得试用资格

}

Return:

{

"status\_code": 0,

"data": {

"totalRow": 1,

"pageNumber": 1,

"lastPage": true,

"firstPage": true,

"totalPage": 1,

"pageSize": 30,

"list": \[

{

"cover":
"http://o9ixtumvv.bkt.clouddn.com/20180709182906045-hyEDbt5L.jpeg",

"trial\_id": 1,

"created\_time": "2018-08-06 17:27:21",

"note": null,

"user\_id": 11080,

"order\_number": "18080617272155711080",

"shipping\_type": 0,

"name": "洗发水试用-免费",

"id": 1,

"order\_id": 3288,

"version": 1,

"status": "AUDITING"

}

\]

}

}

127. **其它配置**

128. **意见反馈**

POST <http://112.74.26.228:10080/rest/feedback>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"content": "建议门槛更低些，可以让更多人参与。", //必选

"images": \[ //可选

"http://image.url",

"http://image2.url"

\]

}

Return:

{

"message": "feedback.created",

"status\_code": 0

}

Error Return:

{

"message": "invalid.input.json",

"status\_code": 1

}

129. **常见问题类型**

GET <http://112.74.26.228:10080/rest/faq_type>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status\_code": 0,

"data": \[{

"id": 1,

"name": "FN"

}, {

"id": 2,

"name": "UI"

}\]

}

130. **常见问题**

GET <http://112.74.26.228:10080/rest/faq?typeId=1&pageNumber=1&pageSize=20>

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Query Parameter:

typeId - optional, 问题类型ID

pageNumber - optional, 页数

pageSize - optional, 每页记录数

Return:

{

"status\_code": 0,

"data": \[{

"created\_date": "2016-05-16 12:52:15",

"content": "分销拥金可提现时间是订单关闭后一天。",

"id": 1,

"last\_modified\_date": "2016-05-16 12:52:15",

"title": "分销拥金可提现时间",

"type\_id": 1

}\]

}

131. **关于商城**

GET <http://112.74.26.228:10080/rest/about_mall>

Return:

{

"status\_code": 0,

"data": {

"content": null,

"id": 1,

"image": "http://host:port/images/a.jpg"

}

}

132. **广告**

GET <http://112.74.26.228:10080/rest/ad>

返回所有广告组别的广告。

Return:

{

"status\_code": 0,

"data": \[{

"id": 1,

"name": "头位广告",

"ads": \[{

"id": 1,

"enabled": 1,

"name": "a",

"group\_id": 1,

"image": "/ad/7ce3c3f9662b92b759ecb8f523070631.jpg",

"type": "a",

"target\_url": "http://localhost:9990"

}\]

}, {

"id": 2,

"name": "首页banner",

"ads": \[\]

}\]

}

GET <http://112.74.26.228:10080/rest/ad/>\<group-name\>

返回该组别下的广告列表。

Return:

{

"status\_code": 0,

"data": \[{

"id": 1,

"enabled": 1,

"name": "a",

"group\_id": 1,

"image": "/ad/7ce3c3f9662b92b759ecb8f523070631.jpg",

"type": "a",

"target\_url": "http://localhost:9990"

}\]

}

133. **客服QQ**

GET <http://112.74.26.228:10080/rest/kf_qq>

返回QQ列表。

Return:

{

"status\_code": 0,

"data": \[

{

"number": "234234", //QQ号

"name": "AAA",

"id": 1,

"enabled": 1

},

{

"number": "2342",

"name": "BBB",

"id": 2,

"enabled": 1

}

\]

}

134. **Base64上传图片**

POST <http://112.74.26.228:10080/rest/upload_image>

通过POST base64 编码的图片来上传

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEASABIAAD/2\...\...\...

return:

{

"status\_code": 0,

"data":
"http://112.74.26.228:8000/upload/2016-06-30/20160630113427-00803.jpg"

}

135. **form上传图片**

POST <http://112.74.26.228:10080/rest/upload_image_x>

通过POST form 上传

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

return:

{

"status\_code": 0,

"data": \[

{

"file\_name": "e39936cbc10f49cef1316342a3938fec.png",

"original\_file\_name":
"20180427-231841-把祷告事项从应用内分享到微信群\~显示错误.png",

"url":
"https://www.kequandian.net/upload/2018-05-30/e39936cbc10f49cef1316342a3938fec.png"

},

{

"file\_name": "ba87f98c1028d55f5978fca64a6bce29.jpeg",

"original\_file\_name": "20161104133328890-xfTkpZAK.jpeg",

"url":
"https://www.kequandian.net/upload/2018-05-30/ba87f98c1028d55f5978fca64a6bce29.jpeg"

}

\]

}

136. **系统公告**

GET <http://112.74.26.228:10080/rest/system_announcement>

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

return:

{

"status\_code": 0,

"data": \[

{

"name": "fdsf",

"id": 33,

"created\_date": "2016-10-17 15:49:40",

"content": "safas afds afadsfas"

},

{

"name": "fdsfsd",

"id": 34,

"created\_date": "2016-10-17 15:51:08",

"content": "sfdsfds"

}

\]

}

137. **微信公众号访问域名**

GET <http://112.74.26.228:10080/rest/wx/host_prefix>

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

return:

{

"status\_code": 0,

"data": "https://www.muaskin.com/wx"

}

138. **收藏宝贝**

139. **返回收藏宝贝列表**

GET <http://112.74.26.228:10080/rest/product_favorite?pageNumber=1&pageSize=20>

Query Parameter:

pageNumber - optional, 页数

pageSize - optional, 每页记录数

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return：

{

"status\_code": 0,

"data": \[{

"id": 1,

"user\_id": 1,

"product\_id": 1,

"collect\_date": "2016-05-18 16:52:15",

"category\_id": 1,

"name": p1,

"cover": imag/xx.png,

"brand": ,

"origin":,

"stock\_balance":,

"sales":,

"description":,

"status":,

"created\_date":,

"last\_modified\_date":,

"unit":,

"price":,

"cost\_price":,

"suggested\_price":,

"promoted":,

"freight":,

"free\_shipping":,

"sort\_order":;

}\]

}

140. **添加收藏宝贝**

POST <http://112.74.26.228:10080/rest/product_favorite>

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

{

"product\_id": 1

}

Return：

{

"status\_code": 0,

"message": "product.favorite.created",

}

Error Return:

{

"message": "invalid.input.json",

"status\_code": 1

}

141. **删除收藏宝贝**

DELETE <http://112.74.26.228:10080/rest/product_favorite/id>

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Parameter:

id -商品id

Return：

{

"message": "product.favorite.deleted",

"status\_code": 0

}

Error Return:

{

"message": "no.such.product.favorite",

"status\_code": 1

}

142. **打单系统API**

143. **快递公司列表**

GET <http://112.74.26.228:10080/rest/admin/express>

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return：

{

"status\_code": 0,

"data": \[{

"id": 3,

"enabled": 1,

"name": "百世快递",

"is\_default": 1,

"code": "baishiwuliu"

}, {

"id": 1,

"enabled": 1,

"name": "天天快递",

"is\_default": 0,

"code": "tiantian"

}, {

"id": 2,

"enabled": 1,

"name": "万象物流",

"is\_default": 0,

"code": "wanxiangwuliu"

}\]

}

144. **订单列表**

GET <http://112.74.26.228:10080/rest/admin/order?status=CONFIRMED_DELIVER_PENDING&status=DELIVERING&started_date=1313432434&end_date=1334453432424&order_number=32432432432&order_number=23432432432>

Query Parameter:

status - optional,
订单状态，可以同时提供多个值，各个值间是"或"的关系。如果为空，则查询CONFIRMED\_DELIVER\_PENDING状态的订单。

started\_date - optional，整数类型， 开始时间

end\_date - optional, 整数类型， 结束时间

order\_number - optional，
订单号，可以同时提供多个值，各个值间是"或"的关系。

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return：

{

"status\_code": 0,

"data": \[{

"detail": "和平区 89652号",

"phone": "13652698536",

"is\_deliver\_reminder": 1,

"contact\_user": "huang",

"remark": null,

"invoice": 0,

"street": null,

"trade\_number": "TEST1467273404816",

"express\_number": null,

"deal\_date": null,

"express\_company": null,

"city": "天津",

"id": 299,

"cover":
"http://112.74.26.228:8000/p/c45bb9fda6d985a3be40b40bdb693bb0.jpg",

"confirm\_date": null,

"description": "超效洁净护理洗衣液2.5L【运费10元】 x 1. ",

"province": "天津",

"user\_id": 2,

"express\_code": null,

"district": "和平区",

"deliver\_date": null,

"delivered\_date": null,

"created\_date": "2016-06-30 15:55:40",

"order\_number": "2016063015554024000000201",

"zip": null,

"status": "CONFIRMED\_DELIVER\_PENDING",

"invoice\_title": null,

"receiving\_time": null,

"deliver\_order\_number": null,

"total\_price": 44.80,

"previous\_status": null,

"settled": 0,

"freight": 10.00,

"pay\_date": "2016-06-30 15:56:44",

"payment\_type": "WECHAT",

"order\_items": \[{

"quantity": 12,

"product\_specification\_id": null,

"weight": 22,

"product\_specification\_name": null,

"product\_name": "a",

"cover": "/p/b06260c587244e867209a5ba374a16ed.jpeg",

"final\_price": 132.00,

"price": 11.00,

"product\_id": 1,

"id": 3,

"bulk": null,

"order\_id": 2,

"partner\_level\_zone": 1,

"barcode": null,

"store\_location": null,

"status": "CREATED",

"cost\_price": 1.00

}, {

"quantity": 21,

"product\_specification\_id": 1,

"weight": 32,

"product\_specification\_name": "sfsf",

"product\_name": "b",

"cover": "/p/39df6836637605a5c86e8aec6ac8a43d.jpeg",

"final\_price": 693.00,

"price": 33.00,

"product\_id": 2,

"id": 4,

"bulk": null,

"order\_id": 2,

"partner\_level\_zone": 1,

"barcode": null,

"store\_location": null,

"status": "CREATED",

"cost\_price": 22.00

}\]

}, {

"detail": "同德乡田心西路富新大厦202",

"phone": "13430377263",

"is\_deliver\_reminder": 1,

"contact\_user": "邓棋云",

"remark": null,

"invoice": 0,

"street": null,

"trade\_number": "TEST1469777476820",

"express\_number": null,

"deal\_date": null,

"express\_company": null,

"city": "广州",

"id": 478,

"cover": "http://images.10mup.com/20160722155600409-t2lJM6oT.jpg",

"confirm\_date": null,

"description":
"亮白增艳护理洗衣液2.5L【全国包邮（甘肃、宁夏、新疆、西藏、青海、内蒙古除外）】法国香薰
x 1. ",

"province": "广东",

"user\_id": 210,

"express\_code": null,

"district": "白云区",

"deliver\_date": null,

"created\_date": "2016-07-29 15:30:30",

"order\_number": "160729153030841210",

"zip": null,

"status": "CONFIRMED\_DELIVER\_PENDING",

"invoice\_title": null,

"receiving\_time": null,

"deliver\_order\_number": null,

"total\_price": 38.80,

"previous\_status": null,

"settled": 0,

"freight": 0.00,

"pay\_date": "2016-07-29 15:31:16",

"payment\_type": "WECHAT",

"order\_items": \[\]

}, {

"detail": "西槎路田心西路",

"phone": "13822222291",

"is\_deliver\_reminder": 1,

"contact\_user": "肖生",

"remark": null,

"invoice": 0,

"street": null,

"trade\_number": "TEST1471255826887",

"express\_number": null,

"deal\_date": null,

"express\_company": null,

"city": "广州",

"id": 497,

"cover": "http://images.10mup.com/20160723174322764-pmKT58D2.jpg",

"confirm\_date": null,

"description": "纳爱斯柠檬绿茶牙膏天然柠檬绿茶口腔清洁160gX3支 x 1.
",

"province": "广东",

"user\_id": 205,

"express\_code": null,

"district": "白云区",

"deliver\_date": null,

"created\_date": "2016-08-15 18:09:13",

"order\_number": "160815180913014205",

"zip": null,

"status": "CONFIRMED\_DELIVER\_PENDING",

"invoice\_title": null,

"receiving\_time": null,

"deliver\_order\_number": null,

"total\_price": 19.83,

"previous\_status": null,

"settled": 0,

"freight": 0.00,

"pay\_date": "2016-08-15 18:10:26",

"payment\_type": "WECHAT",

"order\_items": \[\]

}, {

"detail": "西槎路田心西路",

"phone": "13822222291",

"is\_deliver\_reminder": 1,

"contact\_user": "肖生",

"remark": null,

"invoice": 0,

"street": null,

"trade\_number": "TEST1471363956667",

"express\_number": null,

"deal\_date": null,

"express\_company": null,

"city": "广州",

"id": 504,

"cover": "http://images.10mup.com/20160722155600409-t2lJM6oT.jpg",

"confirm\_date": null,

"description":
"亮白增艳护理洗衣液2.5L【全国包邮（甘肃、宁夏、新疆、西藏、青海、内蒙古除外）】薰衣草
x 1. ",

"province": "广东",

"user\_id": 205,

"express\_code": null,

"district": "白云区",

"deliver\_date": null,

"created\_date": "2016-08-17 00:11:38",

"order\_number": "160817001138232205",

"zip": null,

"status": "CONFIRMED\_DELIVER\_PENDING",

"invoice\_title": null,

"receiving\_time": null,

"deliver\_order\_number": null,

"total\_price": 38.80,

"previous\_status": null,

"settled": 0,

"freight": 0.00,

"pay\_date": "2016-08-17 00:12:36",

"payment\_type": "WECHAT",

"order\_items": \[\]

}\]

}

145. **批量更新订单发货信息**

POST <http://112.74.26.228:10080/rest/admin/deliver>

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

\[{

"order\_number": "23432432432",

"express\_id": 2,

"express\_number": "23423432432"

}\]

Return:

{

"message": "order.delivered",

"status\_code": 0

}

146. **批量完成订单发货**

POST <http://112.74.26.228:10080/rest/admin/delivered>

Header:

Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Data:

\[{

"order\_number": "23432432432"

}\]

Return:

{

"message": "order.delivered",

"status\_code": 0

}

147. **支付宝支付**

148. **支付宝支付**

POST [http://host:port/rest/ali/push\_order](http://host:port/rest/ali/push_order)

Data:

{

"order\_number": "1234", //账单号

"order\_type": "Order", //账单类型，订单：Order, 钱包充值： Wallet,
预约： Appointment

"type": "QRCODE" // QRCODE： PAD端生成支付宝二维码， APP：
移动应用调起支付宝支付

}

PAD端拿到 qrCode 字段生成二维码给用户使用支付宝扫码进行支付。

APP端拿到 orderString后 发给支付宝唤起支付宝支付。

Response:

{

"status\_code": 0,

"data": {

"qr\_code": "https://qr.alipay.com/bax01098eimzy9vigelm00c7" //
type是QRCODE时返回

"order\_string":
"alipay\_sdk=alipay-sdk-java-3.4.27.ALL&app\_id=2016092200567241&biz\_content=%7B%22body%22%3A%22DEMO%22%2C%22out\_trade\_no%22%3A%221234%22%2C%22subject%22%3A%22DEMO%22%2C%22timeout\_express%22%3A%2230m%22%2C%22total\_amount%22%3A%2211.1%22%7D&charset=utf-8&format=json&method=alipay.trade.app.pay&notify\_url=%2Frest%2Fpub%2Fali%2Fpay\_notify&sign=JP1AxixqyWqz8n4CRNAvkhysh8dCH86fV6oMkftLzRdyZqWIQIHW%2FHWhnwHgw4Xfj4lkwoJFPVCi1pYw0Ef0zFE5PVFBRaABLFQcX3sRB4pO6UDrXvo%2BR8vqFTrnuYwXCS91VxKlU4Fj%2FMa94ZJ4eUtm62qvyqS9wbyGTEaVy9vddjSiEgPS8fAch9V3qNobNYFGC7Mfhi8BjHX1zgONQusR75DnqH4DOywdmarzZFHrtlVBeQg1gI89dyeiLZOthiZ0jsBHxmS4jNxkiw%2BRF7Sr8HDyKV9Ubd0po6rdLsInHtVivom6hVKjzvM1kJkltXIpUZ39jiTTD6iaUy%2B9Bw%3D%3D&sign\_type=RSA2&timestamp=2018-11-05+18%3A25%3A16&version=1.0"
//type是 APP 时返回

}

}
