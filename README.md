## 前端地址
 - [微信公众号前端代码(基于angular)](https://github.com/kequandian/mall-wxa-alliance)
 - [标准小程序代码](https://github.com/kequandian/mall-wxa-starter)

## API

 - [用户API](./用户api.md)

 - [产品API](./产品api.md)

 - [订单API](./订单api.md)

 - [物流API](./物流api.md)

 - [购物车API](./购物车api.md)

 - [收货地址API](./收货地址api.md)

 - [运费计算API](./运费计算api.md)

 - [佣金API](./佣金api.md)

 - [分销API](./分销api.md)

 - [会员API](./会员api.md)

 - [优惠券API](./优惠券api.md)

 - [钱包API](./钱包api.md)

 - [营销API](./营销api.md)

 - [收藏宝贝API](./收藏宝贝api.md))

 - [打单系统API](./打单系统api.md)

 - [支付API](./支付api.md)

 - [其它配置API](./其它配置api.md)

### 获取商城全局配置项

GET https://mall.smallsaas.cn/rest/global_config

Return:
```json
{
	"status_code": 0,
	"data": {
		"point_exchange_rate": 100,
		"auto_select_coupon": false,
		"drawing_condition": 100
	}
}
```
