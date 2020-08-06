## 其它配置API

### 意见反馈

POST https://mall.smallsaas.cn/rest/feedback 

Header: Authorization: token

Data:
```
{
    "content": "建议门槛更低些，可以让更多人参与。", //必选
    "images": [ //可选
        "http://image.url",
        "http://image2.url"
    ]
}
```

Return:
```
{
    "message": "feedback.created",
    "status_code": 0
}
```

Error Return:
```
{
    "message": "invalid.input.json",
    "status_code": 1
}
```

### 常见问题类型

GET https://mall.smallsaas.cn/rest/faq_type 

Header: Authorization:  token

Return:
```
{
    "status_code": 0,
    "data": [{
        "id": 1,
        "name": "FN"
    }, {
        "id": 2,
        "name": "UI"
    }]
}
```

### 常见问题

GET https://mall.smallsaas.cn/rest/faq?typeId=1&pageNumber=1&pageSize=20 

Header: Authorization: token

Param:

 - typeId - optional, 问题类型ID

 - pageNumber - optional, 页数

 - pageSize - optional, 每页记录数

Return:
```
{
    "status_code": 0,
    "data": [{
        "created_date": "2016-05-16 12:52:15",
        "content": "分销拥金可提现时间是订单关闭后一天。",
        "id": 1,
        "last_modified_date": "2016-05-16 12:52:15",
        "title": "分销拥金可提现时间",
        "type_id": 1
    }]
}
```

### 关于商城

GET https://mall.smallsaas.cn/rest/about_mall 

Return:
```
{
    "status_code": 0,
    "data": {
        "content": null,
        "id": 1,
        "image": "http://host:port/images/a.jpg"
    }
}
```

### 广告

#### 返回所有广告组别的广告。

GET https://mall.smallsaas.cn/rest/ad 


Return:
```
{
    "status_code": 0,
    "data": [{
        "id": 1,
        "name": "头位广告",
        "ads": [{
            "id": 1,
            "enabled": 1,
            "name": "a",
            "group_id": 1,
            "image": "/ad/7ce3c3f9662b92b759ecb8f523070631.jpg",
            "type": "a",
            "target_url": "http://localhost:9990"
    	}]
    }, {
        "id": 2,
        "name": "首页banner",
        "ads": []
    }]
}
```
#### 返回该组别下的广告列表。

GET https://mall.smallsaas.cn/rest/ad/{group-name}

Return:
```
{
    "status_code": 0,
    "data": [{
        "id": 1,
        "enabled": 1,
        "name": "a",
        "group_id": 1,
        "image": "/ad/7ce3c3f9662b92b759ecb8f523070631.jpg",
        "type": "a",
        "target_url": "http://localhost:9990"
    }]
}
```

### 客服QQ

#### 返回QQ列表。

GET https://mall.smallsaas.cn/rest/kf_qq 

Return:
```
{
    "status_code": 0,
    "data": [{
        "number": "234234", //QQ号
        "name": "AAA",
        "id": 1,
        "enabled": 1
    },{
        "number": "2342",
        "name": "BBB",
        "id": 2,
        "enabled": 1
    }]
}
```

### Base64上传图片

POST https://mall.smallsaas.cn/rest/upload_image 

> 通过POST base64 编码的图片来上传

Header: Authorization: token

Data:

> data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEASABIAAD/2\...\...\...

Return:
```
{
    "status_code": 0,
    "data":"http://112.74.26.228:8000/upload/2016-06-30/20160630113427-00803.jpg"
}
```

### form上传图片

POST https://mall.smallsaas.cn/rest/upload_image_x 

> 通过POST form 上传

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "file_name": "e39936cbc10f49cef1316342a3938fec.png",
        "original_file_name":"20180427-231841-把祷告事项从应用内分享到微信群\~显示错误.png",
        "url":"https://www.kequandian.net/upload/2018-05-30/e39936cbc10f49cef1316342a3938fec.png"
    },{
        "file_name": "ba87f98c1028d55f5978fca64a6bce29.jpeg",
        "original_file_name": "20161104133328890-xfTkpZAK.jpeg",
        "url":"https://www.kequandian.net/upload/2018-05-30/ba87f98c1028d55f5978fca64a6bce29.jpeg"
    }]
}
```

### 系统公告

GET https://mall.smallsaas.cn/rest/system_announcement 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": [{
        "name": "fdsf",
        "id": 33,
        "created_date": "2016-10-17 15:49:40",
        "content": "safas afds afadsfas"
    },{
        "name": "fdsfsd",
        "id": 34,
        "created_date": "2016-10-17 15:51:08",
        "content": "sfdsfds"
    }]
}
```

### 微信公众号访问域名

GET https://mall.smallsaas.cn/rest/wx/host_prefix 

Header: Authorization: token

Return:
```
{
    "status_code": 0,
    "data": "https://www.muaskin.com/wx"
}
```