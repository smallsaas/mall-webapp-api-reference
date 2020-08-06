## 优惠券API

### 分享订单拿优惠券

POST https://mall.smallsaas.cn/rest/order_share

只有CLOSED_CONFIRMED的订单才可以分享。

Header: Authorization: token

Data：
```
{
	"order_number": "2343243242"
}
```

Return:
```
{
	"status_code": 1,
	"data": {
		"code": "wrwfafef",
		//分享code，用这个code去构建分享到朋友圈时的链接的参数。
		"order_number": "2343243242"
	}
}
```

### 优惠券列表

GET https://mall.smallsaas.cn/rest/coupon?status=ACTIVATION&pageNumber=1&pageSize=10 

Header: Authorization: token

Param： 

 - status - optional, 状态， 默认返回 ACTIVATION 状态的。

 - pageNumber - optional, 分页页数

 - pageSize - optional, 每页记录数

状态类型：
```
public enum Status {
    NON_ACTIVATION, //未激活
    ACTIVATION, //已激活
    OVERDUE, //已过期
    USED //已使用
}
```

Return:

> 如果discount不是0，那么就是折扣券，比如"discount": 60, 表示打六折。
> 如果money不是0， 那么就是代金券。
```
{
    "status_code": 0,
    "data": {
        "ACTIVATION": 1,
        "USED": 0,
        "NON_ACTIVATION": 1,
        "OVERDUE": 0,
        "coupons": [{
            "code": "9e0f38da-8a05-4243-a338-c1d373b2943d",
            "discount": 0,
            "description": null,
            "type": "ORDER",
            "display_name": "a",
            "cond": " <rule-set name="getFinalPrice" \> <mvel-rule id="step1" multipleTimes="false" xexclusive="true" valid="true"\> <condition\><![CDATA[true]]\></condition> <action><![CDATA[finalPrice=totalPrice-4]]\></action\> </mvel-rule> </rule-set> ",
            "valid_date": "2017-01-13 18:01:44",
            "money": 4,
            "user_id": 1,
            "name": "q",
            "id": 1,
            "created_date": "2017-01-11 18:01:44",
            "attribute": "{"source":"SYSTEM"}",
            "auto_give": 0,
            "status": "ACTIVATION"
        }]
    }
}
```

### 点击分享链接领取优惠券

POST https://mall.smallsaas.cn/rest/coupon 

Header: Authorization: token

> 用户须关注公众号才可以激活优惠券。

Data:
```
{
	"code": "werwqerweqfaf" //分享码
}
```

Success Return:
```
{
    "status_code": 0,
    "data": {
        "coupon_taken_records": [ //该分享被领取的记录
        {
            "share_id": 1,
            "user_id": 1,
            "name": "Administrator",
            "created_date": "2016-11-28 10:43:08",
            "message": "又有券可用了。",
            "coupon_value": 6
        }
        ],
        "coupons": [//该用户领取的优惠券列表，对于第一次点击链接领取时才有这个属性。
        {
            "code": "1982dbcf-442a-4111-923f-6b20b67eb31e",
            "description": null,
            "type": "ORDER",
            "display_name": "式",
            "valid_date": "2016-12-01",
            "money": 4,
            "user_id": 1,
            "name": "aaaa",
            "created_date": "2016-11-28",
            "id": 1,
            "status": "ACTIVATION"
        },
        {
            "code": "0d0cf6c8-58c4-4df7-91e3-a14e74046b97",
            "description": null,
            "type": "ORDER",
            "display_name": "33",
            "valid_date": "2016-12-02",
            "money": 2,
            "user_id": 1,
            "name": "发啊发",
            "created_date": "2016-11-28",
            "id": 2,
            "status": "ACTIVATION"
        }
        ],
        "coupon_value": 6 //领取的优惠券价值
    }
}
```

### 激活优惠券

PUT https://mall.smallsaas.cn/rest/coupon/id 

> 领取（激活）优惠券, 用户须关注公众号才可以激活优惠券。

Param:

 - id - integer, 优惠券ID

Header: Authorization: token

Data:
```
{
	"status": "ACTIVATION"
}
```

Failure Retrun：
```
{
    "status_code": 1,
    "message": "user.must.be.followed"
}
```

Success Return:
```
{
    "status_code": 0,
    "message": "activate.success"
}
```

### 删除优惠券

DELETE https://mall.smallsaas.cn/rest/coupon/id 

Param:

 - id - integer, 优惠券ID

Header: Authorization: token

Success Returm:
```
{
    "status_code": 0,
    "message": "delete.success"
}
```

### 用户优惠券通知

GET https://mall.smallsaas.cn/rest/coupon_notify 

>如果还没通知过用户，那么首页可以弹出红包框。
如果 'has_unread_coupon' 为true，那么需要对'个人中心，优惠券'
添加红点 提示用户。
notify为总开关，只有notify为true时才需要弹出红包。
当notify为true时：
如果new_user为true，则显示'新用户红包'，否则就是显示'恭喜您获得X张优惠券'。
如果is_user_followed为true，则显示点击关注领取， 否则显示点击查看。

Header: Authorization: token

Success Return:
```
{
    "status_code": 1,
    "data": {
        "notify": true, //需要弹出红包通知用户
        "new_user": true, //是否是新注册用户
        "coupon_count": 2, //当notify为true时才返回
        "coupon_value": 34, //当notify为true时才返回
        "is_user_followed": true, //用户是否关注公众号
        "has_unread_coupon": true, //表示用户有未读优惠券,这时'个人中心'需要显示红点
        "activation_coupons": [{
            "id": 1,
            "name": "拼团免单券",
            "type": "MARKETING_PIECE_GROUP", //类型为MARKETING_PIECE_GROUP表示拼团券
            "status": "ACTIVATION"
        }]
    }
}
```

### 下单前计算优惠信息

POST https://mall.smallsaas.cn/rest/coupon_calculation?phone=13800000001 

Param:

 - phone - optional， 用户手机号，查询该用户的优惠券优惠信息,pad端用传入订单的产品和价格列表，返回该用户的优惠券对这个订单优惠后的信息

Header: Authorization: token

Data:
```
[{
    "product_id": 1,
    "price": 20 //该产品的总价格，注意：不是单价，比如买啦2件，那这里的值应该是单价＊2
},{
    "product_id": 2,
    "price": 39.9
}]
```

Return:
```
[{
    "coupon_id": 1,
    "coupon_name": "全单8折",
    "valid_date"："2016-11-30 11:11:11", //有效时间
    "final_price": 47.92 //这个订单使用这个优惠劵后的总价格
},{
    "coupon_id": 2,
    "coupon_name": "单品买立减8元",
    "valid_date"："2016-11-30 11:11:11", //有效时间
    "final_price": 51.9
},{
    "coupon_id": 3,
    "coupon_name": "满50立减5元",
    "valid_date"："2016-11-30 11:11:11", //有效时间
    "final_price": 55.9
}]
```

### 查看我的优惠券分享信息

GET https://mall.smallsaas.cn/rest/coupon_share 

> 下单完成后用户对红包进行了分享，这个api可以查看分享过的列表。

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "valid_date": "2016-12-06 12:18:43",
        "code": "e58a9055-f966-4b59-b36d-b8de66bbfc25",
        "user_id": 1,
        "order_number": "12345",
        "share_date": "2016-12-01 12:18:43",
        "link":"http://www.kequandian.net/app/app/coupon?share_code=e58a9055-f966-4b59-b36d-b8de66bbfc25&invite_code=a1b2c3",
        "id": 1
    }]
}
```

### 优惠券类型列表

GET https://mall.smallsaas.cn/rest/admin/coupon_type 

Return:

### 后台赠送优惠券

POST https://mall.smallsaas.cn/rest/admin/coupon 

Data:
```
{
    "phone": "1390000000",
    "couponTypeIds": [ 1, 2, 3 ]
}
```

Return:
```
{
    "status_code": 1,
    "message": "ok"
}
```

