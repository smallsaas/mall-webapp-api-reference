# 支付API

## 微信支付

GET https://mall.smallsaas.cn/app/payment/wpay/order-number

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


## 支付宝支付

POST [http://host:port/rest/ali/push_order](http://host:port/rest/ali/push_order)

Data:
```
{
    "order_number": "1234", //账单号
    "order_type": "Order", //账单类型，订单：Order, 钱包充值： Wallet, 预约：  Appointment
    "type": "QRCODE" // QRCODE： PAD端生成支付宝二维码， APP：移动应用调起支付宝支付
}
```

> PAD端拿到 qrCode 字段生成二维码给用户使用支付宝扫码进行支付。
> APP端拿到 orderString后 发给支付宝唤起支付宝支付。

Return:
```
{
    "status_code": 0,
    "data": {
        "qr_code": "https://qr.alipay.com/bax01098eimzy9vigelm00c7" //type是QRCODE时返回
        "order_string":"alipay_sdk=alipay-sdk-java-3.4.27.ALL&app_id=2016092200567241&biz_content=%7B%22body%22%3A%22DEMO%22%2C%22out_trade_no%22%3A%221234%22%2C%22subject%22%3A%22DEMO%22%2C%22timeout_express%22%3A%2230m%22%2C%22total_amount%22%3A%2211.1%22%7D&charset=utf-8&format=json&method=alipay.trade.app.pay&notify_url=%2Frest%2Fpub%2Fali%2Fpay_notify&sign=JP1AxixqyWqz8n4CRNAvkhysh8dCH86fV6oMkftLzRdyZqWIQIHW%2FHWhnwHgw4Xfj4lkwoJFPVCi1pYw0Ef0zFE5PVFBRaABLFQcX3sRB4pO6UDrXvo%2BR8vqFTrnuYwXCS91VxKlU4Fj%2FMa94ZJ4eUtm62qvyqS9wbyGTEaVy9vddjSiEgPS8fAch9V3qNobNYFGC7Mfhi8BjHX1zgONQusR75DnqH4DOywdmarzZFHrtlVBeQg1gI89dyeiLZOthiZ0jsBHxmS4jNxkiw%2BRF7Sr8HDyKV9Ubd0po6rdLsInHtVivom6hVKjzvM1kJkltXIpUZ39jiTTD6iaUy%2B9Bw%3D%3D&sign_type=RSA2&timestamp=2018-11-05+18%3A25%3A16&version=1.0" //type是 APP 时返回
    }
}
```


