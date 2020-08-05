## 收货地址API

### 我的地址列表

GET https://mall.smallsaas.cn/rest/contact 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "id": 3,
        "zip": "510000",
        "detail": "6F",
        "phone": "1380000000",
        "contact_user": "Mr Huang",
        "street": "jianzhong road",
        "province": "GD",
        "is_default": 1,
        "street_number": "50",
        "user_id": 4,
        "district": "Tiahne",
        "city": "GZ"
    }]
}
```

### 添加新地址

POST https://mall.smallsaas.cn/rest/contact 

Header: Authorization: token

Data:
```
{
    "contact_user": "Mr Huang",
    "phone": "1380000000",
    "zip": "510000",
    "province": "GD",
    "city": "GZ",
    "district": "Tiahne",
    "street": "jianzhong road",
    "street_number": "50",
    "detail": "6F",
    "is_default": 1
}
```

Return:
```
{
    "status_code": 0,
    "data": "contact.saved"
}
```

### 更新地址

PUT https://mall.smallsaas.cn/rest/contact/id 

Header: Authorization: token

Data:
```
{
    "contact_user": "Mr Huang",
    "phone": "1380000000",
    "zip": "510000",
    "province": "GD",
    "city": "GZ",
    "district": "Tiahne",
    "street": "jianzhong road",
    "street_number": "50",
    "detail": "6F",
    "is_default": 0
}
```

Return:
```
{
    "status_code": 0,
    "data": {
        "id": 1,
        "contact_user": "Mr Huang",
        "phone": "1380000000",
        "zip": "510000",
        "province": "GD",
        "city": "GZ",
        "district": "Tiahne",
        "street": "jianzhong road",
        "street_number": "50",
        "detail": "6F"
        "is_default": 0,
        "user_id": 1
    }
}
```

### 删除地址

DELETE https://mall.smallsaas.cn/rest/contact/id 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": "contact.deleted"
}
```

### 得到默认地址

GET https://mall.smallsaas.cn/rest/default_contact 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": {
        "id": 73,
        "zip": "510000",
        "detail": "5F",
        "phone": "1380000000",
        "contact_user": "Mr Huang",
        "street": "jianzhong roadxxxxx",
        "province": "广东省",
        "is_default": 1,
        "street_number": "50",
        "user_id": 4,
        "district": "天河区",
        "city": "广州市"
    }
}
```

### 更新默认地址

PUT https://mall.smallsaas.cn/rest/default_contact/id 

Header: Authorization: token

Return:
```
{
    "message": "contact.updated",
    "status_code": 0
}
```