## 前端地址
 - [微信公众号前端代码(基于angular)](https://github.com/kequandian/mall-wxa-alliance)
 - [标准小程序代码](https://github.com/kequandian/mall-wxa-starter)

## API

### [用户API](./用户api.md)

### [商城API](./商城api.md)

### [产品API](./产品api.md)

### [订单API](./订单api.md)

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
