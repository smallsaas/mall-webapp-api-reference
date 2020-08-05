## 运费计算API

### 运费计算

POST https://mall.smallsaas.cn/rest/product_carriage 

Data:
```
{
    "delivery_type": "EXPRESS", //可选项：EXPRESS, SELF_PICK, FLASH, 默认EXPRESS
    "province": "广东",
    "city": "广州",
    "data":[{
        "fare_id": 1,
        "price": 23.20,
        "quantity": 4,
        "weight": 500, //该产品的重量，从product可以拿到，单位是g
        "bulk": 100 //该产品的体积， 可以忽略
    }]
}
```

Return:
```
{
    "status_code": 0,
    "data": {
        "carriage": 4.00, //运费
        "message": "付同样的运费,还可以拼单0.30KG哦.",
        "delta": -180.00 //可忽略。距离满包邮的差额。注意：这是一个负数。只有是负数时才表示离满包邮有差额。
    }
}
```

### 查询产品限购

GET https://mall.smallsaas.cn/rest/product_purchase_strategy?productId=234&quantity=2 

Param:
 - productId: 产品ID

 - quantity: 购买数量

Header: Authorization: token

可以购买，Return:
```
{
    "status_code": 0,
    "message": "ok"
}
```

限购了， 不能购买，Return:
```
{
    "status_code": 1,
    "message": "超出购买限额, 限购2件, 你过去10天内已购买过1件. "
}
```