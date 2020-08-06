## 分销API

### 我的分销商层次信息

GET https://mall.smallsaas.cn/rest/seller_level 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "result": true,
        "levels": [2, 1, 0], //各级的分销商总数
        "max_level": 3 //三级分销
    }
}
```

### 我的分销商信息

GET https://mall.smallsaas.cn/rest/seller 

Header: Authorization: token

> 返回下一级的朋友

Return:
```
{
    "status_code": 0,
    "data": {
        "id": 1,
        "user_name": "Administrator",
        "partner_id": null, //合伙人ID
        "level": 1,
        "partner_ship": 1, //是否是合伙人
        "partner_pool_count": 9, //合伙人池人数
        "seller_ship_time": "2016-04-28 13:08:35", //成为分销商时间
        "partner_ship_time": "2016-04-28 13:08:35", //成为合伙人时间
        "user_id": 1,
        "seller_ship": 1, //是否是分销商
        "parent_id": null,
        "followed": 1, //是否关注公众号
        "follow_time": "2016-05-06 12:00:00", //关注时间
        "unfollowed_children_count": 0, //未关注的下级总数
        "followed_children_count": 0, //已关注的下级总数
        "agent_ship": 1, //是否是代理商
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
        "children": [{
            "seller_ship_time": null,
            "level": 2, //没用，忽略
            "partner_ship_time": null,
            "user_name": "abc", //用户名
            "avatar": null, //头像URL
            "sa_level": 1,//属于该分销商的第几级分销商.只有type=all时才有这个属性。
            "partner_id": null,
            "user_id": 3,
            "partner_ship": 0,
            "parent_id": 1,
            "id": 3,
            "seller_id": 3,
            "seller_ship": 0,
            "followed": 1, //是否关注公众号
            "follow_time": "2016-05-06 12:00:00", //关注时间
            "agent_ship": 1, //是否是代理商
            "register_date": "2018-10-11", //注册时间
            "grade": "1" // VIP系统的会员级别ID
        }, {
            "seller_ship_time": null,
            "level": 2,
            "partner_ship_time": null,
            "user_name": "xyz",
            "avatar": null,
            "sa_level": 1,
            "partner_id": null,
            "user_id": 9,
            "partner_ship": 0,
            "parent_id": 1,
            "id": 9,
            "seller_id": 9,
            "seller_ship": 0,
            "followed": 1, //是否关注公众号
            "follow_time": "2016-05-06 12:00:00", //关注时间
            "agent_ship": 0 //是否是代理商
        }, {
            "seller_ship_time": null,
            "level": 3,
            "partner_ship_time": null,
            "user_name": "a",
            "avatar": null,
            "sa_level": 2,
            "partner_id": null,
            "user_id": 4,
            "partner_ship": 0,
            "parent_id": 3,
            "id": 4,
            "seller_id": 4,
            "seller_ship": 0,
            "followed": 1, //是否关注公众号
            "follow_time": "2016-05-06 12:00:00", //关注时间
            "agent_ship": 0 //是否是代理商
        }, {
            "seller_ship_time": null,
            "level": 3,
            "partner_ship_time": null,
            "user_name": "b",
            "avatar": null,
            "sa_level": 2,
            "partner_id": null,
            "user_id": 5,
            "partner_ship": 0,
            "parent_id": 3,
            "id": 5,
            "seller_id": 5,
            "seller_ship": 0,
            "followed": 1, //是否关注公众号
            "follow_time": "2016-05-06 12:00:00", //关注时间
            "agent_ship": 1 //是否是代理商
        }]
    }
}
```

### 下级分销商信息

GET https://mall.smallsaas.cn/rest/seller/seller_id 

Header: Authorization: token

Param:
 - seller_id: 下级分销商ID

Return:
```
{
    "status_code": 0,
    "data": {
        "id": 2,
        "user_name": "a",
        "partner_id": 1,
        "level": 2,
        "partner_ship": 0,
        "seller_ship_time": null,
        "partner_ship_time": null,
        "followed": 1, //是否关注公众号
        "follow_time": "2016-05-06 12:00:00", //关注时间
        "children": [{
        "id": 4,
        "user_name": "a1",
        "partner_id": 1,
        "level": 3,
        "partner_ship": 0,
        "seller_ship_time": null,
        "partner_ship_time": null,
        "user_id": 4,
        "seller_ship": 0,
        "parent_id": 2,
        "followed": 1, //是否关注公众号
        "follow_time": "2016-05-06 12:00:00" //关注时间
    }, {
        "id": 5,
        "user_name": "a2",
        "partner_id": 1,
        "level": 3,
        "partner_ship": 0,
        "seller_ship_time": null,
        "partner_ship_time": null,
        "user_id": 5,
        "seller_ship": 0,
        "parent_id": 2,
        "followed": 1, //是否关注公众号
        "follow_time": "2016-05-06 12:00:00"//关注时间
    }],
    "user_id": 2,
    "seller_ship": 0,
    "parent_id": 1
    }
}
```

### 申请成为分销商

POST https://mall.smallsaas.cn/rest/seller 

Header: Authorization: token

> 申请成为皇冠商时的前提：申请成为皇冠商开关已打开

Data:
```
{
    "real_name": "Huang",
    "phone": "1308888899",
    "type": "CROWN" //申请类型，默认不填则为申请 分销商 资格。CROWN为申请线下皇冠商资格。
}
```

Return:
```
{
    "status_code": 0,
    "data": {
    	"seller_ship": 1
    }
}
```

### 以扫码方式申请成为某皇冠商的"线下经销商"或"线下皇冠商"

POST https://mall.smallsaas.cn/rest/physical_seller 

Header: Authorization: token

> 成为皇冠商前提：以扫码方式申请成为皇冠商的开关已经打开

> Tips:
1.若申请人是一个Seller，申请内容是线下经销商，则递交成为线下经销商的申请
2.若申请人本身是一个线下经销商，申请内容是皇冠商，此时会根据自动审核皇冠商机制来自动给予皇冠商资格
3.若申请人是一个Seller,申请内容是线下皇冠，此时会先申请成为线下并自动通过，然后申请成为皇冠，根据自动审核皇冠商机制来自动给予皇冠商资格

Data:
```
{
    "uid": "U00001", //required,推荐人的UID
    "real_name": "黄", //required,申请人真实姓名，用于更新个人信息
    "phone": "13800000000", //required,申请人手机，用于更新个人信息
    "type": "CROWN", //optional，省略表示申请成为线下经销商，CROWN表示申请成为线下皇冠商
    "province": "广东", //required
    "city": "广州", //required
    "district": "荔湾区" //required
}
```

Success Return:
```
{
    "status_code": 0,
    "message": "apply.success"
}
```

Error Return:
```
{
    "status_code": 1,
    "message": "user.is.not.crownship"
}

{
    "status_code": 1,
    "message": "invalid.user"
}

{
    "status_code": 1,
    "message": "invalid.phone"
}

{
    "status_code": 1,
    "message": "cannot.apply.yourself"
}
```

### 线下经销商查看线下信息

GET https://mall.smallsaas.cn/rest/physical_seller 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "parent_seller_id": null,
        "parent": null,
        "city": null,
        "children_count": 2, //physical_seller_children_count, physical_seller_children 只有具 //有皇冠商资格时才返回。
        "user_name": "Administrator",
        "total_settled_amount": 0,
        "avatar": null,
        "uid": "U00000001",
        "province": null,
        "total_amount": 0,
        "children": [], //星级经销商下线列表
        "crown_children": [ //皇冠商下线列表（包含下级和下下级皇冠商）
        {
            "parent_seller_id": 1,
            "city": null,
            "level": 1, //1.下级皇冠商 2.下下级皇冠商
            "user_name": "user123",
            "total_settled_amount": 0,
            "crown_ship": 1,
            "real_name": "user123",
            "avatar": null,
            "followed": 1,
            "uid": "U011707251055190003",
            "follow_time": null,
            "province": null,
            "total_amount": 0,
            "phone": null,
            "district": null,
            "latest_bonus_date": null,
            "id": 182,
            "created_date": "2017-09-19 10:59:06",
            "seller_id": 11014
        },{
            "parent_seller_id": 11014,
            "city": null,
            "level": 2,
            "user_name": "关应康",
            "total_settled_amount": 0,
            "crown_ship": 1,
            "real_name": null,
            "avatar":"http://wx.qlogo.cn/mmopen/vi_32/AWrNt30IeSoibiaaicZafBbkw39icOzMibCfDSMhQH9uRYxRLQMzUp4hJBHtvYMZn9FwXMkpibM47C0OW94nJU0lyOjw/0",
            "followed": 1,
            "uid": "U011707271136230002",
            "follow_time": null,
            "province": null,
            "total_amount": 0,
            "phone": null,
            "district": null,
            "latest_bonus_date": null,
            "id": 181,
            "created_date": "2017-09-19 10:58:36",
            "seller_id": 11019
        }],
        "district": null,
        "crown_children_count": 1,//只有具有皇冠商资格时才返回。下级皇冠商数量
        "crown_children_count_lv2": 1, // 只有具有皇冠商资格时才返回。下下级皇冠商数量
        "latest_bonus_date": null,
        "id": 179,
        "created_date": "2017-08-09 12:03:07",
        "seller_id": 1
    }
}
```

### 线下皇冠商查看进货结算明细

GET https://mall.smallsaas.cn/rest/physical_purchase_summary?month=2017-06 

Param:

 - month: optional, 要查询的月份，格式yyyy-MM,如果不传该参数，则返回所有月份的记录，用于'结算记录'UI。如果传了参数，则返回该月的明细，用于'我的推荐'UI。

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "transferred": 0, //是否已转积分系统
        "statistic_month": "2017-09-01", //统计月份
        "monthly_amount": 5600, //本月进货
        "total_settled_amount": 848, //累计总提成. 当有month参数时才返回该项
        "monthly_settled_amount": 848, //提成金额
        "monthly_expected_settled_amount": 0, //上级期望提成（前端用不到）
        "monthly_expected_settled_amount_lv2": 0,//上上级期望提成（前端用不到）
        "my_recommended_sellers": [ //我的推荐线下经销商.当有month参数时才返回该项（包含两级，下级排前面，下下级排//后面）
        {
            "transferred": 0,
            "level": 1, //1.下级 2.下下级
            "user_name": "user123",
            "statistic_month": "2017-09-01",
            "monthly_amount": 3200,
            "avatar": null,
            "monthly_settled_amount": 960,
            "monthly_expected_settled_amount_lv2": 0,
            "uid": "U011707251055190003",
            "transferred_amount": 0,
            "monthly_expected_settled_amount": 728,
            "settlement_proportion": 100,
            "id": 192,
            "seller_id": 11014
        },
        {
            "transferred": 0,
            "level": 2,
            "user_name": "关应康",
            "statistic_month": "2017-09-01",
            "monthly_amount": 6000,
            "avatar":"http://wx.qlogo.cn/mmopen/vi_32/AWrNt30IeSoibiaaicZafBbkw39icOzMibCfDSMhQH9uRYxRLQMzUp4hJBHtvYMZn9FwXMkpibM47C0OW94nJU0lyOjw/0",
            "monthly_settled_amount": 0,
            "monthly_expected_settled_amount_lv2": 120,
            "uid": "U011707271136230002",
            "transferred_amount": 0,
            "monthly_expected_settled_amount": 960,
            "settlement_proportion": 100,
            "id": 191,
            "seller_id": 11019
        }
        ],
        "transferred_amount": 0,
        "total_amount": 5600,
        "settlement_proportion": 100,
        "id": 193,
        "seller_id": 1
        }
    ]
}
```

### 线下代理商查看进货结算明细

GET https://mall.smallsaas.cn/rest/agent_summary?month=2017-08 

Param:

 - month: optional, 要查询的月份，格式yyyy-MM,如果不传该参数，则返回所有月份的记录，用于'结算记录'UI。如果传了参数，则返回该月的明细。

Header: Authorization: token

>Tips:
1.对于每个线下代理，其最后一次生成年终奖的时间假设为2016-08-04，则程序会于2017-08-04生成他的年终奖（如果从来未生成过年终奖，则把他成为线下的日期作为最后一次生成年终奖时间）。
因此在2017-08-04之前访问此api将会看不到由2016-08-04\~2017-08-04的年终奖。
2.为简单起见，只有生成年终奖的月份才会看到年终奖。

Return:
```
{
    "status_code": 0,
    "data": [{
        "amount": 2600, //进货额
        "transferred": 0, //是否已转积分系统
        "pcd_name": "广东", //地区名称
        "bonus": { //年终奖金
        "settled_amount": 11969,
        "amount": 23938,
        "transferred": 0,
        "transferred_amount": 0,
        "statistic_month": "2017-07-25",
        "pcd_id": 2147,
        "year_statistic_amount": 0, //奖金项没有"年累计订单额"
        "settlement_proportion": 50,
        "id": 19,
        "end_month": "2018-07-25",//代表从statistic_month到end_month的年终奖金
        "seller_id": 11014
    },
        "statistic_month": "2017-10-01", //开始月份
        "pcd_id": 2147,
        "year_statistic_amount": 2600, //年累计订单额
        "settled_amount": 7.8, //提成额
        "transferred_amount": 0, //已转积分
        "agentPurchaseJournals": [ //根据产品，提成比例来汇总的订单明细
        {
            "sum_settled_amount": 6, //本月提成
            "sum_final_price": 2000, //进货金额
            "product_id": 149, //产品id
            "agent_proportion_percentage": "0.30", //提成比例（0.30表示0.30%）
            "product_name": "碧丽雅超效洁净手洗专用洗衣液1.25L\*10瓶/箱"//产品名称
        },{
            "sum_settled_amount": 12,
            "sum_final_price": 4000,
            "product_id": 673,
            "agent_proportion_percentage": "0.30",
            "product_name": "十美优品净澈水润型沐浴露600ml\*4瓶/箱"
        },{
            "sum_settled_amount": 1.3,
            "sum_final_price": 432,
            "product_id": 675,
            "agent_proportion_percentage": "0.30",
            "product_name": "十美优品滋养修护型护发素600ml\*4瓶/箱"
        }],
            "settlement_proportion": 0, //提成比例
            "id": 39,
            "end_month": null, //结束月份
            "seller_id": 11014
        },{
        "amount": 2600,
        "transferred": 0,
        "pcd_name": "广东-广州",
        "bonus": {
            "settled_amount": 212.16,
            "amount": 10608,
            "transferred": 0,
            "transferred_amount": 0,
            "statistic_month": "2017-07-25",
            "pcd_id": 2148,
            "year_statistic_amount": 0,
            "settlement_proportion": 2,
            "id": 22,
            "end_month": "2018-07-25",
            "seller_id": 11014
        },
        "statistic_month": "2017-10-01",
        "pcd_id": 2148,
        "year_statistic_amount": 2600,
        "settled_amount": 7.8,
        "transferred_amount": 0,
        "agentPurchaseJournals": [{
            "order_user_id": 11019,
            "agent_proportion": 3,
            "quantity": 20,
            "pcd_name": "广州",
            "pcd_id": 2148,
            "product_specification_name": null,
            "product_name": "十美优品净澈水润型沐浴露600ml\*4瓶/箱",
            "order_item_id": 5529,
            "settled_amount": 4.8,
            "order_user_name": "关应康",
            "final_price": 1600,
            "price": 80,
            "product_id": 673,
            "percentage": 10,
            "marketing_name": "十美优品净澈水润型沐浴露600ml\*4瓶/箱",
            "marketing_id": 14,
            "id": 7,
            "create_date": "2017-10-09 11:21:34",
            "seller_id": 11014,
            "product_cover": "http://images.10mup.com/20170708154457918-gkpUE7r4.jpg"
        },{
            "order_user_id": 11019,
            "agent_proportion": 3,
            "quantity": 10,
            "pcd_name": "广州",
            "pcd_id": 2148,
            "product_specification_name": null,
            "product_name": "碧丽雅超效洁净手洗专用洗衣液1.25L\*10瓶/箱",
            "order_item_id": 5530,
            "settled_amount": 3,
            "order_user_name": "关应康",
            "final_price": 1000,
            "price": 100,
            "product_id": 149,
            "percentage": 10,
            "marketing_name": "碧丽雅超效洁净手洗专用洗衣液1.25L\*10瓶/箱",
            "marketing_id": 11,
            "id": 8,
            "create_date": "2017-10-09 11:21:34",
            "seller_id": 11014,
            "product_cover": "http://images.10mup.com/20160914142106802-oFWNcqv1.jpg"
        }],
        "settlement_proportion": 0,
        "id": 42,
        "end_month": null,
        "seller_id": 11014
    }]
}
```

### 线下代理商查看年终奖励对照表

GET https://mall.smallsaas.cn/rest/physical_agent_bonus?pcd_id=1 

Param:

 - pcd_id: required，地区id

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "id": 1,
        "percentage": 10, //奖金比例 （当min_amount<销售额<=max_amount
        ，应用此percentage）
        "min_amount": 0, //销售额下限
        "max_amount": 1000, //销售额上限
        "pcd_id": 1
    },{
        "id": 2,
        "percentage": 20,
        "min_amount": 1000,
        "max_amount": -1, //-1表示无上限
        "pcd_id": 1
    }]
}
```

### 线下皇冠商查看被推荐人的进货明细列表

GET https://mall.smallsaas.cn/rest/physical_

Param:

 - seller_id: required，被推荐人的seller_id

 - month: optional，省略则列出所有月份的进货明细，格式为yyyy-MM

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "order_number": "123456xxx", //订单号
        "created_date": "2017-06-12 13:53:00",
        "amount": 1000, //进货额（不是指该订单的进货额，而是该订单其中1个订单项的进货额）
        "id": 2,
        "order_item_id": 1, //订单项id
        "product_name": "油条", //产品名称
        "seller_id": 2, //被推荐人的seller_id（即传过来的）
        "order_id": 1, //订单id
        "product_settlement_proportion": 20, //产品提成比例
        "expected_reward": 30, //预期提成金额，不是真正的提成金额
        "note": null
    },{
        "order_number": "123456xxx",
        "created_date": "2017-06-12 13:53:20",
        "amount": 3000,
        "id": 1,
        "order_item_id": 2,
        "product_name": "飞机",
        "seller_id": 2,
        "order_id": 1,
        "product_settlement_proportion": 30,
        "expected_reward": 50,
        "note": null
    }]
}
```

### 线下分成比例对照表

GET https://mall.smallsaas.cn/rest/physical_proportion 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "id": 1,
        "percentage": 2, //分成比例（%）
        "min_amount": 1000, //最小进货额
        "max_amount": 5000 //最大进货额
    },{
        "id": 2,
        "percentage": 5,
        "min_amount": 5001,
        "max_amount": 10000
    },{
        "id": 3,
        "percentage": 6,
        "min_amount": 10001,
        "max_amount": 50000
    },{
        "id": 4,
        "percentage": 8,
        "min_amount": 50001,
        "max_amount": -1
    }]
}
```

### 皇冠经销商,星级经销商申请需知

GET https://mall.smallsaas.cn/rest/physical_apply_tips?type=CROWN 

Param:

 - type: required，（CROWN 皇冠经销商， STAR星级经销商, ANNOUNCE线下门店系统公告)

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "created_date": null,
        "content": "<p\>内容。。。。</p\>",
        "type": "CROWN",
        "id": 1,
        "enabled": 1, //是否启用
        "last_modified_date": "2017-06-23 12:26:50", //最后一次的修改时间
        "name": "皇冠需知"
    }
}
```

### 申请成为合伙人

POST https://mall.smallsaas.cn/rest/copartner 

Header: Authorization: token

Data:
```
{
    "phone": "13900000001",
    "name": "黄小二",
    "address": "广东广州荔湾区周门路16号"
}
```

Success Return:
```
{
    "status_code": 0,
    "message": "ok"
}
```

Failure Return:
```
{
    "status_code": 1,
    "message": "already.copartner"
}
```

### 合伙人查看团队列表

GET https://mall.smallsaas.cn/rest/copartner 

Header: Authorization: token

Success Return:
```
{
    "status_code": 0,
    "data": {
        "create_time": "2018-08-23 11:52:14",
        "children_count": 1,
        "children": [{
            "uid": "U011808231159370001",
            "follow_time": null,
            "create_time": "2018-08-23 12:32:15",
            "phone": "13800000000",
            "user_name": "13922112131",
            "real_name": "黄",
            "avatar": null,
            "followed": 0,
            "seller_id": 3
        }],
        "id": 2,
        "seller_id": 2,
        "status": "NORMAL"
    }
}
```

Failure Return:
```
{
    "status_code": 1,
    "message": "not.a.copartner"
}
```

### 合伙人查看分成

GET https://mall.smallsaas.cn/rest/copartner_settlement?month=2018-08 

Header: Authorization: token

Success Return:
```
{
    "status_code": 0,
    "data": {
        "settlement_proportion": 4, //分成比例
        "total_settlement_amount": 0, //总分成
        "total_amount": 0, //总进货量
        "monthly_amount": 0, //当月进货量
        "monthly_settlement_amount": 0, //当月提成
        "create_time": "2018-08-23 11:52:14",
        "children": [{
            "seller_ship_time": "2018-08-23 11:59:37",
            "create_time": "2018-08-23 12:32:15",
            "level": 1,
            "partner_ship_time": "2018-08-23 12:32:15",
            "crown_id": null,
            "user_name": "13922112131",
            "crown_ship": 1,
            "crown_apply_failure_times": 0,
            "real_name": "黄",
            "avatar": null,
            "followed": 0,
            "uid": "U011808231159370001",
            "follow_time": null,
            "crown_ship_temp": 1,
            "partner_id": null,
            "user_id": 3,
            "partner_ship": 1,
            "crown_ship_time": "2018-08-23 12:32:55",
            "phone": "13800000000",
            "parent_id": null,
            "id": 3,
            "seller_ship": 1,
            "seller_id": 3,
            "partner_level_id": 1,
            "monthly_amount": 0, //当月进货量
            "monthly_settlement_amount": 0 //当月提成
        }],
        "id": 2,
        "seller_id": 2,
        "status": "NORMAL"
    }
}
```

### 合伙人查看结算记录

GET https://mall.smallsaas.cn/rest/copartner_settlement 

Header: Authorization: token

Success Return:
```
{
    "status_code": 0,
    "data": [{
        "statistic_month": "2018-02",
        "settled_amount": 100, //分成
        "transferred_amount": 10000 //转积分
    }]
}
```

### 合伙人查看团队成员的进货提成明细

GET https://mall.smallsaas.cn/rest/copartner_settlement/:sellerid?month=2018-08 

Param: 
 - sellerId: 团队成员的sellerid

Header: Authorization: token

Success Return:
```
{
    "status_code": 0,
    "data": [{
        "product_name": "洗衣液",
        "amount": 100, //进货量
        "reward": 10, //提成
        "settlement_proportion": 10 //提成比例
    }]
}
```