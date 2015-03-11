# 同事圈api设计
## 基本api
post /circle_contents 发新消息  
delete /circle_contents/:contentId 删除已发消息  
post /circle_contents/:contentId/comments 评论或赞  
~~delete /circle_contents/:contentId/comments/:commentId 撤消评论或取消赞~~  
delete /circle_comments/:commentId 撤消评论或取消赞  
get /circle/company 获取公司消息及评论  
get /circle/campaign/:campaignId 获取活动消息及评论  
get /circle/team/:teamId 获取个人小队消息及评论  

~~get /circle_reminds 获取是否有最新消息~~  
get /circle_reminds/comments 获取同事圈提醒(被赞、被评论、赞过或评论过的消息有更新)  
~~delete /circle_reminds/comments 删除同事圈提醒~~  

## 辅助api
~~get /teams?query 获取小队列表(在现在基础上添加功能)~~  
~~get /campaigns?query 获取活动列表(在现在基础上添加功能)~~  

## 数据模型
新添加2个集合: CircleContent, CircleComment.

CircleContent:
```coffeescript
CircleContent = new Schema
    cid:
        type: Schema.Types.ObjectId # 所属公司id
        required: true
    tid: [Schema.Types.ObjectId] # 关联的小队id(可选，不是必要的)
    campaign_id: Schema.Types.ObjectId # 关联的活动id(可选，不是必要的)
    content: String # 文本内容(content和photos至少要有一个)
    photos: [{
        uri: String
        width: Number
        height: Number
    }] # 照片列表
    post_user_id:
        type: Schema.Types.ObjectId # 发消息的用户的id（头像和昵称再次查询）
        required: true
    post_date:
        type: Date
        default: Date.now
        required: true
    status:
        type: String
        enum: ['show', 'delete']
        required: true
        default: 'show'
    latest_comment_date: # 最新评论时间
        type: Date
        required: true
    comment_user: [user] # 参与过评论的用户
    relative_cids: [Schema.Types.ObjectId] # 参加同事圈消息所属的活动的所有公司id
user # user组件
    _id: 
        type: Schema.Types.ObjectId
        required: true
    comment_num:
        type: Number
        required: true
    appreciated: # 参与评论者是否点赞
        type: Boolean
        default: false
        required: true
```

CircleComment:
```coffeescript
CircleComment = new Schema
    # 类型，评论或赞
    kind:
        type: String
        enum: ['comment', 'appreciate']
        required: true
    content: String
    is_only_to_content: # 是否仅仅是回复消息，而不是对用户(影响显示)
        type: Boolean
        default: true
        required: true
    target_content_id:
        type: Schema.Types.ObjectId # 评论目标消息的id
        required: true
    target_user_id:
        type: Schema.Types.ObjectId # 评论目标用户的id(直接回复消息则保存消息发布者的id)
        required: true
    post_user_cid:
        type: Schema.Types.ObjectId # 发评论或赞的用户的公司id
        required: true
    post_user_id:
        type: Schema.Types.ObjectId # 发评论或赞的用户的id（头像和昵称再次查询）
        required: true
    post_date:
        type: Date
        default: Date.now
    status:
        type: String
        enum: ['show', 'delete', 'content_delete']
        default: 'show'
```

