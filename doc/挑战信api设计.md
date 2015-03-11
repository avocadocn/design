# 挑战信api设计
## 基本api
post /competition_messages 发挑战信
get /competition_messages 获取挑战信（个人/小队，发出/收到的挑战日志）
put /competition_messages/:messageId 接受/拒绝挑战

##辅助api
components:
post /components/vote 投票

## 数据模型
新增：CompetitonMessage, Vote

CompetitonMessage: #挑战信
```coffeescript
CompetitonMessage = new Schema
  sponsor_team:   #发起方
    type: Schema.Types.ObjectId
    ref: 'CompanyGroup'
  opposite_team:  #被挑战方
    type: Schema.Types.ObjectId
    ref: 'CompanyGroup'
  competition_type: Number     #类型，1为挑战，2为联谊
  create_time:    #创建时间
    type: Date
    default: Date.now
  deal_time:      #处理时间
    type: Date
  status:         #状态
    type: String
    #分别为：已发送请求(未被处理),接受未发活动,被拒绝,已生成挑战
    enum: ['sent', 'accepted', 'rejected', 'competing']
    default: 'sent'
  campaign:       #发成功后的campaign的_id
    type: Schema.Types.ObjectId
    ref: 'Campaign'
  content: String #挑战词

Vote：   #投票组件
  host_id: Schema.Types.ObjectId #主体id,如挑战信等
  host_type:                     #主体类型
    type: String
    enum: ['competition']
    default: 'competition'
  units: [{
    tid:Schema.Types.ObjectId    #小队id
    positive:                    #赞成人数
      type: Number
      default: 0
    positive_member: [{
      type: Schema.Types.ObjectId
      ref: 'User'
    }]  #赞成者
  }]
```

Comments模型修改:
```javascript
//增加以挑战信为主体
host_type:{
  type: String,
  enum: ['message', 'album', 'campaign', 'competition', 'campaign_detail', 'photo', 'comment', 'competition_message']
}
```
