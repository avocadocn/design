# 排行榜api设计
## 基本api
get /rank 获取某城市的某类型的排行榜，如果本公司有该类型小队则增加自己公司小队的信息  
~~get /rank/company/:companyId 获取公司的所有小队的排行信息~~  
get /rank/team/:teamId 获取小队的排行信息  
get /rank/user 获取个人的所有参加的小队的排行信息  

## 数据模型
新添加2个集合: Rank

Rank:
```javascript
//小队模型
var _team = new Schema({
  _id: Schema.Types.ObjectId, // 小队的id
  cid:Schema.Types.ObjectId,  // 小队的公司id
  name: String,               // 小队名称
  logo: String,               // 小队的logo
  activity_score: Number,     // 小队的活跃度
  score: Number,              // 小队的积分
  rank: Number                // 小队的排名
});
//排行榜模型
var Rank = new Schema({
  create_date: {
    type: Date,
    default: Date.now
  },                           // 创建时间
  city: {
    province: String,
    city: String
  },                           //所属地区，省市
  group_type:{
    _id:String,
    name:String
  },                           // 小队类型
  name: String,                // 排行榜的名称，暂时未使用
  team: [_team]                // 排行榜里的小队
});
```

