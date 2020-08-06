## 打单系统API

### 快递公司列表

GET https://mall.smallsaas.cn/rest/admin/express 

Header: Authorization: token

Return：
```
{
    "status_code": 0,
    "data": [{
        "id": 3,
        "enabled": 1,
        "name": "百世快递",
        "is_default": 1,
        "code": "baishiwuliu"
    }, {
        "id": 1,
        "enabled": 1,
        "name": "天天快递",
        "is_default": 0,
        "code": "tiantian"
    }, {
        "id": 2,
        "enabled": 1,
        "name": "万象物流",
        "is_default": 0,
        "code": "wanxiangwuliu"
    }]
}
```

### 订单列表

GET https://mall.smallsaas.cn/rest/admin/order?status=CONFIRMED_DELIVER_PENDING&status=DELIVERING&started_date=1313432434&end_date=1334453432424&order_number=32432432432&order_number=23432432432 

Param:

 - status - optional, 订单状态，可以同时提供多个值，各个值间是"或"的关系。如果为空，则查询CONFIRMED_DELIVER_PENDING状态的订单。

 - started_date - optional，整数类型， 开始时间

 - end_date - optional, 整数类型， 结束时间

 - order_number - optional， 订单号，可以同时提供多个值，各个值间是"或"的关系。

Header: Authorization: token

Return：
```
{
    "status_code": 0,
    "data": [{
        "detail": "和平区 89652号",
        "phone": "13652698536",
        "is_deliver_reminder": 1,
        "contact_user": "huang",
        "remark": null,
        "invoice": 0,
        "street": null,
        "trade_number": "TEST1467273404816",
        "express_number": null,
        "deal_date": null,
        "express_company": null,
        "city": "天津",
        "id": 299,
        "cover": "http://112.74.26.228:8000/p/c45bb9fda6d985a3be40b40bdb693bb0.jpg",
        "confirm_date": null,
        "description": "超效洁净护理洗衣液2.5L【运费10元】 x 1. ",
        "province": "天津",
        "user_id": 2,
        "express_code": null,
        "district": "和平区",
        "deliver_date": null,
        "delivered_date": null,
        "created_date": "2016-06-30 15:55:40",
        "order_number": "2016063015554024000000201",
        "zip": null,
        "status": "CONFIRMED_DELIVER_PENDING",
        "invoice_title": null,
        "receiving_time": null,
        "deliver_order_number": null,
        "total_price": 44.80,
        "previous_status": null,
        "settled": 0,
        "freight": 10.00,
        "pay_date": "2016-06-30 15:56:44",
        "payment_type": "WECHAT",
        "order_items": [{
            "quantity": 12,
            "product_specification_id": null,
            "weight": 22,
            "product_specification_name": null,
            "product_name": "a",
            "cover": "/p/b06260c587244e867209a5ba374a16ed.jpeg",
            "final_price": 132.00,
            "price": 11.00,
            "product_id": 1,
            "id": 3,
            "bulk": null,
            "order_id": 2,
            "partner_level_zone": 1,
            "barcode": null,
            "store_location": null,
            "status": "CREATED",
            "cost_price": 1.00
          }, {
            "quantity": 21,
            "product_specification_id": 1,
            "weight": 32,
            "product_specification_name": "sfsf",
            "product_name": "b",
            "cover": "/p/39df6836637605a5c86e8aec6ac8a43d.jpeg",
            "final_price": 693.00,
            "price": 33.00,
            "product_id": 2,
            "id": 4,
            "bulk": null,
            "order_id": 2,
            "partner_level_zone": 1,
            "barcode": null,
            "store_location": null,
            "status": "CREATED",
            "cost_price": 22.00
        }]
    }]
}
```

### 批量更新订单发货信息

POST https://mall.smallsaas.cn/rest/admin/deliver 

Header: Authorization: token

Data:
```
[{
    "order_number": "23432432432",
    "express_id": 2,
    "express_number": "23423432432"
}]
```

Return:
```
{
    "message": "order.delivered",
    "status_code": 0
}
```

### 批量完成订单发货

POST https://mall.smallsaas.cn/rest/admin/delivered 

Header: Authorization: token

Data:
```
[{
	"order_number": "23432432432"
}]
```

Return:
```
{
    "message": "order.delivered",
    "status_code": 0
}
```