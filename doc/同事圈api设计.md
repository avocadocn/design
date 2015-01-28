# 同事圈api设计
## 基本api
post /circle_contents 发新消息  
get /circle_contents 获取最新消息  
delete /circle_contents/:contentId 删除已发消息  
post /circle_contents/:contentId/comments 评论或赞  
delete /circle_contents/:contentId/comments/:commentId 撤消评论或取消赞  

get /circle_reminds?has_new=true 获取是否有最新消息  
get /circle_reminds?userId=xx 获取同事圈提醒(被赞、被评论、赞过或评论过的消息有更新)  
get /circle_messages 获取个人消息列表  

## 辅助api
get /teams?query 获取小队列表(在现在基础上添加功能)  
get /campaigns?query 获取活动列表(在现在基础上添加功能)  

## 数据模型
新添加3个集合: CircleContent, CircleComment, CircleRemind.

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
    post_user:
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
    comment_users: [Schema.Types.ObjectId] # 参与过评论的用户id
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
    post_user: Schema.Types.ObjectId # 发评论或赞的用户的id（头像和昵称再次查询）
    post_date:
        type: Date
        default: Date.now
    status:
        type: String
        enum: ['show', 'delete']
        default: 'show'
```

CircleRemind:
```coffeescript
CircleRemind = new Schema
    uid: Schema.Types.ObjectId # 消息提醒列表所有者id
    has_new_content: Boolean # 有没有同事发新消息
    msg_list: [{
        kind:
            type: String
            enum: ['newComment', 'newAppreciate'] # 类型：新的评论或赞
            required: true
        post_user: # 发赞或评论的用户
            _id:
                type: Schema.Types.ObjectId
                required: true
            photo:
                type: String
                required: true
            nickname:
                type: String
                required: true
        content: String # 评论内容
    }], # 可设置上限
    clear_date: Date # 上次清空消息列表的时间
```
