## 支付API

### 分享订单拿优惠券

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

