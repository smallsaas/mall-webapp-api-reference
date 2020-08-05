## 物流API

### 查看订单物流信息

GET https://mall.smallsaas.cn/rest/express_info?order_number=0000000101455770560193531 

Param:

 - orderNumber: ORDER-NUMBER

Header: Authorization: token

> state:
> 快递单当前的状态 ：　
> 0：在途，即货物处于运输过程中；
> 1：揽件，货物已由快递公司揽收并且产生了第一条跟踪信息；
> 2：疑难，货物寄送过程出了问题；
> 3：签收，收件人已签收；
> 4：退签，即货物由于用户拒签、超区等原因退回，而且发件人已经签收；
> 5：派件，即快递正在进行同城派件；
> 6：退回，货物正处于退回发件人的途中；

Return:
```
{
	"com": "baishiwuliu",
	"data": [{
		"context": "镇江市|签收|镇江市【新句容】，百世邻里下蜀代理点已签收",
		"time": "2016-06-19 18:12:40"
	}, {
		"context": "镇江市|派件|镇江市【新句容】，【下蜀陈龙/18112812262】正在派件",
		"time": "2016-06-19 11:26:05"
	}, {
		"context": "镇江市|到件|到镇江市【新句容】",
		"time": "2016-06-19 07:20:20"
	}, {
		"context": "南京市|发件|南京市【南京转运中心】，正发往【新句容】",
		"time": "2016-06-19 02:24:17"
	}, {
		"context": "南京市|到件|到南京市【南京转运中心】",
		"time": "2016-06-19 01:31:20"
	}, {
		"context": "广州市|到件|到广州市【广州转运中心】",
		"time": "2016-06-18 02:24:44"
	}, {
		"context": "广州市|发件|广州市【广州白云石槎分部】，正发往【广州转运中心】",
		"time": "2016-06-18 01:12:42"
	}, {
		"context": "广州市|收件|广州市【广州白云石槎分部】，【田001/02036450972】已揽收",
		"time": "2016-06-17 18:45:46"
	}, {
		"context": "广州市|发件|广州市【广州转运中心】，正发往【南京转运中心】",
		"time": "2016-06-10 04:13:25"
	}],
	"comcontact": "400-8856-561",
	"succeed": true,
	"nu": "70534708088780",
	"company": "baishiwuliu",
	"state": "3",
	"message": "ok",
	"status": "1"
}
```

Failure Return:
```
{
	"message": "cannot.find.express.info",
	"status_code": 1
}
```

### 购物车列表

GET https://mall.smallsaas.cn/rest/shopping_cart 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "created_date": "2016-04-25 19:15:45",
        "id": 3,
        "cover":"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
        "price": null,
        //price正常情况是有的，如果为null，则表示出错了，对应两种出错原因：1.由于用户未配置默认配
        //送区域而不能计算价格；2.用户配置了默认配送区域，但对应的批发活动的区域价格定义中没有匹配的，也不能计算价格
        "msg": "尚未配置默认配送区域，将不能计算价格", //如果price为
        //null，则会提供该msg域，提示错误信息，有两种错误信息，分别对应上述两种出错原因
        "marketing": "WHOLESALE", //营销活动 （WHOLESALE代表批发活动）
        "marketing_id": "1", //批发活动id
        "product_id": 1,
        "fare_id": 1, //运费模版ID
        "product_name": "超效洁净护理洗衣液2.5L【全国包邮】",
        "quantity": 1,
        "user_id": 4,
        "product_specification_name": "a1",//规格名称
        "product_specification_id": 2 //规格ID，提交订单时用
    },{
        "created_date": "2016-04-25 19:15:45",
        "id": 3,
        "cover": "https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
        "price": 34.80,
        "product_id": 1,
        "fare_id": 1, //运费模版ID
        "product_name": "超效洁净护理洗衣液2.5L【全国包邮】",
        "quantity": 1,
        "user_id": 4,
        "product_specification_name": "a1",//规格名称
        "product_specification_id": 2 //规格ID，提交订单时用
    }, {
        "created_date": "2016-04-25 19:15:45",
        "id": 4,
        "cover":"https://mall.smallsaas.cn/p/2b3edeb3c3ca2a12b06893cb12286710.png",
        "price": 69.60,
        "product_id": 3,
        "fare_id": 1,
        "product_name": "超效洁净护理洗衣液2.5Lx2瓶【全国包邮】",
        "quantity": 1,
        "user_id": 4
    }]
}
```

52. **添加到购物车**

POST https://mall.smallsaas.cn/rest/shopping_cart?increase=false 

如果已存在，则更新，如果quantity是0，则删除。

parameter:

increase: optional, default true.
如果为true则累加购物车数量，为false则替换数量。

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

[{

"product_id": 1,

"quantity": 1,

"product_specification_id": 1, //optional, 选择的产品规格ID

"marketing_id": 1, //optional 营销活动id

"marketing": "WHOLESALE" //optional 营销活动(一般是批发
WHOLESALE,团购是直接下单的）

}, { //非批发产品不需要提供 marketing_id 和 marketing 字段

"product_id": 3,

"quantity": 1

}]

Return 购物车列表:

{

"status_code": 0,

"data": [{

"created_date": "2016-04-25 19:15:45",

"id": 3,

"cover":
"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",

"price": 34.80,

"weight": 1000, // 重量

"bulk": 1000, //体积

"product_id": 1,

"free_shipping": 1,

"product_name": "超效洁净护理洗衣液2.5L【全国包邮】",

"freight": 0.00,

"quantity": 1,

"product_specification_name": "a1",//规格名称

"user_id": 4,

"marketing_id": 1,

"marketing": "WHOLESALE"

}, {

"created_date": "2016-04-25 19:15:45",

"id": 4,

"cover":
"https://mall.smallsaas.cn/p/2b3edeb3c3ca2a12b06893cb12286710.png",

"price": 69.60,

"weight": 1000, // 重量

"bulk": 1000, //体积

"product_id": 3,

"free_shipping": 1,

"product_name": "超效洁净护理洗衣液2.5Lx2瓶【全国包邮】",

"freight": 0.00,

"quantity": 1,

"user_id": 4,

"marketing_id": null

"marketing": null

}]

}

53. **删除购物车**

清空购物车

DELETE https://mall.smallsaas.cn/rest/shopping_cart 

Header: Authorization:
eyJ0b2tlbiI6IjczYmI2MWFjNmRlN2E0NDVlOGI4MzNmZjlkYWJlYjI4NTBhMzg0NmMiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status_code": 0,

"data": "shopping_cart.delete.success"

}

54. **我的地址列表**

GET https://mall.smallsaas.cn/rest/contact 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status_code": 0,

"data": [{

"id": 3,

"zip": "510000",

"detail": "6F",

"phone": "1380000000",

"contact_user": "Mr Huang",

"street": "jianzhong road",

"province": "GD",

"is_default": 1,

"street_number": "50",

"user_id": 4,

"district": "Tiahne",

"city": "GZ"

}]

}

55. **添加新地址**

POST https://mall.smallsaas.cn/rest/contact 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

"contact_user": "Mr Huang",

"phone": "1380000000",

"zip": "510000",

"province": "GD",

"city": "GZ",

"district": "Tiahne",

"street": "jianzhong road",

"street_number": "50",

"detail": "6F",

"is_default": 1

}

Return:

{

"status_code": 0,

"data": "contact.saved"

}

56. **更新地址**

PUT https://mall.smallsaas.cn/rest/contact/id 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

"contact_user": "Mr Huang",

"phone": "1380000000",

"zip": "510000",

"province": "GD",

"city": "GZ",

"district": "Tiahne",

"street": "jianzhong road",

"street_number": "50",

"detail": "6F",

"is_default": 0

}

Return:

{

"status_code": 0,

"data": {

"id": 1,

"contact_user": "Mr Huang",

"phone": "1380000000",

"zip": "510000",

"province": "GD",

"city": "GZ",

"district": "Tiahne",

"street": "jianzhong road",

"street_number": "50",

"detail": "6F"

"is_default": 0,

"user_id": 1

}

}

57. **删除地址**

DELETE https://mall.smallsaas.cn/rest/contact/id 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status_code": 0,

"data": "contact.deleted"

}

58. **得到默认地址**

GET https://mall.smallsaas.cn/rest/default_contact 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status_code": 0,

"data": {

"id": 73,

"zip": "510000",

"detail": "5F",

"phone": "1380000000",

"contact_user": "Mr Huang",

"street": "jianzhong roadxxxxx",

"province": "广东省",

"is_default": 1,

"street_number": "50",

"user_id": 4,

"district": "天河区",

"city": "广州市"

}

}

59. **更新默认地址**

PUT https://mall.smallsaas.cn/rest/default_contact/id 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"message": "contact.updated",

"status_code": 0

}

60. **默认快递**

GET https://mall.smallsaas.cn/rest/default_express 

Return:

{

"status_code": 0,

"data": {

"code": "ff",

"name": "天天快递",

"id": 2,

"is_default": 1,

"enabled": 1

}

}

61. **运费计算**

POST https://mall.smallsaas.cn/rest/product_carriage 

Data:

{

"delivery_type": "EXPRESS", //可选项：EXPRESS, SELF_PICK, FLASH,
默认EXPRESS

"province": "广东",

"city": "广州",

"data":[

{

"fare_id": 1,

"price": 23.20,

"quantity": 4,

"weight": 500, //该产品的重量，从product可以拿到，单位是g

"bulk": 100 //该产品的体积， 可以忽略

}

]

}

Return:

{

"status_code": 0,

"data": {

"carriage": 4.00, //运费

"message": "付同样的运费,还可以拼单0.30KG哦.",

"delta": -180.00
//可忽略。距离满包邮的差额。注意：这是一个负数。只有是负数时才表示离满包邮有差额。

}

}

62. **查询产品限购**

GET https://mall.smallsaas.cn/rest/product_purchase_strategy?productId=234&quantity=2 

parameter:

productId: 产品ID

quantity: 购买数量

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

可以购买，

Return:

{

"status_code": 0,

"message": "ok"

}

限购了， 不能购买，

Return:

{

"status_code": 1,

"message": "超出购买限额, 限购2件, 你过去10天内已购买过1件. "

}

63. **拥金API**

64. **查看提现账号信息**

GET https://mall.smallsaas.cn/rest/withdraw_account 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Return:

{

"status_code": 0,

"data": [{

"id": 1,

"bank_name": null,

"owner_name": "Mr.A",

"account": "234234234324",

"user_id": 1,

"type": "ALIPAY"

}]

}

65. **添加提现账号信息**

POST https://mall.smallsaas.cn/rest/withdraw_account 

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

"owner_name": "Mr.A",

"type": "ALIPAY",

"account": "234234234324",

"bank_name":"中国工商银行科韵路支行" //当type为BANK时需要

}

Return:

{

"message": "withdraw.account.created",

"status_code": 0

}

66. **删除提现账号信息**

DELETE https://mall.smallsaas.cn/rest/withdraw_account/id 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Parameter:

id: 账户ID

Return:

{

"message": "withdraw.account.deleted",

"status_code": 0

}

67. **查看余额**

GET https://mall.smallsaas.cn/rest/owner_balance 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Success Return:

{

"status_code": 0,

"data": {

"total_reward": 8, //总提成

"balance": 2, //可用余额

"is_agent": true, //是否是代理商

"is_seller": true, //是否是销售商

"is_partner": true, //是否是经销商

"is_crown": true, //是否皇冠

"is_crown_ship_temp": true,
//是否为临时皇冠，临时皇冠不能进入线下门店

"is_physical": true, //是否线下资格

"is_copartner": true, //是否合伙人

"partner_pool_count": 9, //合伙人池人数

"partner_level": { //如果不是经销商，那么就为null

"id": 1,

"level": 1, //表示该经销商的级别，1表示一星

"headcount_quota": 3,

"name": "一星经销商"

},

"next_partner_level": { //如果没有下一级，那么就为null

"id": 2,

"level": 2, //下一级别

"headcount_quota": 3, //下一星的人数

"name": "二星经销商"

},

}，

"msg":
"您现在是临时线下皇冠商，成为永久线下皇冠商需要在4小时内完成2000元的批发任务"
//如果是临时线下皇冠商，则会出现

//此提示

}

68. **申请提现**

POST https://mall.smallsaas.cn/rest/owner_balance 

Header: Authorization:
eyJ0b2tlbiI6IjQzN2NhZjRiYjQxOWZhZGEwZDgwYmFmMTEzYjY0OGNlMzdiM2NmYWQiLCJsb2dpbl9uYW1lIjoiYWRtaW4ifQ==

Data:

{

"withdraw_type": "Wallet", // optional, wallet为提现到零钱帐户

"withdraw_account_id": 1, // optional, 账户ID

"withdraw_cash": 100.00 //提现金額

}

Success Return:

{

"message": "apply.success",

"status_code": 1

}

Failure Return:

{

"message": "apply.failure",

"status_code": 1

}

69. **查看提现历史记录**

GET https://mall.smallsaas.cn/rest/reward_cash 

Parameters:

page_number: optional, 页码，default 1;

page_size: optional, 每页记录数，default 30;

start_date: optional, 开始时间， default 上个月;

end_date: optional, 结束时间， default 今天。

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

"status_code": 0,

"data": [

{

"id": 2,

"apply_time": "2016-06-16 13:23:39",

"bank_name": null,

"account_number": "oXauMwcMqGeV6zdHGL_1CcmjlQUg",

"status": "APPLYING",

"name": "Jacky.D.H",

"cash": 100,

"owner_id": 62,

"complete_time": null,

"reject_time": null,

"account_name": "Jacky.D.H",

"account_type": "WECHAT"

}

]

}

70. **查看分成订单汇总信息**

GET https://mall.smallsaas.cn/rest/order_item_reward 

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

查询参数:

page_number: optional, 页数

page_size: optional, 每页记录数

start_date: optional, 开始时间

end_date: optional, 结束时间

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

PENDING_SETTLEMENT, //待结算

SETTLED, //已结算， 只有已结算的拥金才会有余额里体现

REFUNDED //已退款， 表示该订单已发生退货退款，本分成无效。

}

resp:

{

"status_code": 0,

"data": {

"order_item_rewards": [

{

"reward": 2,

"created_time": "2016-06-05 11:11:22",

"level": 1, //结合type一起使用，表示参与分成时的级别，比如type=SELLER,
level=1, 表示作为一级分销商参与分成

"owner_id": 1,

"order_number": "1234567890", //订单号

"order_profit": 20, //整个订单项的利润,页面不应显示出来

"settled_time": null,

"type": "AGENT", //分成的角色，AGENT：作为代理商分成

"percent": 10, //分成比例，前端ignore，页面不应显示出来

"withdrawn_time": null,

"product_name": "A", //产品名称

"product_price": 20.00, //产品价格

"product_quantity": 1, //产品数量

"order_item_id": 1,

"cover": "/assets/img/find_user.png", //产品图片

"name": "Administrator",

"id": 4,

"state": "SETTLED", //分成状态

"order_id": 1,

"payment_type": "WECHAT",

"point_exchange_rate": 100

},

{

"reward": 2,

"created_time": "2016-06-05 11:11:22",

"level": 3,

"owner_id": 1,

"order_number": "1234567890",

"order_profit": 20,

"settled_time": null,

"type": "PARTNER",

"percent": null,

"withdrawn_time": null,

"product_name": "A",

"order_item_id": 1,

"cover": "/assets/img/find_user.png",

"name": "Administrator",

"id": 3,

"state": "PENDING_SETTLEMENT",

"order_id": 1,

"payment_type": "WECHAT",

"point_exchange_rate": 100

},

{

"reward": 2,

"created_time": "2016-06-05 11:11:22",

"level": 1,

"owner_id": 1,

"order_number": "1234567890",

"order_profit": 20,

"settled_time": null,

"type": "SELLER",

"percent": 10,

"withdrawn_time": null,

"product_name": "A",

"order_item_id": 1,

"cover": "/assets/img/find_user.png",

"name": "Administrator",

"id": 2,

"state": "PENDING_SETTLEMENT",

"order_id": 1,

"payment_type": "WECHAT",

"point_exchange_rate": 100

},

{

"reward": 2,

"created_time": "2016-06-05 11:11:22",

"level": null,

"owner_id": 1,

"order_number": "1234567890",

"order_profit": 20,

"settled_time": null,

"type": "SELF",

"percent": 10,

"withdrawn_time": null,

"product_name": "A",

"order_item_id": 1,

"cover": "/assets/img/find_user.png",

"name": "Administrator",

"id": 1,

"state": "PENDING_SETTLEMENT",

"order_id": 1,

"payment_type": "WECHAT",

"point_exchange_rate": 100

}

],

"pending_reward": 6,

"settled_reward": 2,

"total_order_count": 2,

"settled_order_count": 1,

"pending_order_count": 1

}

}

71. **查看产品分成**

GET https://mall.smallsaas.cn/rest/product_settlement?id=product-id&marketingType=type&marketingId=id

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

查询参数:

-   id: integer,required, 产品ID

-   marketingType: string, optional, 营销活动类型，如拼团为PIECE-GROUP

-   marketingId: integer, optinal, 营销活动ID

Return:

{

"status_code": 0,

"data": 30.00

}

72. **分销API**

73. **我的分销商层次信息**

GET https://mall.smallsaas.cn/rest/seller_level 

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status_code": 0,

"data": {

"result": true,

"levels": [2, 1, 0], //各级的分销商总数

"max_level": 3 //三级分销

}

}

74. **我的分销商信息**

GET https://mall.smallsaas.cn/rest/seller 

返回下一级的朋友

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status_code": 0,

"data": {

"id": 1,

"user_name": "Administrator",

"partner_id": null, //合伙人ID

"level": 1,

"partner_ship": 1, //是否是合伙人

"partner_pool_count": 9, //合伙人池人数

"seller_ship_time": "2016-04-28 13:08:35", //成为分销商时间

"partner_ship_time": "2016-04-28 13:08:35", //成为合伙人时间

"user_id": 1,

"seller_ship": 1, //是否是分销商

"parent_id": null,

"followed": 1, //是否关注公众号

"follow_time": "2016-05-06 12:00:00", //关注时间

"unfollowed_children_count": 0, //未关注的下级总数

"followed_children_count": 0, //已关注的下级总数

"agent_ship": 1, //是否是代理商

"partner_level": { //如果不是经销商，那么就为null

"id": 1,

"level": 1, //表示该经销商的级别，1表示一星

"headcount_quota": 3,

"name": "一星经销商"

},

"next_partner_level": { //如果没有下一级，那么就为null

"id": 2,

"level": 2, //下一级别

"headcount_quota": 3, //下一星的人数

"name": "二星经销商"

},

"children": [{

"seller_ship_time": null,

"level": 2, //没用，忽略

"partner_ship_time": null,

"user_name": "abc", //用户名

"avatar": null, //头像URL

"sa_level": 1,
//属于该分销商的第几级分销商.只有type=all时才有这个属性。

"partner_id": null,

"user_id": 3,

"partner_ship": 0,

"parent_id": 1,

"id": 3,

"seller_id": 3,

"seller_ship": 0,

"followed": 1, //是否关注公众号

"follow_time": "2016-05-06 12:00:00", //关注时间

"agent_ship": 1, //是否是代理商

"register_date": "2018-10-11", //注册时间

"grade": "1" // VIP系统的会员级别ID

}, {

"seller_ship_time": null,

"level": 2,

"partner_ship_time": null,

"user_name": "xyz",

"avatar": null,

"sa_level": 1,

"partner_id": null,

"user_id": 9,

"partner_ship": 0,

"parent_id": 1,

"id": 9,

"seller_id": 9,

"seller_ship": 0,

"followed": 1, //是否关注公众号

"follow_time": "2016-05-06 12:00:00", //关注时间

"agent_ship": 0 //是否是代理商

}, {

"seller_ship_time": null,

"level": 3,

"partner_ship_time": null,

"user_name": "a",

"avatar": null,

"sa_level": 2,

"partner_id": null,

"user_id": 4,

"partner_ship": 0,

"parent_id": 3,

"id": 4,

"seller_id": 4,

"seller_ship": 0,

"followed": 1, //是否关注公众号

"follow_time": "2016-05-06 12:00:00", //关注时间

"agent_ship": 0 //是否是代理商

}, {

"seller_ship_time": null,

"level": 3,

"partner_ship_time": null,

"user_name": "b",

"avatar": null,

"sa_level": 2,

"partner_id": null,

"user_id": 5,

"partner_ship": 0,

"parent_id": 3,

"id": 5,

"seller_id": 5,

"seller_ship": 0,

"followed": 1, //是否关注公众号

"follow_time": "2016-05-06 12:00:00", //关注时间

"agent_ship": 1 //是否是代理商

}]

}

}

75. **下级分销商信息**

GET https://mall.smallsaas.cn/rest/seller/seller_id 

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Parameter: seller_id: 下级分销商ID

Return:

{

"status_code": 0,

"data": {

"id": 2,

"user_name": "a",

"partner_id": 1,

"level": 2,

"partner_ship": 0,

"seller_ship_time": null,

"partner_ship_time": null,

"followed": 1, //是否关注公众号

"follow_time": "2016-05-06 12:00:00", //关注时间

"children": [{

"id": 4,

"user_name": "a1",

"partner_id": 1,

"level": 3,

"partner_ship": 0,

"seller_ship_time": null,

"partner_ship_time": null,

"user_id": 4,

"seller_ship": 0,

"parent_id": 2,

"followed": 1, //是否关注公众号

"follow_time": "2016-05-06 12:00:00" //关注时间

}, {

"id": 5,

"user_name": "a2",

"partner_id": 1,

"level": 3,

"partner_ship": 0,

"seller_ship_time": null,

"partner_ship_time": null,

"user_id": 5,

"seller_ship": 0,

"parent_id": 2,

"followed": 1, //是否关注公众号

"follow_time": "2016-05-06 12:00:00"//关注时间

}],

"user_id": 2,

"seller_ship": 0,

"parent_id": 1

}

}

76. **申请成为分销商**

POST https://mall.smallsaas.cn/rest/seller 

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

申请成为皇冠商时的前提：申请成为皇冠商开关已打开

Data:

{

"real_name": "Huang",

"phone": "1308888899",

"type": "CROWN" //申请类型，默认不填则为申请 分销商 资格。
CROWN为申请线下皇冠商资格。

}

Return:

{

"status_code": 0,

"data": {

"seller_ship": 1

}

}

77. **以扫码方式申请成为某皇冠商的"线下经销商"或"线下皇冠商"**

POST https://mall.smallsaas.cn/rest/physical_seller 

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

"real_name": "黄", //required,申请人真实姓名，用于更新个人信息

"phone": "13800000000", //required,申请人手机，用于更新个人信息

"type": "CROWN",
//optional，省略表示申请成为线下经销商，CROWN表示申请成为线下皇冠商

"province": "广东", //required

"city": "广州", //required

"district": "荔湾区" //required

}

Success Resp:

{

"status_code": 0,

"message": "apply.success"

}

Error Return:

{

"status_code": 1,

"message": "user.is.not.crownship"

}

{

"status_code": 1,

"message": "invalid.user"

}

{

"status_code": 1,

"message": "invalid.phone"

}

{

"status_code": 1,

"message": "cannot.apply.yourself"

}

78. **线下经销商查看线下信息**

GET https://mall.smallsaas.cn/rest/physical_seller 

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status_code": 0,

"data": {

"parent_seller_id": null,

"parent": null,

"city": null,

"children_count": 2, //physical_seller_children_count,
physical_seller_children 只有具

//有皇冠商资格时才返回。

"user_name": "Administrator",

"total_settled_amount": 0,

"avatar": null,

"uid": "U00000001",

"province": null,

"total_amount": 0,

"children": [], //星级经销商下线列表

"crown_children": [ //皇冠商下线列表（包含下级和下下级皇冠商）

{

"parent_seller_id": 1,

"city": null,

"level": 1, //1.下级皇冠商 2.下下级皇冠商

"user_name": "user123",

"total_settled_amount": 0,

"crown_ship": 1,

"real_name": "user123",

"avatar": null,

"followed": 1,

"uid": "U011707251055190003",

"follow_time": null,

"province": null,

"total_amount": 0,

"phone": null,

"district": null,

"latest_bonus_date": null,

"id": 182,

"created_date": "2017-09-19 10:59:06",

"seller_id": 11014

},

{

"parent_seller_id": 11014,

"city": null,

"level": 2,

"user_name": "关应康",

"total_settled_amount": 0,

"crown_ship": 1,

"real_name": null,

"avatar":
"http://wx.qlogo.cn/mmopen/vi_32/AWrNt30IeSoibiaaicZafBbkw39icOzMibCfDSMhQH9uRYxRLQMzUp4hJBHtvYMZn9FwXMkpibM47C0OW94nJU0lyOjw/0",

"followed": 1,

"uid": "U011707271136230002",

"follow_time": null,

"province": null,

"total_amount": 0,

"phone": null,

"district": null,

"latest_bonus_date": null,

"id": 181,

"created_date": "2017-09-19 10:58:36",

"seller_id": 11019

}

],

"district": null,

"crown_children_count": 1,
//只有具有皇冠商资格时才返回。下级皇冠商数量

"crown_children_count_lv2": 1, // 只有具有皇冠商资格时才返回。
下下级皇冠商数量

"latest_bonus_date": null,

"id": 179,

"created_date": "2017-08-09 12:03:07",

"seller_id": 1

}

}

79. **线下皇冠商查看进货结算明细**

GET https://mall.smallsaas.cn/rest/physical_purchase_summary?month=2017-06 

Parameter:

month: optional,
要查询的月份，格式yyyy-MM,如果不传该参数，则返回所有月份的记录，用于'结算记录'UI。如果传了参数，则返回该月的明细，用于'我的推荐'UI。

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Return:

{

"status_code": 0,

"data": [

{

"transferred": 0, //是否已转积分系统

"statistic_month": "2017-09-01", //统计月份

"monthly_amount": 5600, //本月进货

"total_settled_amount": 848, //累计总提成. 当有month参数时才返回该项

"monthly_settled_amount": 848, //提成金额

"monthly_expected_settled_amount": 0, //上级期望提成（前端用不到）

"monthly_expected_settled_amount_lv2": 0,
//上上级期望提成（前端用不到）

"my_recommended_sellers": [ //我的推荐线下经销商.
当有month参数时才返回该项（包含两级，下级排前面，下下级排

//后面）

{

"transferred": 0,

"level": 1, //1.下级 2.下下级

"user_name": "user123",

"statistic_month": "2017-09-01",

"monthly_amount": 3200,

"avatar": null,

"monthly_settled_amount": 960,

"monthly_expected_settled_amount_lv2": 0,

"uid": "U011707251055190003",

"transferred_amount": 0,

"monthly_expected_settled_amount": 728,

"settlement_proportion": 100,

"id": 192,

"seller_id": 11014

},

{

"transferred": 0,

"level": 2,

"user_name": "关应康",

"statistic_month": "2017-09-01",

"monthly_amount": 6000,

"avatar":
"http://wx.qlogo.cn/mmopen/vi_32/AWrNt30IeSoibiaaicZafBbkw39icOzMibCfDSMhQH9uRYxRLQMzUp4hJBHtvYMZn9FwXMkpibM47C0OW94nJU0lyOjw/0",

"monthly_settled_amount": 0,

"monthly_expected_settled_amount_lv2": 120,

"uid": "U011707271136230002",

"transferred_amount": 0,

"monthly_expected_settled_amount": 960,

"settlement_proportion": 100,

"id": 191,

"seller_id": 11019

}

],

"transferred_amount": 0,

"total_amount": 5600,

"settlement_proportion": 100,

"id": 193,

"seller_id": 1

}

]

}

80. **线下代理商查看进货结算明细**

GET https://mall.smallsaas.cn/rest/agent_summary?month=2017-08 

Parameter:

month: optional,
要查询的月份，格式yyyy-MM,如果不传该参数，则返回所有月份的记录，用于'结算记录'UI。如果传了参数，则返回该月的明细。

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

Tips:
1.对于每个线下代理，其最后一次生成年终奖的时间假设为2016-08-04，则程序会于2017-08-04生成他的年终奖（如果从来未生成过年终奖，则把他成为线下的日期作为最后一次生成年终奖时间）。
因此在2017-08-04之前访问此api将会看不到由2016-08-04\~2017-08-04的年终奖。
2.为简单起见，只有生成年终奖的月份才会看到年终奖。

Return:

{

"status_code": 0,

"data": [

{

"amount": 2600, //进货额

"transferred": 0, //是否已转积分系统

"pcd_name": "广东", //地区名称

"bonus": { //年终奖金

"settled_amount": 11969,

"amount": 23938,

"transferred": 0,

"transferred_amount": 0,

"statistic_month": "2017-07-25",

"pcd_id": 2147,

"year_statistic_amount": 0, //奖金项没有"年累计订单额"

"settlement_proportion": 50,

"id": 19,

"end_month": "2018-07-25",
//代表从statistic_month到end_month的年终奖金

"seller_id": 11014

},

"statistic_month": "2017-10-01", //开始月份

"pcd_id": 2147,

"year_statistic_amount": 2600, //年累计订单额

"settled_amount": 7.8, //提成额

"transferred_amount": 0, //已转积分

"agentPurchaseJournals": [ //根据产品，提成比例来汇总的订单明细

{

"sum_settled_amount": 6, //本月提成

"sum_final_price": 2000, //进货金额

"product_id": 149, //产品id

"agent_proportion_percentage": "0.30", //提成比例（0.30表示0.30%）

"product_name": "碧丽雅超效洁净手洗专用洗衣液1.25L\*10瓶/箱"
//产品名称

},

{

"sum_settled_amount": 12,

"sum_final_price": 4000,

"product_id": 673,

"agent_proportion_percentage": "0.30",

"product_name": "十美优品净澈水润型沐浴露600ml\*4瓶/箱"

},

{

"sum_settled_amount": 1.3,

"sum_final_price": 432,

"product_id": 675,

"agent_proportion_percentage": "0.30",

"product_name": "十美优品滋养修护型护发素600ml\*4瓶/箱"

}

],

"settlement_proportion": 0, //提成比例

"id": 39,

"end_month": null, //结束月份

"seller_id": 11014

},

{

"amount": 2600,

"transferred": 0,

"pcd_name": "广东-广州",

"bonus": {

"settled_amount": 212.16,

"amount": 10608,

"transferred": 0,

"transferred_amount": 0,

"statistic_month": "2017-07-25",

"pcd_id": 2148,

"year_statistic_amount": 0,

"settlement_proportion": 2,

"id": 22,

"end_month": "2018-07-25",

"seller_id": 11014

},

"statistic_month": "2017-10-01",

"pcd_id": 2148,

"year_statistic_amount": 2600,

"settled_amount": 7.8,

"transferred_amount": 0,

"agentPurchaseJournals": [

{

"order_user_id": 11019,

"agent_proportion": 3,

"quantity": 20,

"pcd_name": "广州",

"pcd_id": 2148,

"product_specification_name": null,

"product_name": "十美优品净澈水润型沐浴露600ml\*4瓶/箱",

"order_item_id": 5529,

"settled_amount": 4.8,

"order_user_name": "关应康",

"final_price": 1600,

"price": 80,

"product_id": 673,

"percentage": 10,

"marketing_name": "十美优品净澈水润型沐浴露600ml\*4瓶/箱",

"marketing_id": 14,

"id": 7,

"create_date": "2017-10-09 11:21:34",

"seller_id": 11014,

"product_cover":
"http://images.10mup.com/20170708154457918-gkpUE7r4.jpg"

},

{

"order_user_id": 11019,

"agent_proportion": 3,

"quantity": 10,

"pcd_name": "广州",

"pcd_id": 2148,

"product_specification_name": null,

"product_name": "碧丽雅超效洁净手洗专用洗衣液1.25L\*10瓶/箱",

"order_item_id": 5530,

"settled_amount": 3,

"order_user_name": "关应康",

"final_price": 1000,

"price": 100,

"product_id": 149,

"percentage": 10,

"marketing_name": "碧丽雅超效洁净手洗专用洗衣液1.25L\*10瓶/箱",

"marketing_id": 11,

"id": 8,

"create_date": "2017-10-09 11:21:34",

"seller_id": 11014,

"product_cover":
"http://images.10mup.com/20160914142106802-oFWNcqv1.jpg"

}

],

"settlement_proportion": 0,

"id": 42,

"end_month": null,

"seller_id": 11014

}

]

}

81. **线下代理商查看年终奖励对照表**

GET https://mall.smallsaas.cn/rest/physical_agent_bonus?pcd_id=1 

Paras:

pcd_id: required，地区id

Header: Authorization:
eyJ0b2tlbiI6IjMxODhiZmUxMzM2ZjY0MGQ5ZmU3OTUxMDZkYTUzMjE5MDJlODAwZjAiLCJsb2dpbl9uYW1lIjoiMTIzIn0=

{

"status_code": 0,

"data": [

{

"id": 1,

"percentage": 10, //奖金比例 （当min_amount\<销售额\<=max_amount
，应用此percentage）

"min_amount": 0, //销售额下限

"max_amount": 1000, //销售额上限

"pcd_id": 1

},

{

"id": 2,

"percentage": 20,

"min_amount": 1000,

"max_amount": -1, //-1表示无上限

"pcd_id": 1

}

]

}

82. **线下皇冠商查看被推荐人的进货明细列表**

GET https://mall.smallsaas.cn/rest/physical_
