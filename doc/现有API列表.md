# 公司
## POST /company/mailCheck 验证邮箱是否已用于注册公司账号
```javascript
data: {
  login_email: String
}

res: Boolean
```
## POST /company/codeCheck 验证邀请码是否有效
```javascript
data: {
  invite_code: String
}

res: Boolean
```
## POST /company/officialNameCheck 验证企业官方名是否已被注册
```javascript
data: {
  official_name: String
}

res: Boolean
```
## POST /company/usernameCheck 验证企业用户名是否已被注册
```javascript
data: {
  username: String
}

res: Boolean
```
## POST /company/addDomain 添加邮箱后缀
```javascript
data: {
  companyId: String,
  domain: String
}

res: {
  result: Number, // 0或1, 成功为1，失败为0
  msg: String
}
```
## POST /company/groupSelect 选择小组
```javascript
data: {
    selected_groups: [{
      _id: String,
      group_type: String,
      entity_type: String
    }]
}

res: {
  result: Number,
  msg: String
}
//or
res: String // 错误时直接返回错误信息
```
## POST /company/createDetail 创建用户名和密码
```javascript
data: {
  official_name: String,
  username: String,
  password: String
}

res: {
  result: Number,
  msg: String
}
```
## POST /company/saveGroup/:companyId HR增加小队
```javascript
data: {
  selected_group: {
    _id: String,
    group_type: String,
    entity_type: String
  },
  tname: String
}

res: {
  result: Number,
  msg: String
}
// or
res: String
```
## GET /company/getCompanyTeamsInfo/:companyId/:type
```javascript
res: {
  cid: String,
  role: String,
  teams: [{
    _id: String,
    gid: String,
    did: String,
    group_type: String,
    logo: String,
    active: Boolean,
    count: {
      current_week_campaign: Number,
      current_week_member: Number,
      last_week_campaign: Number,
      last_week_member: Number,
      last_month_campaign: Number,
      last_month_member: Number
    },
    entity_type: String,
    leader: [{
      _id: String,
      nickname: String,
      photo: String,
      join_time: Date
    }],
    member: [{
      _id: String,
      nickname: String,
      photo: String,
      join_time: Date
    }],
    name: String,
    campaign_theme: String,
    campaign_id: String,
    campaign_start_time: Date,
    photos: [Object]
    photo_list: Date,
    more: Boolean,
    collapse: Boolean
  }]
}
// or
res: {
  result: Number,
  msg: String
}
```
## GET /company/timeLine/:companyId
```javascript
res: {
  result: Number,
  msg: String
}
// or
res: text/html
```
## POST /company/changeUser/:companyId 修改用户信息（注意，不是公司信息）
```javascript
data: {
  operate: String,
  user: {
    _id: String,
    nickname: String,
    photo: String,
    department: String
  }
}

res: {
  result: Number,
  msg: String
}
```
## GET /company/getAccount/:companyId
```javascript
res: {
  result: Number,
  company: {
    login_email: String,
    register_date: String,
    domain: String
  },
  info: Object， // mongoose.model('Company') Schema info
  team: [Object], // Schema team
  role: String,
  msg: String
}
```
## POST /company/changePassword/:companyId
```javascript
data: {
  nowpassword: String,
  newpassword: String
}

res: {
  result: Number,
  msg: String
}
```
## POST /company/saveAccount/:companyId
```javascript
data: {
  info: Object,
  domain: String
}

res: {
  result: 1,
  msg: String
}
```
## POST /company/saveGroupInfo/:companyId
```javascript
data: {
  tid: String,
  tname: String
}

res: {
  result: Number,
  msg: String
}
```
## POST /company/campaignSponsor/:companyId
```javascript
data: {
  theme: String,
  content: String, //(暂时只有挑战有)
  location: {
    name: String,
    coordinate: []
  },
  start_time: Date,
  deadline: Date,
  member_min: Number, //(选填)
  member_max: Number, //(选填)
  deadline: Date, //(选填)
  tags: [String] //(暂时只有挑战有,选填)
  campaign_mold: String
}

res: {
  result: Number,
  msg: String,
  campaign_id: String
}
```
## POST /company/appointLeader/:companyId
```javascript
data: {
  tid: String,
  user: Object, // 对象属性待确认
  operate: Boolean
}

res: {
  msg: String
} // 成功返回200状态码，失败返回500等其它错误码
```

## GET /company/getTags/:companyId 获取公司活动的tags
```javascript
res: {
  [{
    _id: String, // tag text
    number: Number
  }]
}
```
