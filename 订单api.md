## 订单API

### 订单状态说明

 - CREATED_PAY_PENDING － 待支付

 - CLOSED_PAY_TIMEOUT － 支付超时关闭

 - CLOSED_CANCELED － 已取消

 - PAID_CONFIRM_PENDING － 已支付

 - CONFIRMED_DELIVER_PENDING － 待发货

 - DELIVERING － 发货中

 - DELIVERED_CONFIRM_PENDING－ 已发货

 - CANCELED_RETURN_PENDING － 待退货

 - CLOSED_CONFIRMED － 已确认收货

 - CANCELED_REFUND_PENDING － 待退款

 - CLOSED_REFUNDED － 已退款

 - CONFIRMED_PICK_PENDING － 待取货

### 我的订单列表

GET https://mall.smallsaas.cn/rest/order?pageNumber=1&pageSize=20&status=CREATED_PAY_PENDDING 

Param:

 - pageNumber: 页数，可空，默认1

 - pageSize - 每页记录数，可空，默认50

 - status: 订单状态, optional

Header: Authorization: token

Describe:

 - pay_expiry_time: 待支付订单支付的超时时间

Return:
```json
{
	"status_code": 0,
	"data": [{
		"user_id": 1,
		"phone": "1380000000",
		"contact_user": "Mr Huang",
		"province": "GD",
		"city": "GZ",
		"district": "Tiahne",
		"street": "jianzhong road",
		"detail": "6F",
		"trade_number": null,
		"deal_date": null,
		"express_number": "1232323",
		"express_code": "24234",
		"express_company": "abc",
		"coupon_info": null,
		"zip": "510000",
		"id": 3,
		"cover":"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
		"confirm_date": null,
		"description": "超效洁净护理洗衣液2.5L【全国包邮】 x 1. ",
		"deliver_date": null,
		"created_date": "2016-04-26 10:27:56",
		"order_number": "0000000101461637676506360",
		"status": "CREATED_PAY_PENDING",
		"remark": null,
		"invoice": 1,
		"invoice_title": "ABC company",
		"receiving_time": "anytime",
		"deliver_order_number": null,
		"total_price": 34.80,
		"user_name": "Administrator",
		"freight": 0.00,
		"pay_date": null,
		"payment_type": "ALIPAY",
		"point_exchange_rate": 100,
		"pay_expiry_time": "2018-08-20 17:53:01",
		"order_items": [{
			"quantity": 2,
			"product_specification_id": null,
			"weight": 500,
			"product_specification_name": null,
			"product_name": "REJOICE飘柔家庭护理芦荟长效止痒滋润洗发露400ML",
			"marketing_description": null,
			"cover": "http://images.10mup.com/20161104102243958-v499XJvA.jpg",
			"marketing": null,
			"final_price": 25.8,
			"price": 12.9,
			"product_id": 335,
			"marketing_id": null,
			"id": 5920,
			"bulk": 0,
			"order_id": 3290,
			"partner_level_zone": 1,
			"barcode": "6903148126660",
			"store_location": null,
			"status": "CREATED",
			"cost_price": 10.21
		}]
	}]
}
```

### 我的退货退款订单列表

GET https://mall.smallsaas.cn/rest/refund_order?pageNumber=1&pageSize=20 

Param:

 - pageNumber: 页数，可空，默认1

 - pageSize: 每页记录数，可空，默认50

Header: Authorization: token

Describe:

 - order_customer_service: 售后单信息
 
 - refund_fee: 退款金额

Return:
```json
{
	"status_code": 0,
	"data": [{
		"trade_number": "test_trade_num",
		"pay_date": "2016-12-14 13:42:33",
		"deliver_order_number": null,
		"order_customer_service": { 
			"reason": "AFSFSF",
			"express_code": null,
			"service_type": "REFUND",
			"images": "[]",
			"log": "[{"time":"2016-12-14 01:42:47","user":"Administrator","content":"afaf"}]",
			"refund_fee": null, //退款金额
			"id": 5,
			"created_date": "2016-12-14 13:42:47",
			"express_number": null,
			"order_id": 5,
			"express_company": null,
			"status": "CREATED"
		},
		"city": "GZ",
		"invoice_title": "ABC company",
		"receiving_time": "anytime",
		"user_name": "Administrator",
		"order_number": "1612141342218661",
		"freight": 0,
		"description": "aaaa x 2. ",
		"remark": null,
		"express_company": null,
		"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",
		"express_code": null,
		"is_deleted": 0,
		"province": "GD",
		"street": "jianzhong road",
		"is_deliver_reminder": 0,
		"id": 5,
		"express_number": null,
		"previous_status": "CONFIRMED_DELIVER_PENDING",
		"delivered_date": null,
		"zip": "510000",
		"deal_date": null,
		"total_price": 66,
		"contact_user": "Mr Huang",
		"settled": 0,
		"coupon_info": null,
		"payment_type": "WECHAT",
		"user_id": 1,
		"phone": "1380000000",
		"point_exchange_rate": 100,
		"deliver_date": null,
		"confirm_date": "2016-12-14 13:42:33",
		"district": "Tiahne",
		"created_date": "2016-12-14 13:42:21",
		"invoice": 1,
		"detail": "6F",
		"status": "CANCELED_REFUND_PENDING"
	},{
		"trade_number": "test_trade_num",
		"pay_date": "2016-12-14 11:35:54",
		"deliver_order_number": null,
		"order_customer_service": {
			"reason": "rrr",
			"express_code": null,
			"service_type": "RETURN",
			"images": "[]",
			"log": "[{"time":"2016-12-14
				11:36:32","user":"Administrator","content":"yyy"},{"time":"2016-12-14
				11:36:56","user":"Administrator","content":"ok"},{"time":"2016-12-14
				11:37:00","user":"Administrator","content":"同意"},{"time":"2016-12-14
				11:38:07","user":"Administrator","content":"退货收到确认"},{"time":"2016-12-14
				01:10:24","user":"Administrator","content":"退款失败,
				请稍后重试"},{"time":"2016-12-14
				01:11:08","user":"Administrator","content":"已完成退款"}]",
			"refund_fee": 66,
			"id": 4,
			"created_date": "2016-12-14 11:36:32",
			"express_number": null,
			"order_id": 4,
			"express_company": null,
			"status": "REFUNDED"
		},
		"city": "GZ",
		"invoice_title": "ABC company",
		"receiving_time": "anytime",
		"user_name": "Administrator",
		"order_number": "1612141135416631",
		"freight": 0,
		"description": "aaaa x 2. ",
		"remark": null,
		"express_company": "afa",
		"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",
		"express_code": "afsd",
		"is_deleted": 0,
		"province": "GD",
		"street": "jianzhong road",
		"is_deliver_reminder": 0,
		"id": 4,
		"express_number": "rwrwe4",
		"previous_status": "DELIVERED_CONFIRM_PENDING",
		"delivered_date": "2016-12-14 11:36:05",
		"zip": "510000",
		"deal_date": null,
		"total_price": 66,
		"contact_user": "Mr Huang",
		"settled": 0,
		"coupon_info": null,
		"payment_type": "WECHAT",
		"user_id": 1,
		"phone": "1380000000",
		"point_exchange_rate": 100,
		"deliver_date": "2016-12-14 11:36:03",
		"confirm_date": "2016-12-14 11:35:54",
		"district": "Tiahne",
		"created_date": "2016-12-14 11:35:41",
		"invoice": 1,
		"detail": "6F",
		"status": "CLOSED_REFUNDED"
	},{
		"trade_number": "test_trade_num",
		"pay_date": "2016-12-14 11:27:23",
		"deliver_order_number": null,
		"order_customer_service": {
			"reason": "AFSFSF",
			"express_code": null,
			"service_type": "REFUND",
			"images": "[]",
			"log": "[{"time":"2016-12-14
				11:27:52","user":"Administrator","content":"afaf"},{"time":"2016-12-14
				11:31:17","user":"Administrator","content":"ok"},{"time":"2016-12-14
				11:31:19","user":"Administrator","content":"同意"},{"time":"2016-12-14
				11:32:14","user":"Administrator","content":"更新退款金额为
				58 元"},{"time":"2016-12-14
				11:33:08","user":"Administrator","content":"已完成退款"}]",
			"refund_fee": 58,
			"id": 3,
			"created_date": "2016-12-14 11:27:52",
			"express_number": null,
			"order_id": 3,
			"express_company": null,
			"status": "REFUNDED"
		},
		"city": "GZ",
		"invoice_title": "ABC company",
		"receiving_time": "anytime",
		"user_name": "Administrator",
		"order_number": "1612141127143691",
		"freight": 0,
		"description": "aaaa x 2. ",
		"remark": null,
		"express_company": null,
		"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",
		"express_code": null,
		"is_deleted": 0,
		"province": "GD",
		"street": "jianzhong road",
		"is_deliver_reminder": 0,
		"id": 3,
		"express_number": null,
		"previous_status": "CONFIRMED_DELIVER_PENDING",
		"delivered_date": null,
		"zip": "510000",
		"deal_date": null,
		"total_price": 66,
		"contact_user": "Mr Huang",
		"settled": 0,
		"coupon_info": null,
		"payment_type": "WECHAT",
		"user_id": 1,
		"phone": "1380000000",
		"point_exchange_rate": 100,
		"deliver_date": null,
		"confirm_date": "2016-12-14 11:27:23",
		"district": "Tiahne",
		"created_date": "2016-12-14 11:27:14",
		"invoice": 1,
		"detail": "6F",
		"status": "CLOSED_REFUNDED"
	},{
		"trade_number": "test_trade_num",
		"pay_date": "2016-12-13 15:35:06",
		"deliver_order_number": null,
		"order_customer_service": {
			"reason": "AFSFSF",
			"express_code": null,
			"service_type": "RETURN",
			"images": "[]",
			"log": "[{"time":"2016-12-13
				03:35:30","user":"Administrator","content":"afaf"},{"time":"2016-12-13
				03:35:38","user":"Administrator","content":"afd"},{"time":"2016-12-13
				03:35:46","user":"Administrator","content":"同意"},{"time":"2016-12-13
				03:35:51","user":"Administrator","content":"退货收到确认"},{"time":"2016-12-13
				03:35:55","user":"Administrator","content":"更新退款金额为
				60 元"},{"time":"2016-12-13
				03:37:12","user":"Administrator","content":"更新退款金额为
				61 元"},{"time":"2016-12-13
				03:48:57","user":"Administrator","content":"a"},{"time":"2016-12-13
				03:52:01","user":"Administrator","content":"com.jfeat.order.exception.RefundOrderException:
				order.refund.failure"},{"time":"2016-12-13
				03:52:55","user":"Administrator","content":"java.lang.RuntimeException:
				com.jfeat.order.exception.RefundOrderException:
				order.refund.failure"},{"time":"2016-12-13
				04:00:49","user":"Administrator","content":"com.jfeat.order.exception.RefundOrderException:
				order.refund.failure"},{"time":"2016-12-13
				04:11:29","user":"Administrator","content":"fsdas"},{"time":"2016-12-13
				04:11:36","user":"Administrator","content":"更新退款金额为
				60 元"},{"time":"2016-12-13
				04:11:41","user":"Administrator","content":"退款失败,
				请稍后重试"},{"time":"2016-12-13
				05:18:40","user":"Administrator","content":"退款失败,
				请稍后重试"},{"time":"2016-12-14
				11:26:17","user":"Administrator","content":"已完成退款"}]",
			"refund_fee": 60,
			"id": 2,
			"created_date": "2016-12-13 15:35:30",
			"express_number": null,
			"order_id": 2,
			"express_company": null,
			"status": "REFUNDED"
		},
		"city": "GZ",
		"invoice_title": "ABC company",
		"receiving_time": "anytime",
		"user_name": "Administrator",
		"order_number": "1612131532015531",
		"freight": 0,
		"description": "aaaa x 2. ",
		"remark": "afafafafafafa",
		"express_company": "afa",
		"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",
		"express_code": "afsd",
		"is_deleted": 0,
		"province": "GD",
		"street": "jianzhong road",
		"is_deliver_reminder": 0,
		"id": 2,
		"express_number": "234",
		"previous_status": "DELIVERED_CONFIRM_PENDING",
		"delivered_date": "2016-12-13 15:35:16",
		"zip": "510000",
		"deal_date": null,
		"total_price": 66,
		"contact_user": "Mr Huang",
		"settled": 0,
		"coupon_info": null,
		"payment_type": "WECHAT",
		"user_id": 1,
		"phone": "1380000000",
		"point_exchange_rate": 100,
		"deliver_date": "2016-12-13 15:35:14",
		"confirm_date": "2016-12-13 15:35:06",
		"district": "Tiahne",
		"created_date": "2016-12-13 15:32:01",
		"invoice": 1,
		"detail": "6F",
		"status": "CLOSED_REFUNDED"
	},{
		"trade_number": "test_trade_num",
		"pay_date": "2016-12-13 14:01:47",
		"deliver_order_number": null,
		"order_customer_service": {
			"reason": "AFSFSF",
			"express_code": null,
			"service_type": "RETURN",
			"images": "[]",
			"log": "[{"time":"2016-12-13
				02:03:26","user":"Administrator","content":"afaf"},{"time":"2016-12-13
				02:03:41","user":"Administrator","content":"同意"},{"time":"2016-12-13
				02:03:44","user":"Administrator","content":"退货收到确认"},{"time":"2016-12-13
				02:12:38","user":"Administrator","content":"更新退款金额为
				{0} 元"},{"time":"2016-12-13
				02:13:42","user":"Administrator","content":"更新退款金额为
				62 元"},{"time":"2016-12-13
				02:17:23","user":"Administrator","content":""},{"time":"2016-12-13
				02:24:43","user":"Administrator","content":"更新退款金额为
				61 元"},{"time":"2016-12-13
				02:33:33","user":"Administrator","content":""},{"time":"2016-12-13
				02:34:49","user":"Administrator","content":"更新退款金额为
				60 元"},{"time":"2016-12-13
				02:35:04","user":"Administrator","content":"已完成退款"}]",
			"refund_fee": 60,
			"id": 1,
			"created_date": "2016-12-13 14:03:26",
			"express_number": null,
			"order_id": 1,
			"express_company": null,
			"status": "REFUNDED"
		},
		"city": "GZ",
		"invoice_title": "ABC company",
		"receiving_time": "anytime",
		"user_name": "Administrator",
		"order_number": "1612131401365671",
		"freight": 0,
		"description": "aaaa x 2. ",
		"remark": null,
		"express_company": "afa",
		"cover": "/p/7fe63684ff08bb7cb6414742232776ac.jpeg",
		"express_code": "afsd",
		"is_deleted": 0,
		"province": "GD",
		"street": "jianzhong road",
		"is_deliver_reminder": 0,
		"id": 1,
		"express_number": "324242",
		"previous_status": "DELIVERED_CONFIRM_PENDING",
		"delivered_date": "2016-12-13 14:02:41",
		"zip": "510000",
		"deal_date": null,
		"total_price": 66,
		"contact_user": "Mr Huang",
		"settled": 0,
		"coupon_info": null,
		"payment_type": "WECHAT",
		"user_id": 1,
		"phone": "1380000000",
		"point_exchange_rate": 100,
		"deliver_date": "2016-12-13 14:02:15",
		"confirm_date": "2016-12-13 14:01:47",
		"district": "Tiahne",
		"created_date": "2016-12-13 14:01:36",
		"invoice": 1,
		"detail": "6F",
		"status": "CLOSED_REFUNDED"
	}]
}
```

### 我的订单详情

GET https://mall.smallsaas.cn/rest/order/{orderNumber}

Param: 

 - orderNumber: 订单号

Header: Authorization: token

Describe:

 - deal_date: 收货成交时间

 - confirm_date: 平台确认时间

Return:
```
{
	"status_code": 0,
	"data": {
		"detail": "6F",
		"phone": "1380000000",
		"contact_user": "Mr Huang",
		"remark": null,
		"invoice": 1,
		"street": "jianzhong road",
		"trade_number": null,
		"deal_date": null, 
		"city": "GZ",
		"id": 3,
		"cover":"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
		"confirm_date": null, 
		"description": "超效洁净护理洗衣液2.5L【全国包邮】 x 1. ",
		"province": "GD",
		"order_items": [{
		"id": 5,
		"cover":"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
		"price": 34.80,
		"cost_price": 20.00,
		"final_price": 34.80,
		"product_id": 1,
		"status": "CREATED",
		"product_name": "超效洁净护理洗衣液2.5L【全国包邮】",
		"quantity": 1,
		"order_id": 3,
		"product_specification_id": 2,
		"product_specification_name": "a1" //用户选择的规格
		}],
		"user_id": 1,
		"district": "Tiahne",
		"deliver_date": null, //开始发货时间
		"delivered_date": null, //完成发货时间
		"created_date": "2016-04-26 10:27:56", //创建时间
		"order_number": "0000000101461637676506360",
		"zip": "510000",
		"status": "CREATED_PAY_PENDING",
		"invoice_title": "ABC company",
		"receiving_time": "anytime",
		"deliver_order_number": null,
		"total_price": 34.80,
		"freight": 0.00,
		"pay_date": null, //支付时间
		"payment_type": "ALIPAY",
		"point_exchange_rate": 100, //积分支付时的兑换率
		"pay_expiry_time": "2018-08-20 17:53:01",//待支付订单支付的超时时间
		"order_customer_service": {
			"reason": "afaf", //退货原因
			"express_code": null,
			"service_type": "RETURN", //售后类型： RETURN－退货退款，REFUND－仅退款
			"id": 1,
			"created_date": "2016-06-16 13:57:12",
			"express_number": "23234324", //快递单号
			"order_id": 1,
			"express_company": "ABC" //快递公司名
		}
	}
}
```

Error Return:
```json
{
	"message": "invalid.order.id",
	"status_code": 1
}
```

### 我的订单数量统计

GET https://mall.smallsaas.cn/rest/order_count 

Header: Authorization: token

Describe:

 - total: 总订单

 - payPending: 待支付

 - delivering: 待发货

 - delivered: 待收货

 - commentPending: 待评价

Return:
```json
{
	"status_code": 0,
	"data": {
		"total": 12, 
		"payPending": 2, 
		"delivering": 4, 
		"delivered": 2, 
		"commentPending": 2 
	}
}
```

### 提醒发货

GET https://mall.smallsaas.cn/rest/order_deliver_reminder/{orderNumber} 

Param: 
 - orderNumber: 订单号

Header: Authorization: token

Return:
```json
{
	"message": "order.deliver.reminded",
	"status_code": 0
}
```

### 订单评价

PUT https://mall.smallsaas.cn/rest/order_comment/{orderNumber}

Param: 

 - orderNumber: 订单号

Header: Authorization: token

Data:
```json
{ "comment_id": "12345" }
```

Return:
```json
{
	"message": "ok",
	"status_code": 0
}
```

### 新建订单

POST https://mall.smallsaas.cn/rest/order 

参考 下单前计算优惠信息 api 返回的优惠券，选择一个优惠劵进行下单。

到支付宝支付时，把order-number的值赋给out_trade_no进行支付。

微信支付: WECHAT

积分支付: POINT

钱包支付: WALLET

```
/**
 * 订单来源
 */
public enum Origin {
	//微信公众号(Wechat public account)
	WPA,
	//小程序
	MINI_PROGRAM,
	//手机应用程序
	APP_ANDROID,
	APP_IOS,
	//其他
	OTHER
}
```

Header: Authorization: token

Data:
```
{
	//配送方式：
	//1. EXPRESS-快递（默认，当不传此参数或传递null时会使用此方式）
	//2. SELF_PICK-自提（当使用此方式时，必须同时指定store_id和store_name）
	//3. FLASH-极速送达（当使用此方式时，必须同时指定store_id和store_name)
	//SELF_PICK和FLASH方式的线上订单，需要店员登录ipad端处理
	"delivery_type": null,
	//订单来源
	//optional。default OTHER
	//WPA（Wechat public account)-微信公众号 MINI-PROGRAM-小程序
	APP-手机应用程序 OTHER-其他
	"origin": "APP",
	"pay_credit": 120, //使用积分抵扣
	"store_id": "123", //门店id
	"store_name": "门店1", //门店名
	"payment_type": "WECHAT",
	"remark": null,
	"receiving_time": "anytime", //收货时间
	"invoice": 1, //是否开发票
	"invoice_title": "ABC company", //发票抬头
	"contact": {
	"contact_user": "Mr Huang",
	"phone": "1380000000",
	"zip": "510000",
	"province": "GD",
	"city": "GZ",
	"district": "Tiahne",
	"street": "jianzhong road",
	"detail": "6F"
},
"order_items": [{
	"product_id": 1,
	"quantity": 2,
	"product_specification_id": 1 //optional，用户选择的产品规格，如果没有则不需要这个项
	}]
}
```

Return:
```
{
	"status_code": 0,
	"data": {
		"created_date": "2016-04-25",
		"order_number": "0000000101461584134091428",
		"status": "CREATED_PAY_PENDING",
		"remark": null,
		"total_price": 290.00,
		"id": 2,
		"cover": "https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
		"description": "p1 x 2. ",
		"freight": 0.00,
		"province": "GD",
		"city": "GZ",
		"district": "LW",
		"street": "AX",
		"detail": null,
		"zip": "510000",
		"phone": "1390000000",
		"contact_user": "ABC",
		"receiving_time": "anytime",
		"invoice": 1,
		"invoice_title": "ABC company",
		"order_items": [{
			"id": 1,
			"cover": "https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
			"price": 145.00,
			"final_price": 290.00,
			"cost_price": 0.00,
			"product_id": 1,
			"status": "CREATED",
			"product_name": "p1",
			"quantity": 2,
			"order_id": 2，
			"product_specification_id": 2,
			"product_specification_name": "a1" //用户选择的产品规格
		}],
		"user_id": 1,
		"payment_type": null
	}
}
```

### 店员新建订单

POST https://mall.smallsaas.cn/rest/store/order 

Header: Authorization: token

Data:
```
{
	//以下两个字段是店员新建订单api额外需要提供的
	"store_id": 123, //required 店铺id
	"store_name": "龙门客栈", //required 店铺名称
	//其他需要提供的域同"新建订单api"
	"payment_type": "WECHAT",
	// 使用积分抵扣
	"pay_credit": 120,
	//订单来源
	//optional。default OTHER
	//WPA（Wechat public account)-微信公众号 MINI-PROGRAM-小程序 APP-手机应用程序 OTHER-其他
	"origin": "APP",
	"remark": null,
	"receiving_time": "anytime", //收货时间
	"invoice": 1, //是否开发票
	"invoice_title": "ABC company", //发票抬头
	"contact": {
	"contact_user": "Mr Huang",
	"phone": "1380000000",
	"zip": "510000",
	"province": "GD",
	"city": "GZ",
	"district": "Tiahne",
	"street": "jianzhong road",
	"detail": "6F"
},
"order_items": [{
	"product_id": 1, //required, 产品id
	"product_specification_id": 1, //optional,产品规格id
	"quantity": 2 //数量
}]
```

Return: 同"新建订单api"

### 店员更新订单状态

PUT https://mall.smallsaas.cn/rest/store/order/order-number

Header: Authorization: token

> 注：店员操作的订单有两种：

> 1.线下订单。
> 收银员调用 \`店员创建订单API\` 下单，此API下单后会立刻返回此订单的信息，此订单的状态为"未支付"，配送方式为"自提"。
> 稍后收银员收到钱之后，认为交易完成了，可以执行"完成(complete)"操作来完成交易。
> 当然客户可以随时取消交易，此时收银员需执行 "取消(cancel)"操作。

> 2.终端用户下的线上订单。这种订单又可分为3种：
> 1. 配送方式为"快递"的订单。这种是以前的方式。
> 2. 配送方式为"自提"的订单（delivery_type:SELF_PICK)。这种方式的订单在下单时就指定了门店自提，即订单是关联一个店铺的。

> 对于这种订单，终端用户在下单并支付之后，订单的状态为"已支付待确认"（即待处理），此时店员可以在ipad端对此订单执行
> "受理(accept)"操作,只能受理，受理后会关联结算店员，订单状态变为CONFIRMED_PICK_PENDING 待取货。
> "受理(accept)"后的自提单(订单状态是CONFIRMED_PICK_PENDING)，如果用户上门取货了，店员可以"完成(complete)"此订单。

> 3. 配送方式为"极速送达"的订单（delivery_type:FLASH)。这种方式的订单在下单时就指定了极速送达（可能是用门店相关的物流系统），即订单也是关联一个店铺的。

> 对于这种订单，终端用户在下单并支付之后，订单的状态为"已支付待确认"（即待处理），此时店员可以在ipad端对此订单执行"受理(accept)"/"拒绝(reject)"操作。
> 拒绝通常是店员发现该店铺没货或其他原因导致本店铺不能处理该订单，这种情况下，api收到拒绝操作的请求，会把该订单所关联的店铺清空，好让平台可以指定其他
> 门店来处理此订单。

> "受理(accept)"后的极速送达单处于待配送状态，如果店铺开始配送了，可以执行"开始配送delivering"操作。

> 开始配送的订单，在店铺把货物送达客户，店员就执行"完成(complete)"来完成订单，不需终端用户自己按完成。

> 注：不关联店铺的订单，店员是看不到的。比如上面介绍的本来是关联了一个店铺，但后来被店员拒绝的订单，拒绝之后，该订单就不关联此店铺了，需要由平台自行重新指定这个订单关联的店铺。

Data:
```
{
	"store_id": "123", //required，店铺id
	"action": "complete" //required, （complete-完成 cancel-取消 accept-受理 reject-拒绝 delivering-开始配送）
}
```

Return:
```
{
	"status_code": 0,
	"message": "更新订单成功"
}
```

### 店员查看门店订单列表（线上，线下订单都在这里查看）

GET https://mall.smallsaas.cn/rest/store/order?pageNumber=1&pageSize=30&storeId=xxx&type=STORE_ORDER&status=CREATED_PAY_PENDING&status=PAID_CONFIRM_PENDING&contactUser=zhangsan&phone=111111&orderNumber=aaa&startTime=2018-05-01&endTime=2018-05-20 

Header: Authorization: token

Param:

 - storeId: required，店铺id

 - type: required，订单类型（ORDER 线上订单 STORE_ORDER 线下订单）

 - status: optional。可多个

 - contactUser: 联系人姓名

 - phone: 联系人电话

 - orderNumber: 订单号

 - startTime \~ endTime：返回的订单的创建时间在startTime \~ endTime之间

> 注意：
> type：
> (1)STORE_ORDER：线下订单（由店员下的单） （ipad端收银 → 历史订单页面需传type=STORE_ORDER）
> (2)ORDER：线上订单（由终端用户下的单）（分两种：1.配送方式为"快递"的单 2.配送方式为"自提"或"极速送达"的单，这样的单在下单时是关联了一个店铺的。由于本api必须传递storeId，因此返回的订单只可能是"线下订单"或者"配送方式为自提或极速送达的线上订单" （ipad端 → 线上待处理订单 → 全部订单需传type=ORDER）

Return:
```
{
	"status_code": 0,
	"data": {
		"totalRow": 1,
		"pageNumber": 1,
		"firstPage": true,
		"lastPage": true,
		"totalPage": 1,
		"pageSize": 30,
		"list": [{
			"trade_number": null,
			"type": "STORE_ORDER",
			"express_company": null,
			"cover": "http://120.79.77.207:8080/images/p/0ea3308197aaccd2635c4b7d31717537.jpeg",
			"store_user_name": "user123",
			"express_code": null,
			"province": "",
			"delivery_type": "SELF_PICK",
			"id": 1,
			"previous_status": null,
			"delivered_date": null,
			"zip": "",
			"deal_date": null,
			"pay_credit": 0,
			"contact_user": "",
			"settled": 0,
			"coupon_info": null,
			"payment_type": "STORE",
			"store_user_id": "2",
			"user_id": 2,
			"phone": "",
			"point_exchange_rate": 100,
			"deliver_date": null,
			"confirm_date": null,
			"district": "",
			"detail": "",
			"status": "CREATED_PAY_PENDING",
			"pay_date": null,
			"deliver_order_number": null,
			"city": "",
			"invoice_title": null,
			"receiving_time": "anytime",
			"user_name": "user123",
			"order_number": "1807181114341472",
			"freight": 0,
			"description": "测试1 x 8. ",
			"mid": null,
			"remark": "iPad 端收银界面",
			"mname": null,
			"is_deleted": 0,
			"street": "",
			"store_name": null,
			"is_deliver_reminder": 0,
			"express_number": null,
			"store_id": null,
			"total_price": 8,
			"marketing_description": null,
			"marketing": null,
			"marketing_id": null,
			"created_date": "2018-07-18 11:14:34",
			"invoice": 0
		}]
	}
}
```

### 店员查看门店订单详情

GET https://mall.smallsaas.cn/rest/store/order/order-number

Header: Authorization: token

Return:
```
{
	"status_code": 0,
	"data": {
		"trade_number": null,
		"type": "STORE_ORDER",
		"express_company": null,
		"cover": "http://120.79.77.207:8080/images/p/0ea3308197aaccd2635c4b7d31717537.jpeg",
		"store_user_name": "user123",
		"express_code": null,
		"province": "",
		"delivery_type": "SELF_PICK",
		"id": 1,
		"previous_status": null,
		"delivered_date": null,
		"order_items": [{
			"quantity": 8,
			"product_specification_id": null,
			"weight": 111,
			"product_specification_name": null,
			"product_name": "测试1",
			"marketing_description": null,
			"cover": "http://120.79.77.207:8080/images/p/0ea3308197aaccd2635c4b7d31717537.jpeg",
			"marketing": null,
			"final_price": 8,
			"price": 1,
			"product_id": 1,
			"marketing_id": null,
			"id": 1,
			"bulk": null,
			"order_id": 1,
			"partner_level_zone": 1,
			"barcode": null,
			"store_location": null,
			"status": "CREATED",
			"cost_price": 1
		}],
		"zip": "",
		"deal_date": null,
		"pay_credit": 0,
		"contact_user": "",
		"settled": 0,
		"coupon_info": null,
		"payment_type": "STORE",
		"store_user_id": "2",
		"user_id": 2,
		"phone": "",
		"point_exchange_rate": 100,
		"deliver_date": null,
		"confirm_date": null,
		"district": "",
		"detail": "",
		"status": "CREATED_PAY_PENDING",
		"pay_date": null,
		"deliver_order_number": null,
		"order_customer_service": null,
		"city": "",
		"invoice_title": null,
		"receiving_time": "anytime",
		"order_number": "1807181114341472",
		"freight": 0,
		"description": "测试1 x 8. ",
		"mid": null,
		"remark": "iPad 端收银界面",
		"mname": null,
		"is_deleted": 0,
		"street": "",
		"store_name": null,
		"is_deliver_reminder": 0,
		"express_number": null,
		"store_id": null,
		"total_price": 8,
		"marketing_description": null,
		"marketing": null,
		"marketing_id": null,
		"created_date": "2018-07-18 11:14:34",
		"invoice": 0
	}
}
```

### 店员新建售后单

POST https://mall.smallsaas.cn/rest/store/order_customer_service 

Header: Authorization: token

Data:
```
{
	"store_id": "1", //required，店铺id
	"store_name": "总店", // required，店铺名
	//退货单分为"有关联订单的退货单"和"没有关联订单的退货单"，换货单必须关联订单。因此对于没有关联订单的退货单，不需传递order_number，对于其他两种，则必须传递order_number
	"order_number": "2342323432432",
	"service_type": "RETURN", //required，REFUND-仅退款 RETURN-退货退款 EXCHANGE-换货
	"reason": "AFSFSF", //required
	"content": "afaf", //optional
	"images": ["http://host/a.jpg", "http://host/b.jgp"], //optional
	"returns": [ //退货项
	{
		"product_id": 130,
		//required（无论是否提供product_specification_id，都要提供product_id）
		"product_specification_id": 22, //optional
		// 1.对于需要关联订单的退货单，不需要传递quantity，会使用其对应的order item的quantity；
		// 2.对于不需要关联订单的退货单，必须传递quantity
		// 3.对于一定要关联订单的换货单，这种单据有两个清单（退货项清单和置换项清单）。无论是退货项还是置换项，都必须指定quantity "quantity": 3, 对于退货单的退货项，必须指定refund_fee； 对于换货单的退货项，无需指定refund_fee，refund_fee由 "此换货单关联的订单对应的订单项的 price \* 传上来的退回数量" 决定
		"refund_fee": 40
	}],
	"exchanges": [ //置换项
	{
		"product_id": 122, //required
		"quantity": 2 //required refund_fee无需提供
	},
	{
		"product_id": 130, //required
		"product_specification_id": 22, //optional
		// 1.对于需要关联订单的退货单，不需要传递quantity，会使用其对应的order item的quantity；
		// 2.对于不需要关联订单的退货单，必须传递quantity
		// 3.对于一定要关联订单的换货单，这种单据有两个清单（退货项清单和置换项清单）。无论是退货项还是置换项，都必须指定quantity
		"quantity": 3, //required
		//refund_fee无需提供
	}]
}
```

Return:
```
{
	"status_code": 0,
	"message": "order.customer.service.created"
}
```

### 店员查看单个售后单

GET https://mall.smallsaas.cn/rest/store/order_customer_service/service_number

Param:

 - service_number: 售后单号

Header: Authorization: token

Return:
```
{
	"status_code": 0,
	"data": {
		"store_id": "1",
		"reason": "AFSFSF",
		"images": "["http://host/a.jpg","http://host/b.jgp"]",
		"log": "[{"time":"2018-07-21 02:38:10","user":"Administrator","content":"afaf"}]",
		"exchanges": [ //置换项（置换清单）（仅换货单有此项）
			{
				"quantity": 2, //数量
				"product_specification_id": null, //产品规格id
				"weight": 111, //重量
				//项类型（RETURN - 退货项（退货单的项和换货单中的退货清单的项都属于此类型） EXCHANGE - 置换项）
				"type": "EXCHANGE",
				"product_specification_name": null,
				"order_customer_service_id": 3, //售后单id
				"product_name": "水桶", //产品名
				"marketing_description": null, //营销活动描述
				"cover": "/p/dbe108b7e5c0283013ebc956f2cc2f4b.jpg",
				"marketing": null,
				"final_price": 22, //总价值
				"price": 11, //价格
				"refund_fee": null, //置换项没有退回金额，此处必为null
				"product_id": 2, //产品id
				"marketing_id": null, //营销活动id
				"id": 6,
				"cost_price": 1 //成本价
			}
		],
		"express_company": null,
		"store_user_name": "Administrator", //店员名
		"express_code": null, //快递单号
		"service_type": "EXCHANGE", //售后单类型（REFUND-仅退款	RETURN-退货退款 EXCHANGE-换货）
		"store_user_id": "1", //店员id
		//1.如果是退货单，此金额为此次退回应退回的金额。
		//2.如果是换货单，且退回项总价值大于置换项总价值，则有refund_fee；若小于，则有supplementary_fee
		"refund_fee": 68, //退回金额
		"supplementary_fee": null, //补交金额
		"store_name": "总店", //店铺名
		"returns": [ //退货清单
			{
				"quantity": 3,
				"product_specification_id": null,
				"weight": 0,
				//项类型（RETURN - 退货项（退货单的项和换货单中的退货清单的项都属于此类型） EXCHANGE - 置换项）
				"type": "RETURN",
				"product_specification_name": null,
				"order_customer_service_id": 3,
				"product_name": "IPHONE",
				"marketing_description": null,
				"cover": null,
				"marketing": null,
				"final_price": 90,
				"price": 30,
				"refund_fee": 90, //退回金额
				"product_id": 1,
				"marketing_id": null,
				"id": 5,
				"cost_price": 0
			}
		],
		"id": 3,
		"created_date": "2018-07-21 14:38:13",
		"express_number": null,
		"service_number": "180721143813797Administrator",
		"order_id": 1,
		"status": "CREATED",
		"order": { //该售后单所关联的订单（如果售后单没有关联订单，则order不存在）
			"trade_number": null,
			"type": "ORDER",
			"express_company": null,
			"cover": null,
			"store_user_name": null,
			"express_code": null,
			"province": "广东",
			"delivery_type": "EXPRESS",
			"id": 1,
			"previous_status": "DELIVERED_CONFIRM_PENDING",
			"delivered_date": "2018-07-20 12:58:40",
			"zip": null,
			"deal_date": null,
			"pay_credit": 0,
			"contact_user": "admin",
			"settled": 0,
			"coupon_info": null,
			"payment_type": "WECHAT",
			"store_user_id": null,
			"user_id": 1,
			"phone": "111",
			"point_exchange_rate": 100,
			"deliver_date": "2018-07-20 12:58:36",
			"confirm_date": "2018-07-20 12:58:32",
			"district": "荔湾区",
			"detail": null,
			"status": "CANCELED_RETURN_PENDING",
			"pay_date": "2018-07-21 12:58:23",
			"deliver_order_number": "111",
			"city": "广州",
			"invoice_title": null,
			"receiving_time": null,
			"order_number": "17072614522001811012",
			"freight": 0,
			"description": null,
			"mid": null,
			"remark": null,
			"mname": null,
			"is_deleted": 0,
			"street": null,
			"store_name": null,
			"is_deliver_reminder": 0,
			"express_number": null,
			"store_id": null,
			"total_price": 500,
			"marketing_description": null,
			"marketing": null,
			"marketing_id": null,
			"created_date": "2018-07-20 12:58:19",
			"invoice": 0
		},
		"order_items": [ ////该售后单所关联的订单的订单项
			{
				"quantity": 3,
				"product_specification_id": null,
				"weight": 0,
				"product_specification_name": null,
				"product_name": "IPHONE",
				"marketing_description": null,
				"cover": null,
				"marketing": null,
				"final_price": 90,
				"price": 30,
				"product_id": 1,
				"marketing_id": null,
				"id": 1,
				"bulk": 0,
				"order_id": 1,
				"partner_level_zone": null,
				"barcode": null,
				"store_location": null,
				"status": "CREATED",
				"cost_price": 0
			}
		]
	}
}
```

### 店员查看订单数量统计

GET https://mall.smallsaas.cn/rest/store/order_count?storeId=1 

Header: Authorization: token

Param:

 - storeId: 门店的ID

Return:
```
{
	"status_code": 0,
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
```

### 店员查看售后单列表

GET https://mall.smallsaas.cn/rest/store/order_customer_service?pageNumber=1&pageSize=30&storeId=123&serviceType=RETURN&serviceNumber=1234&startTime=2018-01-01&endTime=2018-02-02

Param:

 - storeId: optional,门店id

 - service_number: optional,售后单号

 - serviceType: optional, 售后单类型(REFUND-仅退款 RETURN-退货退款 EXCHANGE-换货）

 - startTime \~ endTime: 若同时提供，则返回创建时间在此范围内的售后单列表

Header: Authorization: token

Return:
```
{
	"status_code": 0,
	"data": {
		"totalRow": 1,
		"pageNumber": 1,
		"lastPage": true,
		"firstPage": true,
		"totalPage": 1,
		"pageSize": 30,
		"list": [{
			"store_id": "1", //门店id
			"reason": "AFSFSF", //原因
			"images": "["http://host/a.jpg","http://host/b.jgp"]",
			"log": "[{"time":"2018-07-21 02:38:10","user":"Administrator","content":"afaf"}]",
			"user_name": "Administrator", //订单用户id
			"order_number": "17072614522001811012", //订单号
			"express_company": null, //快递公司
			"store_user_name": "Administrator", //店员名
			"express_code": null,
			"service_type": "EXCHANGE", //售后单类型（REFUND-仅退款 RETURN-退货退款 EXCHANGE-换货）
			"store_user_id": "1", //店员id
			"refund_fee": 68, //退款金额
			"supplementary_fee": null, //补交金额
			"store_name": "总店", //门店名称
			"id": 3,
			"created_date": "2018-07-21 14:38:13",
			"express_number": null, //快递单号
			"service_number": "180721143813797Administrator", //售后单单号
			"order_id": 1,
			"status": "CREATED"
		}]
	}
}
```

### 删除订单

DELETE https://mall.smallsaas.cn/rest/order/order-number

> 注意：
> 只有订单状态为一下四种时可以删除：
> 1. CLOSED_PAY_TIMEOUT
> 2. CLOSED_CANCELED
> 3. CLOSED_CONFIRMED 同时 settled 字段是 1
> 4. CLOSED_REFUNDED

Param:

 - order-number : 订单号

Header: Authorization: token

Return:
```
{
	"status_code": 0,
	"message": "order.delete.success"
}
```

### 分享订单拿优惠券

POST https://mall.smallsaas.cn/rest/order_share

只有CLOSED_CONFIRMED的订单才可以分享。

Header: Authorization: token

Data：
```
{
	"order_number": "2343243242"
}
```

Return:
```
{
	"status_code": 1,
	"data": {
		"code": "wrwfafef",
		//分享code，用这个code去构建分享到朋友圈时的链接的参数。
		"order_number": "2343243242"
	}
}
```

### 查看售后原因列表

GET https://mall.smallsaas.cn/rest/customer_service_type

Header: Authorization: token

Return:
```
{
	"status_code": 0,
	"data": [{
		"name": "fasfa",
		"id": 1
	},{
		"name": "e34543kkk",
		"id": 2
	}]
}
```

### 新建售后单

POST https://mall.smallsaas.cn/rest/order_customer_service


> 订单到达 DELIVERED_CONFIRM_PENDING (待收货） 可以发起退货申请
> 订单状态变成 CANCELED_RETURN_PENDING （待退货），订单项状态变为退货中， 退货单状态为新建后台通过后，退货单变为 待退货后台收到退货后，变成 待退款
> 后台完成退款，订单状态变为 DELIVERED_CONFIRM_PENDING（如果还有其他商品没有退货），变为 REFUNDED（已退款，如果所有商品都退了），订单项状态变为 已退款，退货单状态变为已退款。
> 退货单状态 ： 待处理（CREATED）， RETURN_PENDING (待退货）, REFUND_PENDING (待退款） REFUNDED （已退款）， CANCELED （取消/拒绝）
> 当订单状态是**CONFIRMED_DELIVER_PENDING** 或者**DELIVERED_CONFIRM_PENDING** 时，可以发起退款（service_type is REFUND) 请求。
> 当订单状态是**DELIVERED_CONFIRM_PENDING** 时，可以发起退货退款（service_type is RETURN) 请求 或 换货 （service_type is EXCHANGE)请求。

Header: Authorization: token

Data:
```
{
	"order_number": "2342323432432", //订单号
	"service_type": "RETURN", //RETURN: 退货退款, REFUND: 仅退款，EXCHANGE: 换货
	"reason": "AFSFSF", //原因
	"content": "不要了。", //回复信息
	"images": ["http://localhost/image/a.jpg", "http://loalhost/image/b.jpg"],
	"returns": [ //退货产品
		{
			"product_id": 1,
			"quantity": 2
		},
		{
			"product_id": 2,
			"quantity": 2
		}
	]
}
```

### 查看售后单

GET https://mall.smallsaas.cn/rest/order_customer_service/:id

Header: Authorization: token

Param: 

 - id

> 售后单状态说明：
> CREATED: 待处理
> HANDLING: 处理中
> RETURN_PENDING: 等待货品寄回
> DELIVING: 换货中
> REFUND_PENDING: 待退款
> REFUNDED: 已退款
> CANCELED: 已取消
> EXCHANGED: 已换货

Return:
```
{
	"status_code": 0,
	"data": {
	"reason": "AFSFSF",
	"express_code": null,
	"service_type": "RETURN",
	"images": [
		"http://o9ixtumvv.bkt.clouddn.com/20160729173227596-Vo1I7nGC.png",
		"http://o9ixtumvv.bkt.clouddn.com/20160729173227596-Vo1I7nGC.png"
	],
	"log": [{
		"time": "2016-07-29 05:39:19",
		"user": "Administrator",
		"content": "不要了。"
	}],
	"id": 1,
	"created_date": "2016-07-29 17:39:19",
	"express_number": null,
	"order_id": 1,
	"express_company": null,
	"status": "CREATED"
	}
}
```

### 更新售后单

PUT https://mall.smallsaas.cn/rest/order_customer_service/:id

> 对申请退货的订单更新物流信息.

Header: Authorization: token

Param:

 - id

Data:
```
{
	"express_company": "ABC", //optional, 快递公司名称
	"express_number": "23234324", //optional, 快递单号
	"content": "anymessage" //optional， 回复给平台的消息
}

### 微信支付

GET http://www.kequandian.net/app/payment/wpay/order-number

> 微商城专用支付URL。
> 注意： 这个URL不是API的地址，是app所在服务器的地址. 可以直接访问/app/payment/wpay/order_number
> 新建订单成功后，把order_number作为参数调用这个URL，会发引微信支付请求。

### 微信支付码生成

POST https://mall.smallsaas.cn/rest/wx/push_order

Header: Authorization: token

> PC商城/PAD端 用于生成支付二维码。
> PC端应该根据返回的codeUrl生成二维码，给用户扫码

Data:
```
{
	"order_type": "Order",
	"order_number": "12346", //订单号
	"type": "NATIVE" //type必须是NATIVE
}
```

Return:
```
{
	"status_code": 0,
	"data": {
		"timeStamp": "1533188289",
		"codeUrl": "weixin://wxpay/bizpayurl?pr=bJ1XIh4",
		"package": "prepay_id=wx02133732079021563094f24c1615005248",
		"paySign": "7EEC46D61249DD469759CF598284A0DC",
		"totalFee": "11",
		"appId": "wx117676b671891683",
		"signType": "MD5",
		"title": "DEMO",
		"nonceStr": "1533188289855"
	}
}
```

### 确认订单

PUT https://mall.smallsaas.cn/rest/order/{orderNumer} 

> 用户收货后确认订单。订单当前状态是 DELIVERED_CONFIRM_PENDING时才可以确认。

Param: 

 - orderNumer: 订单号

Header: Authorization: token

Data:
```
{
	"status":"CLOSED_CONFIRMED"
}
```

Return:
```
{
	"message": "order.updated",
	"status_code": 0
}
```

Error Return:
```
{
	"message": "order.status.transfer.error",
	"status_code": 1
}
```
