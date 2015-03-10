# 额外活动api设计
## 基本api
post /activity Publisher发布活动 
get /activity Publisher获取活动信息
get /activity/:activityId/activiy_user/:activiyUserId Publisher审核

get /activity/:activityId 用户获取活动信息(途径：链接、二维码)
post /activity/:activityId 用户注册信息 

## 数据模型
新添加2个集合: Activity, ActivityUser.

Activity:
```coffeescript
var Activity = new Schema
  pid:  #发布者id
    type: Schema.Types.ObjectId
    required: true
  active: # 活动状态
    type: Boolean
    default: true
    requried: true
  theme: # 活动主题
    type: String
    required: true
  introduction: String # 活动简介
  member_num: # 活动额定人数
    type: Number
    required: true
  member_num_remained: # 活动剩余人数
    type: Number
    required: true
  create_time: # 活动创建时间
    type: Date
    default: Date.now
  start_time: # 活动开始时间
    type: Date
    required: true
  end_time: # 活动结束时间
    type: Date
    required: true
  // 选项（必填）
  realname: # 真实姓名
    type: Boolean
    default: false
    required: true
  identity_card: # 身份证号码
    type: Boolean
    default: false
    required: true
  email: # 邮箱
    type: Boolean
    default: false
    required: true
  phone: # 手机号
    type: Boolean
    default: false
    required: true
  // 选项（可选）
  sex: # 性别
    type: Boolean
    default: false
    required: true
  birthday: # 生日
    type: Boolean
    default: false
    required: true
  qq: # qq
    type: Boolean
    default: false
    required: true
  cname: # 公司名称
    type: Boolean
    default: false
    required: true
  department: # 部门名称
    type: Boolean
    default: false
    required: true
  users: [user]
user # user组件
  _id: 
    type: Schema.Types.ObjectId
    required: true
  check_status: // 审核状态
    type: Boolean
    default: false
    required: true
  sign_status: // 签到状态
    type: Boolean
    default: false
    required: true
```

ActivityUser:
```coffeescript
ActivityUser = new Schema
  activity_id: Schema.Types.ObjectId # 额外活动id
  // 选项（必填）
  realname: String,
  identity_card: String,
  email: String,
  phone: String,
  // 选项（可选）
  sex:
    type: String,
    enum: ['男', '女']
  birthday: Date
  qq: String
  cname: String
  department: String
```
   名称   |  属性 |   描述 
---------|-------|------
activity_id|Schema.Types.ObjectId|额外活动id
realname|String|真实姓名
identity_card|String|身份证id
email|String|邮箱
phone|String|手机
sex|String `enum: ['男', '女']`|性别
birthday|Date|生日
qq|String|qq
cname|String|公司名称
department|String|部门名称
