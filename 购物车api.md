## 购物车API

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

### 添加到购物车

POST https://mall.smallsaas.cn/rest/shopping_cart?increase=false 

> 如果已存在，则更新，如果quantity是0，则删除。

Param::

 - increase: optional, default true.
> 如果为true则累加购物车数量，为false则替换数量。

Header: Authorization: token

Data:
```
[{
"product_id": 1,
"quantity": 1,
"product_specification_id": 1, //optional, 选择的产品规格ID
"marketing_id": 1, //optional 营销活动id
"marketing": "WHOLESALE" //optional 营销活动(一般是批发WHOLESALE,团购是直接下单的）
}, { //非批发产品不需要提供 marketing_id 和 marketing 字段
"product_id": 3,
"quantity": 1
}]
```

Return 购物车列表:
```
{
    "status_code": 0,
    "data": [{
        "created_date": "2016-04-25 19:15:45",
        "id": 3,
        "cover": "https://mall.smallsaas.cn/p/516c02b5e8ceb745b6dd61b6e77b3e17.png",
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
        "cover": "https://mall.smallsaas.cn/p/2b3edeb3c3ca2a12b06893cb12286710.png",
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
```

### 删除购物车

### 清空购物车

DELETE https://mall.smallsaas.cn/rest/shopping_cart 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": "shopping_cart.delete.success"
}
```