## 产品API

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

### 获取产品类别列表

GET https://mall.smallsaas.cn/rest/product_category?promoted=true 

Param:

 - promoted: optional, 如果指定该参数，则在一级类别下面返回类别该类别 products（包括它子类别）下的推荐产品列表。

Describe:

 - is_show_products: 点击类别时是否进入该类别下第1个产品的详情页（1 是 0 否）

 - weight: 重量，单位克

 - bulk: 体积

Return:
```json
{
	"status_code": 0,
	"data": [{
		"id": 1,
			"cover": null,
			"sub_categories": [{
			"id": 2,
			"cover":"https://mall.smallsaas.cn/p/fb61f7180cb48a0d1bcff2a4edab9780.png",
			"sub_categories": [],
			"description": null,
			"name": "瓶装2.5L",
			"parent_id": 1
		}, {
			"id": 5,
			"cover":"https://mall.smallsaas.cn/p/aa92d03568a42607011ca55815d48368.png",
			"sub_categories": [],
			"description": null,
			"name": "旅行装(袋)",
			"parent_id": 1
		}],
			"description": null,
			"name": "超效洁净",
			"parent_id": null,
			"is_show_products": 1,
			"products": [{ 
				"free_shipping": 0,
				"freight": 0.00,
				"last_modified_date": "2016-10-10 19:51:55",
				"promoted": 1,
				"stock_balance": 1000,
				"sales": 0,
				"cover":"http://o9ixtumvv.bkt.clouddn.com/20161010195121988-gFvkrsAZ.jpeg",
				"unit": "a",
				"category_id": 3,
				"price": 33.00,
				"suggested_price": 33.00,
				"name": "aaaa",
				"short_name": "aa",
				"id": 1,
				"created_date": "2016-10-10 19:51:23",
				"fare_id": 1,
				"sort_order": 100,
				"partner_level_zone": 1,
				"barcode": null,
				"view_count": 0,
				"store_location": null,
				"status": "ONSELL",
				"cost_price": 33.00,
				"weight": 500, 
				"bulk": 100 
			}]
		}, {
			"id": 3,
			"cover": null,
			"sub_categories": [],
			"description": null,
			"name": "亮白增艳",
			"parent_id": null
		}, {
		"id": 4,
		"cover": null,
		"sub_categories": [],
		"description": null,
		"name": "活氧清洁剂",
		"parent_id": null
	}]
}
```

### 获取某类别下的产品列表

只列出 ONSELL 状态的产品

GET https://mall.smallsaas.cn/rest/product_category/id?pageNumber=1&pageSize=50&orderByDesc=view_count&orderBy=price&orderBy=sales&promoted=true

Param:

 - pageNumber: 当前页，默认1

 - pageSize: 每页记录数，默认50

 - orderBy: 排序列。如果同时指定了超过1个orderBy，则前者优先于后者

 - orderByDesc: 倒序排序列。如果同时指定了orderBy和orderByDesc，则orderBy优先于orderByDesc；

 - orderBy and orderByDesc 可以用的值有： view_count : 人气， price: 价格， sales: 销量

 - promoted: optional, 如果指定该参数，则分页查询该类别下的推荐产品。

Describe:

 - id: 类别ID，如果指定-1 则返回所有产品

 - is_show_products: 点击类别时是否进入该类别下第1个产品的详情页（1 是 0 否）

 - weight: 重量, 单位克

 - bulk: 体积

Return:
```json
{
	"status_code": 0,
	"data": {
		"id": 2,
		"cover":"https://mall.smallsaas.cn/p/fb61f7180cb48a0d1bcff2a4edab9780.png",
		"description": null,
		"name": "瓶装2.5L",
		"is_show_products": 1,
		"products": [{
			"created_date": "2016-04-22 09:30:53",
			"cost_price": 20.00,
			"status": "ONSELL",
			"free_shipping": 1,
			"origin": "广东",
			"suggested_price": 50.00,
			"category_id": 2,
			"stock_balance": 10000,
			"id": 1,
			"unit": "件",
			"cover":"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
			"last_modified_date": "2016-04-23 12:27:59",
			"price": 34.80,
			"category_name": "瓶装2.5L",
			"promoted": 1,
			"sales": 0,
			"name": "超效洁净护理洗衣液2.5L【全国包邮】",
			"freight": 0.00,
			"brand": "大地",
			"sort_order": 100,
			"weight": 500, 
			"bulk": 200 
		}, {
			"created_date": "2016-04-22 11:16:14",
			"cost_price": 70.00,
			"status": "ONSELL",
			"free_shipping": 1,
			"origin": "广州",
			"suggested_price": 88.00,
			"category_id": 2,
			"stock_balance": 600,
			"id": 3,
			"unit": "件",
			"cover":"https://mall.smallsaas.cn/p/2b3edeb3c3ca2a12b06893cb12286710.png",
			"last_modified_date": "2016-04-22 14:22:04",
			"price": 69.60,
			"category_name": "瓶装2.5L",
			"promoted": 0,
			"sales": 0,
			"name": "超效洁净护理洗衣液2.5Lx2瓶【全国包邮】",
			"freight": 0.00,
			"brand": "大陆",
			"sort_order": 100,
			"weight": 500, 
			"bulk": 200 
		}],
		"parent_id": 1
	}
}
```

### 产品热门关键字

GET https://mall.smallsaas.cn/rest/product_hit_word 

Return:
```json
{
	"status_code": 0,
	"data": [{
		"id": 1,
		"hit": 0,
		"name": "皂液"
	}]
}
```

### 产品搜索

GET https://mall.smallsaas.cn/rest/product_search?pageNumber=1&pageSize=20&name=abc&barCode=234234&orderByDesc=view_count&orderBy=price&orderBy=sales 

Param: 

 - pageNumber: 当前页，默认1

 - pageSize: 每页记录数，默认50

 - name: 产品名称

 - barCode: 条形码

 - orderBy: 排序列

 - orderByDesc: 倒序排序列

 - orderBy and orderByDesc 可以用的值有： view_count: 人气， price: 价格， sales: 销量

Describe:

 - weight: 重量, 单位克

 - bulk: 体积

Return:
```json
{
	"status_code": 0,
	"data":[{
		"created_date": "2016-04-22 09:30:53",
		"cost_price": 20.00,
		"status": "ONSELL",
		"free_shipping": 1,
		"origin": "广东",
		"suggested_price": 50.00,
		"category_id": 2,
		"stock_balance": 10000,
		"id": 1,
		"unit": "件",
		"cover":"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
		"last_modified_date": "2016-04-23 12:27:59",
		"price": 34.80,
		"category_name": "瓶装2.5L",
		"promoted": 1,
		"sales": 0,
		"name": "超效洁净护理洗衣液2.5L【全国包邮】",
		"short_name": "aa",
		"freight": 0.00,
		"brand": "大地",
		"sort_order": 100,
		"weight": 500,
		"bulk": 200 
	}, {
		"created_date": "2016-04-22 11:16:14",
		"cost_price": 70.00,
		"status": "ONSELL",
		"free_shipping": 1,
		"origin": "广州",
		"suggested_price": 88.00,
		"category_id": 2,
		"stock_balance": 600,
		"id": 3,
		"unit": "件",
		"cover":"https://mall.smallsaas.cn/p/2b3edeb3c3ca2a12b06893cb12286710.png",
		"last_modified_date": "2016-04-22 14:22:04",
		"price": 69.60,
		"category_name": "瓶装2.5L",
		"promoted": 0,
		"sales": 0,
		"name": "超效洁净护理洗衣液2.5Lx2瓶【全国包邮】",
		"freight": 0.00,
		"brand": "大陆",
		"sort_order": 100,
		"weight": 500, 
		"bulk": 200 
	}]
}
```

### 获取所有产品列表

只列出 ONSELL 状态的产品

GET https://mall.smallsaas.cn/rest/product?all=true 

Param： 

 - all: true 时查询所有产品列表。其他参数会忽略。

 - allow_coupon: 是否可以使用优惠券 0:不可以， 1:可以用

 - credit: 可用积分数量

Describe:

 - weight: 重量, 单位克

 - bulk: 体积

Data:
```json
{
	"status_code": 0,
	"data": [{
		"created_date": "2016-04-22 09:30:53",
		"cost_price": 20.00,
		"status": "ONSELL",
		"free_shipping": 1,
		"origin": "广东",
		"suggested_price": 50.00,
		"category_id": 2,
		"stock_balance": 10000,
		"id": 1,
		"unit": "件",
		"cover":"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
		"last_modified_date": "2016-04-23 12:27:59",
		"price": 34.80,
		"category_name": "瓶装2.5L",
		"promoted": 1,
		"sales": 0,
		"name": "超效洁净护理洗衣液2.5L【全国包邮】",
		"freight": 0.00,
		"brand": "大地",
		"sort_order": 100,
		"weight": 500, 
		"bulk": 200, 
		"allow_coupon": 0, 
		"credit": 0, 
	}]

}
```

### 获取推荐产品列表

只列出 ONSELL 状态的产品

GET https://mall.smallsaas.cn/rest/product?pageNumber=1&pageSize=50&zone=1 

Param:

 - pageNumber: optional, 当前页，默认1

 - pageSize: optional, 每页记录数，默认50

 - zone: optional, 零元区／精品区／特价区 查询。如果不带这个参数，那么就查推荐产品。 零元区: 1， 精品区: 2， 特价区: 3

 - orderBy: 排序列

 - orderByDesc: 倒序排序列

 - orderBy and orderByDesc 可以用的值有: view_count: 人气， price: 价格, sales: 销量
 
Describe:

 - weight: 重量, 单位克

 - bulk: 体积

Retrun:
```json
{
	"status_code": 0,
	"data": [{
		"created_date": "2016-04-22 09:30:53",
		"cost_price": 20.00,
		"status": "ONSELL",
		"free_shipping": 1,
		"origin": "广东",
		"suggested_price": 50.00,
		"category_id": 2,
		"stock_balance": 10000,
		"id": 1,
		"unit": "件",
		"cover":"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
		"last_modified_date": "2016-04-23 12:27:59",
		"price": 34.80,
		"category_name": "瓶装2.5L",
		"promoted": 1,
		"sales": 0,
		"name": "超效洁净护理洗衣液2.5L【全国包邮】",
		"freight": 0.00,
		"brand": "大地",
		"sort_order": 100,
		"weight": 500, 
		"bulk": 200
	}]
}
```

### 查看产品详情

GET https://mall.smallsaas.cn/rest/product/id 

Describe:

 - weight: 重量, 单位克

 - bulk: 体积

 - specifications: 产品规格，当购买产品时，弹出来的框提供的选择项。加入购物车和购买时需要把选择的项提交给后台，具体参考购物车和下单api的要求

 - price: 售价

 - name: 规格名称

 - stock_balance: 库存

 - is_incl_postage_by_if: 条件包邮

 - is_incl_postage： 包邮

 - incl_postage_provisoes: 返回的 条件包邮信息

 - amount: 满多少包邮

 - region: 限制地区使用这个运费

 - first_amount: 首费

 - second_amount: 续费

 - is_default: 没有满足地区，使用这个默认运费

Retrun:
```json
{
	"status_code": 0,
	"data": {
		"created_date": "2016-04-22 09:30:53",
		"cost_price": 20.00,
		"status": "ONSELL",
		"free_shipping": 1,
		"origin": "广东",
		"suggested_price": 50.00,
		"category_id": 2,
		"stock_balance": 10000,
		"id": 1,
		"unit": "件",
		"cover":"https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
		"last_modified_date": "2016-04-23 18:26:39",
		"price": 34.80,
		"promoted": 1,
		"sales": 0,
		"description": "\<h1\>超优惠\<br/\>\</h1\>\<p\>\<img src=\\"/upload/upload/image/20160601/1464767352927011775.png\\" title=\\"1464767352927011775.png\\" alt=\\"logo.png\\"/\>\</p\>\<p\>\<br/\>\</p\>",
		"name": "超效洁净护理洗衣液2.5L【全国包邮】",
		"freight": 0.00,
		"images": [],
		"brand": "大地",
		"sort_order": 100,
		"weight": 500, 
		"bulk": 200, 
		"properties": [{
			"value_type": "STRING",
			"product_id": 1,
			"id": 1,
			"property_value": "a1",
			"display_name": "a1",
			"property_id": 1
		}, {
			"value_type": "STRING",
			"product_id": 1,
			"id": 2,
			"property_value": "a2",
			"display_name": "a2",
			"property_id": 2
		}],
		"covers": [{
			"product_id": 1,
			"id": 1,
			"type": 0,
			"url":"http://localhost:9990/p/6255a9dd831b89aa92ec1df49054603a.jpeg"
		}, {
			"product_id": 1,
			"id": 2,
			"type": 0,
			"url":"http://localhost:9990/p/3b316bb6c6b939eb64c36d047a6c9d6e.jpg"
		}],
		"specifications":[{
			"price": 140, 
			"suggested_price": 140,
			"product_id": 1,
			"name": "a2", 
			"id": 1,
			"stock_balance": 1000,
			"cost_price": 100,
			"weight": 500, 
			"bulk": 200 
			}, {
			"price": 120,
			"suggested_price": 130,
			"product_id": 1,
			"name": "a1",
			"id": 2,
			"stock_balance": 1000,
			"cost_price": 90,
			"weight": 500, 
			"bulk": 200 
		}],
		"fare_template": {
			"is_incl_postage_by_if": 0, 
			"dispatch_time": "24",
			"is_incl_postage": 1, 
			"name": "包邮",
			"title": "［省钱优惠］",
			"content": "满3KG更省钱哦。",
			"shop_addr": "广东-广州",
			"last_modified_date": "2016-08-31 10:56:16",
			"id": 1,
			"valuation_model": 0,
			"incl_postage_provisoes": [{ 
				"amount": 100.00, 
				"bulk_no": null,
				"carry_way": 0,
				"id": 2,
				"fare_id": 2,
				"region": null,
				"type": 3,
				"piece_no": null,
				"weight_no": null
			}],
			"carry_modes": [{
				"second_piece": 1,
				"second_amount": 0.00,
				"first_bulk": null,
				"carry_way": 0,
				"is_default": 0,
				"first_piece": 1,
				"first_weight": null,
				"second_bulk": null,
				"second_weight": null,
				"id": 3,
				"fare_id": 2,
				"region": "广东-广州\|广东-深圳", 
				"first_amount": 8.00
			}, {
				"second_piece": 1,
				"second_amount": 0.00, 
				"first_bulk": null,
				"carry_way": 0,
				"is_default": 1, 
				"first_piece": 1,
				"first_weight": null,
				"second_bulk": null,
				"second_weight": null,
				"id": 2,
				"fare_id": 2,
				"region": null,
				"first_amount": 10.00 
			}],
		},
		"purchase_strategy": {
			"id": 1,
			"name": "关注公众号且限购1件",
			"description": "请先关注公众号，关注后可以购买1件。"
		}
	}
}
```
