# Donler API 测试数据
说明，以下的response如果body中有数据，那么Content-Type默认为`application/json; charset=utf-8`，如果有不同，会特别说明。

所有GET请求，如果找不到相关资源，response的状态码为404

## company API
### POST /companies 创建一个公司
request body:
```javascript
{
  "name": "Donler Test Company", // 公司全称
  // 简称？
  "province": "上海市",
  "city": "上海市",
  "district": "黄浦区"
  "address": "北京西路210号",
  "contacts": "Dart",
  "lindline": {
    "areacode": "021",
    "number": "1234567",
    "extension": "01"
  },
  "email": "cahavar@55yali.com",
  "phone": "18800000881",
  "invite_code": "1A2B3C4D"
}
```
response
```
成功时返回:
Status Code: 201

请求数据不合法时返回:
Status Code: 400
Response Body:
{
  "email": "您输入的邮箱不正确",
  "phone": "手机号码必须是11位的阿拉伯数字",
  "invite_code": "该邀请码是一个无效的邀请码"
}

服务器异常:
Status Code: 500
```
### GET /companies/53aa6fc011fd597b3e1be250 获取公司数据
response:
```
成功时返回:
Status Code: 200

HR身份得到的数据：
{
  "_id": "53aa6fc011fd597b3e1be250",
  "username": "donler_test",
  "email_domains": ["donler.com", "55yali.com"],
  "name": "Donler Test Company",
  "province": "上海市",
  "city": "上海市",
  "district": "黄浦区"
  "address": "北京西路210号",
  "contacts": "Dart",
  "lindline": {
    "areacode": "021",
    "number": "1234567",
    "extension": "01"
  },
  "email": "cahavar@55yali.com",
  "phone": "18800000881",
  "brief": "Donler Test Company is a virtual company for test.",
  "logo": "/img/icons/default_company_logo.png",
  "membernumber": 7,
  "register_date": "2014-07-08T09:22:55.154Z",
  "register_invite_codes": ["3A4B5C6D", "3A4F5C6D"],
  "invite_key": "6FC8AB3D"
}

公司员工得到的数据:
{
  "_id": "53aa6fc011fd597b3e1be250",
  "email_domains": ["donler.com", "55yali.com"],
  "name": "Donler Test Company",
  "province": "上海市",
  "city": "上海市",
  "district": "黄浦区"
  "address": "北京西路210号",
  "lindline": {
    "areacode": "021",
    "number": "1234567",
    "extension": "01"
  },
  "brief": "Donler Test Company is a virtual company for test.",
  "logo": "/img/icons/default_company_logo.png",
  "membernumber": 7,
  "invite_key": "6FC8AB3D"
}



```
