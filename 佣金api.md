## 佣金API

### 查看提现账号信息

GET https://mall.smallsaas.cn/rest/withdraw_account 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "id": 1,
        "bank_name": null,
        "owner_name": "Mr.A",
        "account": "234234234324",
        "user_id": 1,
        "type": "ALIPAY"
    }]
}
```

### 添加提现账号信息

POST https://mall.smallsaas.cn/rest/withdraw_account 

Header: Authorization: token

Type:
```
public enum Type {
    ALIPAY, //支付宝
    WECHAT, //微信
    BANK //银行
}
```

Data:
```
{
    "owner_name": "Mr.A",
    "type": "ALIPAY",
    "account": "234234234324",
    "bank_name":"中国工商银行科韵路支行" //当type为BANK时需要
}
```

Return:
```
{
    "message": "withdraw.account.created",
    "status_code": 0
}
```

### 删除提现账号信息

DELETE https://mall.smallsaas.cn/rest/withdraw_account/id 

Header: Authorization: token

Param:

 - id: 账户ID

Return:
```
{
    "message": "withdraw.account.deleted",
    "status_code": 0
}
```
### 查看余额

GET https://mall.smallsaas.cn/rest/owner_balance 

Header: Authorization: token

Success Return:
```
{
    "status_code": 0,
    "data": {
        "total_reward": 8, //总提成
        "balance": 2, //可用余额
        "is_agent": true, //是否是代理商
        "is_seller": true, //是否是销售商
        "is_partner": true, //是否是经销商
        "is_crown": true, //是否皇冠
        "is_crown_ship_temp": true, //是否为临时皇冠，临时皇冠不能进入线下门店
        "is_physical": true, //是否线下资格
        "is_copartner": true, //是否合伙人
        "partner_pool_count": 9, //合伙人池人数
        "partner_level": { //如果不是经销商，那么就为null
            "id": 1,
            "level": 1, //表示该经销商的级别，1表示一星
            "headcount_quota": 3,
            "name": "一星经销商"
        },
        "next_partner_level": { //如果没有下一级，那么就为null
            "id": 2,
            "level": 2, //下一级别
            "headcount_quota": 3, //下一星的人数
            "name": "二星经销商"
    	},
    }，
    "msg"://如果是临时线下皇冠商，则会出现//此提示
}
```

### 申请提现

POST https://mall.smallsaas.cn/rest/owner_balance 

Header: Authorization: token

Data:
```
{
    "withdraw_type": "Wallet", // optional, wallet为提现到零钱帐户
    "withdraw_account_id": 1, // optional, 账户ID
    "withdraw_cash": 100.00 //提现金額
}
```

Success Return:
```
{
    "message": "apply.success",
    "status_code": 1
}
```

Failure Return:
```
{
    "message": "apply.failure",
    "status_code": 1
}
```

### 查看提现历史记录

GET https://mall.smallsaas.cn/rest/reward_cash 

Param:

 - page_number: optional, 页码，default 1;

- -page_size: optional, 每页记录数，default 30;

- -start_date: optional, 开始时间， default 上个月;

- -end_date: optional, 结束时间， default 今天。

Header: Authorization: token

状态：
```
public enum Status {
    APPLYING,
    REJECTED,
    HANDLING,
    COMPLETED
}
```

Return:
```
{
    "status_code": 0,
    "data": [{
        "id": 2,
        "apply_time": "2016-06-16 13:23:39",
        "bank_name": null,
        "account_number": "oXauMwcMqGeV6zdHGL_1CcmjlQUg",
        "status": "APPLYING",
        "name": "Jacky.D.H",
        "cash": 100,
        "owner_id": 62,
        "complete_time": null,
        "reject_time": null,
        "account_name": "Jacky.D.H",
        "account_type": "WECHAT"
    }]
}
```

### 查看分成订单汇总信息

GET https://mall.smallsaas.cn/rest/order_item_reward 

Header: Authorization: token

Param:

 - page_number: optional, 页数
 - page_size: optional, 每页记录数
 - start_date: optional, 开始时间
 - end_date: optional, 结束时间

> 备: 默认查当月的数据。

分成类型：
```
public enum Type {
    SELLER, //分销商
    AGENT, //代理商
    PLATFORM,//平台
    PARTNER //合伙人
}
```

拥金状态：
```
public enum State {
    PENDING_SETTLEMENT, //待结算
    SETTLED, //已结算， 只有已结算的拥金才会有余额里体现
    REFUNDED //已退款， 表示该订单已发生退货退款，本分成无效。
}
```

Return:
```
{
    "status_code": 0,
    "data": {
        "order_item_rewards": [{
            "reward": 2,
            "created_time": "2016-06-05 11:11:22",
            "level": 1, //结合type一起使用，表示参与分成时的级别，比如type=SELLER,level=1, 表示作为一级分销商参与分成
            "owner_id": 1,
            "order_number": "1234567890", //订单号
            "order_profit": 20, //整个订单项的利润,页面不应显示出来
            "settled_time": null,
            "type": "AGENT", //分成的角色，AGENT：作为代理商分成
            "percent": 10, //分成比例，前端ignore，页面不应显示出来
            "withdrawn_time": null,
            "product_name": "A", //产品名称
            "product_price": 20.00, //产品价格
            "product_quantity": 1, //产品数量
            "order_item_id": 1,
            "cover": "/assets/img/find_user.png", //产品图片
            "name": "Administrator",
            "id": 4,
            "state": "SETTLED", //分成状态
            "order_id": 1,
            "payment_type": "WECHAT",
            "point_exchange_rate": 100
        },{
            "reward": 2,
            "created_time": "2016-06-05 11:11:22",
            "level": 3,
            "owner_id": 1,
            "order_number": "1234567890",
            "order_profit": 20,
            "settled_time": null,
            "type": "PARTNER",
            "percent": null,
            "withdrawn_time": null,
            "product_name": "A",
            "order_item_id": 1,
            "cover": "/assets/img/find_user.png",
            "name": "Administrator",
            "id": 3,
            "state": "PENDING_SETTLEMENT",
            "order_id": 1,
            "payment_type": "WECHAT",
            "point_exchange_rate": 100
        },{
            "reward": 2,
            "created_time": "2016-06-05 11:11:22",
            "level": 1,
            "owner_id": 1,
            "order_number": "1234567890",
            "order_profit": 20,
            "settled_time": null,
            "type": "SELLER",
            "percent": 10,
            "withdrawn_time": null,
            "product_name": "A",
            "order_item_id": 1,
            "cover": "/assets/img/find_user.png",
            "name": "Administrator",
            "id": 2,
            "state": "PENDING_SETTLEMENT",
            "order_id": 1,
            "payment_type": "WECHAT",
            "point_exchange_rate": 100
        },{
            "reward": 2,
            "created_time": "2016-06-05 11:11:22",
            "level": null,
            "owner_id": 1,
            "order_number": "1234567890",
            "order_profit": 20,
            "settled_time": null,
            "type": "SELF",
            "percent": 10,
            "withdrawn_time": null,
            "product_name": "A",
            "order_item_id": 1,
            "cover": "/assets/img/find_user.png",
            "name": "Administrator",
            "id": 1,
            "state": "PENDING_SETTLEMENT",
            "order_id": 1,
            "payment_type": "WECHAT",
            "point_exchange_rate": 100
        }],
        "pending_reward": 6,
        "settled_reward": 2,
        "total_order_count": 2,
        "settled_order_count": 1,
        "pending_order_count": 1
    }
}
```

### 查看产品分成

GET https://mall.smallsaas.cn/rest/product_settlement?id=product-id&marketingType=type&marketingId=id

Header: Authorization: token

Param:

 - id: integer,required, 产品ID

 - marketingType: string, optional, 营销活动类型，如拼团为PIECE-GROUP

 - marketingId: integer, optinal, 营销活动ID

Return:
```
{
    "status_code": 0,
    "data": 30.00
}
```