# 额外活动api设计
## 基本api
post /activity Publisher发布活动  
get /activity Publisher获取活动信息  
get /activity/:activityId/activiy_user/:activiyUserId Publisher审核  

get /activity/:activityId 用户获取活动信息(途径：链接、二维码)  
post /activity/:activityId 用户注册信息  

## 数据模型
新添加2个集合: Activity, ActivityUser.


```javascript
// 有没有同事发新消息, 如果已经为true了再有新消息，则不要再写入更新，在查询时设置条件过滤
has_new_content: {
  type: Boolean,
  default: false
},
new_comment_num: {
  type: Number,
  default: 0
},

// 最新发赞或评论的用户
new_comment_user: {
  _id: Schema.Types.ObjectId,
  photo: String,
  nickname: String
}
```
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
