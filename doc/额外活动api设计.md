# 额外活动api设计
## 基本api
post /activity Publisher发布活动  
get /activity Publisher获取活动信息  
get /activity/:activityId/activiy_user/:activiyUserId Publisher审核  

get /activity/:activityId 用户获取活动信息(途径：链接、二维码)  
post /activity/:activityId 用户注册信息  

## 数据模型
新添加2个集合: Activity, ActivityUser.




ActivityUser:
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
