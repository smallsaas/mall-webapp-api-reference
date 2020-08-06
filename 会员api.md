## 会员API

### 会员级别列表

GET https://mall.smallsaas.cn/rest/member_level 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "id": 1,
        "point": 1000,
        "description": null,
        "name": "Level 1"
    }, {
        "id": 2,
        "point": 2000,
        "description": null,
        "name": "Level 2"
    }, {
        "id": 3,
        "point": 5000,
        "description": null,
        "name": "Level 3"
    }, {
        "id": 4,
        "point": 10000,
        "description": null,
        "name": "Level 4"
    }]
}
```

### 会员信息

GET https://mall.smallsaas.cn/rest/member 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "id": 3,
        "point": 0,
        "birthday": null,
        "sex": null,
        "address": null,
        "description": null,
        "name": "abc",
        "user_id": 4,
        "level_id": 1,
        "mobile": null
    }
}
```

### 更新会员信息

PUT https://mall.smallsaas.cn/rest/member 

Header: Authorization: token

Data:
```
{
"birthday": "1999-10-10",
"sex": 1,
"address": "GZ liwan",
"description": "xxvv",
"name": "abc",
"mobile": "138000000"
}
```

Return:
```
{
    "message": "member.updated",
    "status_code": 0
}
```