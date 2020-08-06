## 营销API

### 拼团列表

GET https://mall.smallsaas.cn/rest/piece_group_purchase?pageNumber=1&pageSize=0&masterFree=1 

Param:

 - pageNumber: optional, 页码, default 1

 - pageSize: optional, 每页记录数, default 30

 - masterFree: optional, 是否团长免单 （1列出团长免单的活动 0列出非团长免单活动）

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "pageNumber": 1,
        "pageSize": 30,
        "totalPage": 1,
        "totalRow": 1,
        "list": [{
            "id": 4, //拼团活动id
            "product_id": 1, //拼团活动所关联的产品id
            "payment_type": "POINT|WECHAT",//该拼团活动支持的支付方式。(WECHAT微信支 POINT 积分 若两种都支持，则用"|"分隔。如 WECHAT|POINT）
            "marketing_name": "活动1", //拼团活动名称
            "status": "ONSELL", //拼团活动状态。INIT/ONSELL/OFFSELL/LOCK（LOCK不允许开团，但已开的团仍然生效 （成员仍能加入已开的团） OFFSELL：不允许开团，已开的团若已拼团成功，则继续生效（但成员不能再加入已开的团了），若拼团未成功，则到时间就退款）
            "free_shipping": 0, //是否包邮。 default 1（0 根据产品定义的邮费计算，1 包邮）
            "suggested_price": 1000, //市场价（元）
            "sale": 0, //已团件数
            "min_participator_count": 2, //最小成团人数，default 2
            "duration": 118800, //活动有效时间，单位秒。
            "cover": "http://o9ixtumvv.bkt.clouddn.com/20170510152514628-dssIB8U8.jpg", //活动封面
            "price": 1134, //团购价（元）
            "coupon_usage": 0, //优惠券使用。default 0（0 不能用优惠券；1 可以用专用优惠券；2 可以用系统 优惠券）
            "master_free": 1, //团长是否免单。default 0（0 非免单活动, 1 可以使用免单优惠券）
            "description": null //描述
        }],
        "promoted_master": { //这是随机抽取出来的一位"被推荐"且"已支付"的团长
            "id": 1, //团长id（当团员要入团时，需要指定要加入哪个团长的团，此时用到团长id）
            "product_id": 1, //产品id
            "payment_type": "POINT|WECHAT",//该拼团活动支持的支付方式。(WECHAT微信支付 POINT 积分 若两种都支持，则用"|"分隔。如 WECHAT|POINT）
            "marketing_name": "活动1", //拼团活动名称
            "marketing_short_name": "活动1缩略名",
            "free_shipping": 0, //是否包邮。 default 1（0 根据产品定义的邮费计算，1 包邮）
            "suggested_price": 1000, //市场价（元）
            "piece_group_purchase_status": "ONSELL", //拼团活动状态。INIT/ONSELL/OFFSELL/LOCK（LOCK 不允许开团，但已开的团仍然生效（成员仍能加入已开的团） OFFSELL： 不允许开团，已开的团若已拼团成功，则继续生效（但成员不能再加入已开的团了），若拼团未成功，则到时间就退款）
            "sale": 0, //已团件数
            "min_participator_count": 2, //最小成团人数，default 2
            "user_name": "aaa", //该团长的用户名
            "duration": 118800, //活动有效时间，单位秒
            "cover": "http://o9ixtumvv.bkt.clouddn.com/20170510152514628-dssIB8U8.jpg", //活动封面
            "price": 1134, //团购价（元）
            "coupon_usage": 0, //优惠券使用。default 0（0 不能用优惠券；1 可以用专用优惠券；2 可以用系统 优惠券）
            "master_free": 1, //团长是否免单。default 0（0 非免单活动, 1 可以使用免单优惠券）
            "end_time": "2017-05-12 09:52:28", //结束时间
            "description": null,
            "promoted": 1, //推荐进入活动详情页方便其他用户参团, 0 不推荐, 1 推荐, 当免单开团的时候该团为不推荐,需要团长自己拉人参团
            "start_time": "2017-05-12 09:49:49", //开团时间
            "piece_group_purchase_master_status": "OPENING",//拼团状态（OPENING正在开团/DEAL拼团成功/FAIL拼团失败）
            "member_status": "PAID", //该团长的支付状态（PAID/UNPAID/REFUND）
            "piece_group_purchase_id": 4, //拼团活动id
            "user_id": 2, //该团长的user_id
            "user_avatar": null //该团长的头像
        }
    }
}
```

### 拼团详情

GET https://mall.smallsaas.cn/rest/piece_group_purchase/:id 

Header: Authorization: token

Param:

 - id: required, 活动id

Return：
```
{
"status_code": 0,
    "data": {
        "id": 1,
        "marketing_name": "活动1", //拼团活动名称
        "marketing_short_name": "活动1缩略名",
        "product_id": 1,
        "payment_type": "WECHAT",//该拼团活动支持的支付方式。(WECHAT微信支付 POINT 积分 若两种都支持，则用"|"分隔。如 WECHAT|POINT）
        "status": "ONSELL", //状态。INIT/ONSELL/OFFSELL/LOCK（LOCK不允许开团，但已开的团仍然生效（成员仍能加入已开的团） OFFSELL：不允许开团，已开的团若已拼团成功，则继续生效（但成员不能再加入已开的团了），若拼团未成功，则到时间就退款）
        "min_participator_count": 2, //最小成团人数，default 2
        "price": 50.00, //团购价（元）
        "suggested_price": 233.00, //市场价（元）
        "sale": 0, //已团件数
        "coupon_usage": 1, //优惠券使用。default 0（0 不能用优惠券；1 可以用专用优惠券；2 可以用系统优惠券）
        "cover":"http://o9ixtumvv.bkt.clouddn.com/20170511111002449-3OUYLBt6.jpg", //活动封面
        "duration": 7200, //有效时间，单位秒。比如有效时间为3600秒，某用户在01:00:00开团，则该团的结束时间为02:00:00
        "free_shipping": 0, //是否包邮。 default 1（0 根据产品定义的邮费计算，1 包邮）
        "master_free": 1, //团长是否免单。default 0（0 非免单活动, 1 可以使用免单优惠券）
        "description": null,
        "product": { //参考产品api的说明
            "free_shipping": 0,
            "freight": 0.00,
            "last_modified_date": "2017-05-11 11:09:40",
            "promoted": 0,
            "specifications": [],
            "sales": 0,
            "cover": "http://o9ixtumvv.bkt.clouddn.com/20170511110938953-VIdliaE0.jpg",
            "category_id": 1,
            "price": 233.00,
            "id": 1,
            "sort_order": 100,
            "barcode": null,
            "store_location": null,
            "cost_price": 33.00,
            "covers": ["http://o9ixtumvv.bkt.clouddn.com/20170511110938953-VIdliaE0.jpg"],
            "weight": 33,
            "stock_balance": 1000,
            "brand_id": null,
            "unit": "件",
            "suggested_price": 3333.00,
            "name": "产品1",
            "short_name": "缩略名1",
            "created_date": "2017-05-11 11:09:39",
            "fare_id": 1,
            "bulk": null,
            "partner_level_zone": 1,
            "view_count": 0,
            "status": "ONSELL",
            "description": "产品描述"
        },
        "promoted_masters": [{ //这是由该拼团活动所有"被推荐"且"已支付"的团长组成的列表
            "id": 1, //团长id（当团员要入团时，需要指定要加入哪个团长的团，此时用到团长id）
            "members_count": 2, //目前参团人数
            "paid_members_count": 1, //目前已支付人数
            "status": "OPENING",
            "member_status": "PAID", //该团长的支付状态（PAID/UNPAID/REFUND）
            "end_time": "2017-05-12 20:52:25", //结束时间
            "promoted": 1, //推荐进入活动详情页方便其他用户参团, 0 不推荐, 1 推荐, 当免单开团的时候该团为不推荐,需要团长自己拉人参团
            "start_time": "2017-05-12 18:08:44", //开团时间
            "user_id": 1,
            "user_name": "张三", //团长名
            "user_avatar": null, //团长头像
            "piece_group_purchase_id": 1 //拼团活动id
        },{
            "id": 2,
            "members_count": 2, //目前参团人数
            "paid_members_count": 1, //目前已支付人数
            "status": "OPENING",
            "member_status": "PAID", //该团长的支付状态（PAID/UNPAID/REFUND）
            "end_time": "2017-05-12 11:52:28",
            "promoted": 1,
            "start_time": "2017-05-12 09:49:49",
            "user_id": 2,
            "user_name": "张三", //团长名
            "user_avatar": null, //团长头像
            "piece_group_purchase_id": 1
        }]
    }
}
```

Error Resp
```
{
    "status_code": 1,
    "message": "pieceGroupPurchase.not.found"
}
```

### 我的拼团列表

GET https://mall.smallsaas.cn/rest/my_piece_group_purchase?pageNumber=1&pageSize=10&status=OPENING 

Header: Authorization: token

Param:

 - pageNumber: optional,default 1

 - pageSize: optional,default 30

 - status: optional, 拼团状态（OPENING正在开团/DEAL拼团成功/FAIL拼团失败）

Return:
```
{
    "status_code": 0,
    "data": {
        "pageNumber": 1,
        "pageSize": 30,
        "totalPage": 1,
        "totalRow": 1,
        "list": [{
            "order_number": "order_number1",
            "total_members_count": 2, //拼团成员总数
            "paid_members_count": 1, //已支付的成员总数
            "product_id": 1,
            "status": "PAID", //支付状态（UNPAID未支付/PAID已支付/REFUND已退款）
            "marketing_name": "活动1", //拼团活动名称
            "marketing_short_name": "活动1缩略名",
            "payment_type": "POINT" //该用户支付订单的方式
            "free_shipping": 0, //是否包邮。 default 1（0 根据产品定义的邮费计算，1 包邮）
            "suggested_price": 1000, //市场价（元）
            "piece_group_purchase_status": "ONSELL",//拼团活动状态。INIT/ONSELL/OFFSELL/LOCK （LOCK不允许开团，但已开的团仍然生效（成员仍能加入已开的团） OFFSELL：不允许开 团，已开的团若已拼团成功，则继续生效（但成员不能再加入已开的团了），若拼团未成功，则到时间就退款）
            "sale": 0, //已团件数
            "min_participator_count": 2, //最小成团人数，default 2
            "duration": 118800, //有效时间，单位秒。比如有效时间为3600秒，某用户在01:00:00开团，则该团的结束时间为02:00:00
            "cover":"http://o9ixtumvv.bkt.clouddn.com/20170510152514628-dssIB8U8.jpg", //活动封面
            "price": 1134, //团购价（元）
            "coupon_usage": 0, //优惠券使用。default 0（0 不能用优惠券；1 可以用专用优惠券；2 可以用系统优惠券）
            "master_free": 1, //团长是否免单。default 0（0 非免单活动, 1 可以使用免单优惠券）
            "end_time": "2017-05-12 09:52:25", //结束时间
            "description": null,
            "promoted": 1, //推荐进入活动详情页方便其他用户参团, 0 不推荐, 1 推荐,当免单开团的时候该团为不推荐,需要团长自己拉人参团
            "start_time": "2017-05-10 18:08:44", //开团时间
            "piece_group_purchase_master_status": "OPENING", //拼团状态（OPENING正在开团/DEAL拼团成功/FAIL拼团失败）
            "user_id": 1,
            "piece_group_purchase_id": 4, //拼团活动id
            "created_time": "2017-05-12 11:31:09" //加入该拼团的时间
        }]
    }
}
```

### 我的拼团详情

GET https://mall.smallsaas.cn/rest/my_piece_group_purchase/:id 

Header: Authorization: token

Param:

 - id: required, 拼团活动id

Return Param：

 - 同我的拼团列表API。

Return:
```
{
    "status_code": 0,
    "data": {
        "id": 1,
        "marketing_name": "活动1",
        "marketing_short_name": "活动1缩略名",
        "payment_type": "POINT" //该用户支付订单的方式
        "product_id": 1,
        "piece_group_purchase_status": "ONSELL",
        "min_participator_count": 2,
        "price": 200.00,
        "suggested_price": 233.00,
        "sale": 50,
        "coupon_usage": 1,
        "cover": "http://o9ixtumvv.bkt.clouddn.com/20170511111002449-3OUYLBt6.jpg",
        "duration": 7200,
        "free_shipping": 0,
        "master_free": 1,
        "description": "描述1",
        "start_time": "2017-05-11 12:22:57",
        "end_time": "2017-05-25 12:22:59",
        "piece_group_purchase_id": 1,
        "promoted": 1,
        "piece_group_purchase_master_status": "OPENING",
        "total_members_count": 2,
        "paid_members_count": 1,
        "created_time": "2017-05-10 17:05:07",
        "user_id": 1,
        "order_number": "order_number1",
        "piece_group_purchase_member_status": "PAID",
        "order": { //订单 请参考订单api
            "detail": null,
            "phone": "13155555555",
            "is_deliver_reminder": 0,
            "contact_user": "张三",
            "remark": "备注1",
            "invoice": 0,
            "street": null,
            "trade_number": null,
            "express_number": null,
            "deal_date": null,
            "express_company": null,
            "city": "广州市",
            "id": 1,
            "cover": null,
            "confirm_date": null,
            "description": "描述1",
            "province": "广东省",
            "user_id": 1,
            "coupon_info": null,
            "express_code": null,
            "district": "荔湾区",
            "deliver_date": null,
            "delivered_date": null,
            "created_date": "2017-06-05 15:01:13",
            "order_number": "xxx",
            "zip": null,
            "point_exchange_rate": 100,
            "marketing": null,
            "status": "DELIVERING",
            "invoice_title": null,
            "marketing_description": null,
            "receiving_time": null,
            "deliver_order_number": null,
            "total_price": 1000,
            "previous_status": null,
            "is_deleted": 0,
            "marketing_id": null,
            "settled": 0,
            "freight": 500,
            "pay_date": "2017-06-05 15:01:15",
            "payment_type": "POINT"
        },
    }
}
```

Error Resp 1：
```
{
    "status_code": 1,
    "message": "pieceGroupPurchase.not.found"
}
```

Error Resp 1：
```
{
    "status_code": 1,
    "message": "not.your.pieceGroupPurchase"
}
```

### 团长详情

GET https://mall.smallsaas.cn/rest/piece_group_purchase_master/:id 

Header: Authorization: token

Param:

 - id: 团长id

Return:
```
{
    "status_code": 0,
    "data": {
        "id": 1, //团长id
        "user_id": 1, //团长的user id
        "piece_group_purchase_id": 1, //拼团活动id
        "start_time": "2017-05-27 09:28:19", //创团时间
        "end_time": "2017-05-28 09:28:21", //结束时间
        "promoted": 1, //是否为推荐团长
        "piece_group_purchase_status": "ONSELL", //状态。INIT/ONSELL/OFFSELL/LOCK （LOCK不允许开团，但已开的团仍然生效（成员仍能加入已开的团） OFFSELL：不允许开 团，已开的团若已拼团成功，则继续生效（但成员不能再加入已开的团了），若拼团未成功，则到时间就退款）
        "piece_group_purchase_master_status": "OPENING", //拼团状态（OPENING正在开团/DEAL拼团成功/FAIL拼团失败）
        "marketing_name": "活动1", //拼团活动名称
        "marketing_short_name": "活动1缩略名",
        "min_participator_count": 2, //最小成团人数，default 2
        "price": 800, //团购价（元）
        "suggested_price": 1000, //市场价（元）
        "sale": 0, //已团件数
        "coupon_usage": 0, //优惠券使用。default 0（0 不能用优惠券；1 可以用专用优惠券；2 可以用系统优惠券）
        "cover":"http://o9ixtumvv.bkt.clouddn.com/20170526143343912-37RImHeW.jpg", //活动封面
        "duration": 7200, //有效时间，单位秒。比如有效时间为3600秒，某用户在01:00:00开团，则该团的结束时间为02:00:00
        "free_shipping": 1, //是否包邮。 default 1（0
        根据产品定义的邮费计算，1 包邮）
        "payment_type": "WECHAT", //该拼团活动支持的支付方式。(WECHAT微信支付 POINT 积分 若两种都支持，则用"|"分隔。如 WECHAT|POINT）
        "master_free": 1, //团长是否免单。default 0（0 非免单活动, 1 可以使用免单优惠券）
        "description": null,
        "product": { //参考产品api的说明
            "weight": 10,
            "partner_level_zone": 1,
            "stock_balance": 1000,
            "fare_id": 1,
            "id": 1,
            "cover": "http://o9ixtumvv.bkt.clouddn.com/20170526142339324-YHykFlst.jpg",
            "sales": 0,
            "promoted": 0,
            "name": "产品1",
            "created_date": "2017-05-26 14:23:40",
            "cost_price": 500,
            "status": "ONSELL",
            "free_shipping": 0,
            "brand_id": null,
            "category_id": 1,
            "suggested_price": 2000,
            "barcode": null,
            "short_name": "缩略名1",
            "bulk": null,
            "specifications": [],
            "unit": "个",
            "last_modified_date": "2017-05-26 14:23:42",
            "price": 1000,
            "covers": [
                "http://o9ixtumvv.bkt.clouddn.com/20170526142339324-YHykFlst.jpg"
            ],
            "freight": 0,
            "store_location": null,
            "sort_order": 100,
            "view_count": 0,
            "description": "产品描述"
        }
    }
}
```

### 开团

POST https://mall.smallsaas.cn/rest/order 

>参考 下单前计算优惠信息 api 返回的优惠券，选择一个优惠劵进行下单。到支付宝支付时，把order-number的值赋给out_trade_no进行支付。
微信支付 - WECHAT
积分支付 - POINT

Header: Authorization: token

Data:
```
{
    //这两个是 "新建订单api" 新增的域
    "marketing": "PIECE-GROUP", //required。开团必须是PIECE-GROUP
    "order_items": [{
    "product_id": 1,
    "product_specification_id": 1,
    "quantity": 2,
    "marketing_id": 1, //required。拼团活动的ID, 即piece_group_purchase的id
    }
    ...其他需要提供的域同"新建订单api"
}
```

Return: 同"新建订单api"

### 参团

POST https://mall.smallsaas.cn/rest/order 

> 参考 下单前计算优惠信息 api 返回的优惠券，选择一个优惠劵进行下单。到支付宝支付时，把order-number的值赋给out_trade_no进行支付。
微信支付 - WECHAT
积分支付 - POINT

Header: Authorization: token

Data:
```
{
    //这两个是 "新建订单api" 新增的域
    "marketing": "PIECE-GROUP-JOINT", //required。参团必须是 PIECE-GROUP-JOINT
    "order_items": [{
        "product_id": 1,
        "product_specification_id": 1,
        "quantity": 2,
        "marketing_id": 1, //required。所参加拼团的团长ID, 即piece_group_purchase_master的id
    }
    ...其他需要提供的域同"新建订单api"
}
```

Return: 同"新建订单api"

### 批发类别列表

GET https://mall.smallsaas.cn/rest/wholesale_category 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "contact": { //用户默认配送地区
            "id": 1,
            "zip": null,
            "detail": null,
            "phone": "1234567",
            "contact_user": "张三",
            "street": null,
            "province": "广东",
            "is_default": 1,
            "street_number": null,
            "user_id": 1,
            "district": "荔湾区",
            "city": "广州"
        },
        "categories": [{
            "id": 2,
            "name": "批发类别2", //类别名
            "sort_order": 5 //排序，小的在前面
        },{
            "id": 1,
            "name": "批发类别1",
            "sort_order": 100
        }]
    }
}
```

### 批发列表

GET https://mall.smallsaas.cn/rest/wholesale?categoryId=1 

> Tips：如果用户没有设置默认配送地区，则此api不返回批发列表。如果有设置，则只返回配送到用户的默认配送地区的批发列表。

Header: Authorization: token

Param:

 - categoryId: optional, 批发活动类别id （如提供则列出该类别的批发活动）

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
        "pageSize": 10,
        "list": [{
            "category_id": 1,
            "cover": "http://o9ixtumvv.bkt.clouddn.com/20170525151147892-Koka1giH.jpg", //批发活动封面
            "sale": 0, //已售个数
            "product": { //参考产品api
                "free_shipping": 0,
                "freight": 0.00,
                "last_modified_date": "2017-05-25 15:09:29",
                "promoted": 0,
                "specifications": [{ //产品规格列表
                "price": 10000.00,
                "suggested_price": 20000.00,
                "product_id": 1,
                "name": "红色",
                "weight": 20,
                "id": 1,
                "bulk": 0,
                "stock_balance": 1000,
                "cost_price": 100.00
        	}, {
            "price": 3000.00,
            "suggested_price": 10000.00,
            "product_id": 1,
            "name": "银色",
            "weight": 10,
            "id": 2,
            "bulk": 0,
            "stock_balance": 1000,
            "cost_price": 100.00
        	}],
            "sales": 0,
            "cover":"http://o9ixtumvv.bkt.clouddn.com/20170525103606389-6Vu95yiR.jpg", //产品默认的封面图
            "price": 1000.00,
            "id": 1,
            "sort_order": 100,
            "barcode": null,
            "store_location": null,
            "cost_price": 10.00,
            "covers":[
                "http://o9ixtumvv.bkt.clouddn.com/20170525153019061-qsQ1cWAF.jpg",
                "http://o9ixtumvv.bkt.clouddn.com/20170525153019363-kLyFRGJS.jpg"
            ], //产品的封面图列表
            "weight": 200,
            "stock_balance": 1000,
            "brand_id": null,
            "unit": "台",
            "suggested_price": 2000.00,
            "name": "诺基亚",
            "short_name": "诺基亚缩略名",
            "created_date": "2017-05-25 10:36:06",
            "fare_id": 1,
            "bulk": null,
            "partner_level_zone": 1,
            "view_count": 0,
            "status": "ONSELL"
            },
            "pricing": { //与用户默认配送地区相匹配的价格项
                "suggested_retail_price": 22,
                "region": "辽宁",
                "id": 8,
                "enabled": 1,
                "price": 11,
                "is_default": 0,
                "wholesale_id": 1,
                "suggested_wholesale_price": 44
            },
            "product_id": 1, //产品id
            "marketing_name": "批发1", //批发活动名称
            "marketing_short_name": "活动1缩略名",
            "description": "机会难得！！！", //描述
            "id": 1,
            "status": "ONSELL" //状态。INIT/ONSELL/OFFSELL
            "settlement_proportion": 30, //分成比例
            "agent_proportion": 20, //代理分成比例
            "unit": 件 //单位
        }]
    }
}
```

### 批发详情

GET https://mall.smallsaas.cn/rest/wholesale/:id 

> Tips：如果用户没有设置默认配送地区，则此api不返回指定的批发详情。

Param:

 - id: required,批发活动id

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "category_id": 1,
        "cover": "http://o9ixtumvv.bkt.clouddn.com/20170525151147892-Koka1giH.jpg", //批发活动封面
        "sale": 0, //已售个数
            "pricings": [{ //价格列表。不同地区的批发价格不同。1.is_default为1的价格项表示该价格适合于所有地区（不含专门设置的地区）enabled若为1，则所有地区都配送（除去is_default为0且enabled为0的价格项; enabled若为0，则所有地区都不配送（除去is_default为0且enabled为1的价格项）2.is_default为0的价格项表示专门设置的地区对应的价格（优先于默认价格项）, enabled若为1，则覆盖默认价格项；enabled若为0，则该地区不配送 3.某些地区不设置，则不配送到该地区。例如: pricings的返回结果为空数组[]，则表示 所有地区都不配送。
            "region": null,
            "id": 47,
            "price": 900,
            "is_default": 1,
            "enabled": 1,
            "wholesale_id": 1,
            "suggested_retail_price": 1000,
            "suggested_whole_price": 800,
        },{
            "region": "江苏-苏州|江苏-南通",
            "id": 48,
            "price": 1100,
            "is_default": 0,
            "enabled": 0,
            "wholesale_id": 1,
            "suggested_retail_price": 850, //产品在该地区的线下建议零售价
            "suggested_whole_price": 800 //产品在该地区的星级经销价
        }],
        "product": [{ //参考产品api
            "free_shipping": 0,
            "freight": 0.00,
            "last_modified_date": "2017-05-25 15:30:19",
            "promoted": 0,
            "specifications": [{
            "price": 10000.00,
            "suggested_price": 20000.00,
            "product_id": 1,
            "name": "红色",
            "weight": 20,
            "id": 1,
            "bulk": 0,
            "stock_balance": 1000,
            "cost_price": 100.00
        }, {
            "price": 3000.00,
            "suggested_price": 10000.00,
            "product_id": 1,
            "name": "银色",
            "weight": 10,
            "id": 2,
            "bulk": 0,
            "stock_balance": 1000,
            "cost_price": 100.00
        }],
        "sales": 0,
        "cover": "http://o9ixtumvv.bkt.clouddn.com/20170525153019061-qsQ1cWAF.jpg",
        "category_id": 1,
        "price": 1000.00,
        "id": 1,
        "sort_order": 100,
        "barcode": null,
        "store_location": null,
        "cost_price": 10.00,
        "covers":[
            "http://o9ixtumvv.bkt.clouddn.com/20170525153019061-qsQ1cWAF.jpg",
            "http://o9ixtumvv.bkt.clouddn.com/20170525153019363-kLyFRGJS.jpg"
        ],
        "weight": 200,
        "stock_balance": 1000,
        "brand_id": null,
        "unit": "台",
        "suggested_price": 2000.00,
        "name": "诺基亚",
        "short_name": "诺基亚缩略名",
        "created_date": "2017-05-25 10:36:06",
        "fare_id": 1,
        "bulk": null,
        "partner_level_zone": 1,
        "view_count": 0,
        "status": "ONSELL"
        },
        "pricing": { //与用户默认配送地区相匹配的价格项
            "suggested_retail_price": 22,
            "region": "辽宁",
            "id": 8,
            "enabled": 1,
            "price": 11,
            "is_default": 0,
            "wholesale_id": 1,
            "suggested_wholesale_price": 44
        },
        "product_id": 1, //产品id
        "marketing_name": "批发1", //批发活动名称
        "marketing_short_name": "批发1缩略名",
        "description": "<p>机会难得！！！<br\></p>", //描述
        "id": 1, //活动id
        "status": "ONSELL" //活动状态（INIT/ONSELL/OFFSELL）,
        "settlement_proportion": 30, //分成比例
        "agent_proportion": 44, //代理分成比例
        "proportionLv1": 24, //下级线下皇冠批发产品时的分成比例 = 分成比例*下级线下皇冠分成比例
        "proportionLv2": 6, //下下级线下皇冠批发产品时的分成比例 = 分成比例*下下级线下皇冠分成比例
        "unit": 件 //单位
    }
}
```

### 新建批发订单

POST https://mall.smallsaas.cn/rest/order 

> 参考 下单前计算优惠信息 api 返回的优惠券，选择一个优惠劵进行下单。到支付宝支付时，把order-number的值赋给out_trade_no进行支付。
微信支付 - WECHAT
积分支付 - POINT

Header: Authorization: token

Data:
```
{
//这两个是 "新建订单api" 新增的域
"marketing": "WHOLESALE", //required。新建批发订单必须是WHOLESALE
"order_items": [{
"product_id": 1,
"product_specification_id": 1,
"quantity": 2,
"marketing_id": 1, //required。批发活动的ID, 即wholesale的id
}
...其他需要提供的域同"新建订单api"
}
```
Return: 同"新建订单api"

### 试用装列表

GET https://mall.smallsaas.cn/rest/trial 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "short_note": "洗发水试用",
        "note": null,
        "end_time": null,
        "shipping_type": 0,
        "index": 100,
        "version": 1,
        "enabled": 1,
        "cover": "http://o9ixtumvv.bkt.clouddn.com/20180709182906045-hyEDbt5L.jpeg",
        "start_time": null,
        "payment_type": null,
        "price": 0,
        "product_id": 335,
        "name": "洗发水试用-免费",
        "id": 1,
        "partaken": true //已经参加过
    }]
}
```

### 试用装详情

GET https://mall.smallsaas.cn/rest/trial/:id 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "short_note": "洗发水试用",
        "note": null,
        "product": {
            "free_shipping": 0,
            "freight": 0,
            "last_modified_date": "2016-12-22 10:10:36",
            "mid": null,
            "promoted": 1,
            "sales": 9,
            "cover": "http://images.10mup.com/20161104102243958-v499XJvA.jpg",
            "category_id": 83,
            "price": 12.9,
            "sku_name": null,
            "id": 335,
            "sort_order": 1,
            "barcode": "6903148126660",
            "store_location": null,
            "cost_price": 10.21,
            "weight": 500,
            "sku_id": null,
            "stock_balance": 13,
            "brand_id": null,
            "unit": "瓶",
            "suggested_price": 20,
            "name": "REJOICE飘柔家庭护理芦荟长效止痒滋润洗发露400ML",
            "bar_code": null,
            "short_name": "止痒滋润洗发露",
            "created_date": "2016-10-07 14:11:51",
            "fare_id": 4,
            "bulk": 0,
            "partner_level_zone": 1,
            "sku_code": null,
            "view_count": 2172,
            "status": "ONSELL"
        },
        "end_time": null,
        "shipping_type": 0,
        "index": 100,
        "version": 2,
        "enabled": 1,
        "cover": "http://o9ixtumvv.bkt.clouddn.com/20180709182906045-hyEDbt5L.jpeg",
        "start_time": null,
        "payment_type": null,
        "price": 0,
        "product_id": 335,
        "name": "洗发水试用-免费",
        "id": 1,
        "partaken": true,
        "covers": [{
            "product_id": 335,
            "id": 1298,
            "type": 0,
            "sort_order": 1,
            "url": "http://images.10mup.com/20161104102243958-v499XJvA.jpg"
        },{
            "product_id": 335,
            "id": 1299,
            "type": 0,
            "sort_order": 2,
            "url": "http://images.10mup.com/20161104102242227-T17IgsG8.jpg"
        },{
            "product_id": 335,
            "id": 1300,
            "type": 0,
            "sort_order": 3,
            "url": "http://images.10mup.com/20161104102241687-lfedAC1r.jpg"
        }]
    }
}
```

### 新建试用装申请订单

POST https://mall.smallsaas.cn/rest/order 

Header: Authorization: token

Data:
```
{
    //这两个是 "新建订单api" 新增的域
    "marketing": "TRIAL", //required。新建试用装订单必须是TRIAL
    "order_items": [{
        "product_id": 1, // 该试用装的产品ID
        "product_specification_id": 1, //规格号，如果有就带上
        "quantity": 1, //数量，必须是1
        "marketing_id": 1, //required。批发活动的ID, 即trial的id
    }
    ...其他需要提供的域同"新建订单api"
}
```

Return: 同"新建订单api"

### 我的试用装申请列表

GET https://mall.smallsaas.cn/rest/trial/application?pageNumber=1&pageSize=30 

Header: Authorization: token

```
public static enum Status {
    APPLYING, //申请中
    AUDITING, //审核中
    DELIVERING, //发货中
    DELIVERED, //已发货
    REJECTED //未获得试用资格
}
```

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
            "cover": "http://o9ixtumvv.bkt.clouddn.com/20180709182906045-hyEDbt5L.jpeg",
            "trial_id": 1,
            "created_time": "2018-08-06 17:27:21",
            "note": null,
            "user_id": 11080,
            "order_number": "18080617272155711080",
            "shipping_type": 0,
            "name": "洗发水试用-免费",
            "id": 1,
            "order_id": 3288,
            "version": 1,
            "status": "AUDITING"
        }]
    }
}
```