## 收藏宝贝API

### 返回收藏宝贝列表

GET https://mall.smallsaas.cn/rest/product_favorite?pageNumber=1&pageSize=20 

Param:

 - pageNumber - optional, 页数

 - pageSize - optional, 每页记录数

Header: Authorization: token

Return：
```
{
    "status_code": 0,
    "data": [{
        "id": 1,
        "user_id": 1,
        "product_id": 1,
        "collect_date": "2016-05-18 16:52:15",
        "category_id": 1,
        "name": p1,
        "cover": imag/xx.png,
        "brand": ,
        "origin":,
        "stock_balance":,
        "sales":,
        "description":,
        "status":,
        "created_date":,
        "last_modified_date":,
        "unit":,
        "price":,
        "cost_price":,
        "suggested_price":,
        "promoted":,
        "freight":,
        "free_shipping":,
        "sort_order":;
    }]
}
```

### 添加收藏宝贝

POST https://mall.smallsaas.cn/rest/product_favorite 

Header: Authorization: token
Data:
```
{
	"product_id": 1
}
```

Return：
```
{
    "status_code": 0,
    "message": "product.favorite.created",
}
```

Error Return:
```
{
    "message": "invalid.input.json",
    "status_code": 1
}
```

### 删除收藏宝贝

DELETE https://mall.smallsaas.cn/rest/product_favorite/id 

Header: Authorization: token

Param:

 - id: 商品id

Return：
```
{
    "message": "product.favorite.deleted",
    "status_code": 0
}
```

Error Return:
```
{
    "message": "no.such.product.favorite",
    "status_code": 1
}
```