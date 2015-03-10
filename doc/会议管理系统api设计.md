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

|   名称   |  属性 |   描述  |
|---------|-------|------|
pid|Schema.Types.ObjectId `required: true`|发布者id
active|Boolean `default: true` `requried: true`|状态
theme|String `requried: true`|主题
introduction|String `requried: true`|简介
member_num|Number `requried: true`|额定人数
member_num_remained|Number `requried: true`|剩余人数
create_time|Date `default: Date.now`|创建时间
start_time|Date `requried: true`|开始时间
end_time|Date `requried: true`|结束时间
realname|Boolean `default: false` `requried: true`|真实姓名（必填）
identity_card|Boolean `default: false` `requried: true`|身份证id（必填）
email|Boolean `default: false` `requried: true`|邮箱（必填）
phone|Boolean `default: false` `requried: true`|手机（必填）
sex|Boolean `default: false` `requried: true`|性别（可选）
birthday|Boolean `default: false` `requried: true`|生日（可选）
qq|Boolean `default: false` `requried: true`|qq（可选）
cname|Boolean `default: false` `requried: true`|公司名称（可选）
department|Boolean `default: false` `requried: true`|部门名称（可选）
users|Array|用户组件

user组件

|   名称   |  属性 |   描述 |
---------|-------|------
_id|Schema.Types.ObjectId `required: true`|注册用户id
check_status|Boolean `default: false` `required: true`|审核状态
sign_status|Boolean `default: false` `required: true`|签到状态

ActivityUser

|   名称   |  属性 |   描述 |
---------|-------|------
activity_id|Schema.Types.ObjectId|额外活动id（必填）
realname|String|真实姓名（必填）
identity_card|String|身份证id（必填）
email|String|邮箱（必填）
phone|String|手机（必填）
sex|String `enum: ['男', '女']`|性别（可选）
birthday|Date|生日（可选）
qq|String|qq（可选）
cname|String|公司名称（可选）
department|String|部门名称（可选）
