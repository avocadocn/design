# 群组api设计
## 基本api
post /teams 发新群组
delete /teams/:teamId 删除群组
put /teams/:teamId 编辑群组
get /teams/user/:userId 获取个人群组列表(TODO)
get /teams/company 获取公司群组列表
get /teams/search 搜索群组
put /teams/:teamId/user/:userId 加入群组
delete /teams/:teamId/user/:userId 退出群组
post /teams/:teamsId/invite 群组邀请

## 数据模型
新添加1个集合: CompanyGroup.

CircleContent:
```coffeescript
var CompanyGroup = new Schema({
    cid: { // 公司id
        type: Schema.Types.ObjectId,
        ref: 'Company'
    },
    cname: String, // 公司名称

    name: String, // 群组名称

    logo: { // 群组封面（是否有default值）
        type: String,
        default: '/img/icons/default_group_logo.png'
    },

    theme_color: { // 群组主题颜色
        type: String,
        default: ''(TODO)
    },

    group_type: { // 群组类型
      open: { // 群组是否公开(全公司可见)
        type: Boolean,
        default: true
      },
      validate: { // 群组是否需要验证
        type: Boolean,
        default: false
      }
    },

    member: [_member], // 群组成员

    leader: { // 群组管理人员（队长）
      _id: {
        type: Schema.Types.ObjectId,
        ref: 'User'
      },
      nickname: String,
      photo: String,
      join_time: {
        type: Date,
        default: Date.now
      }
    },

    invite_url : [{ // 邀请链接
        type: String
    }],

    apply_members:[_apply_member], // 申请加入该群组的人(group_type.validate === true)

    // photo_album_list: [{
    //     type: Schema.Types.ObjectId,
    //     ref: 'PhotoAlbum'
    // }],

    active: { // 小队是否删除(true: 未删除， false: 删除)
        type: Boolean,
        default: true
    },

    // 小队所属公司是否关闭(true: 未关闭; false: 关闭)
    // company_active: { 
    //     type: Boolean,
    //     default: true
    // },

    create_time:{
        type: Date,
        default: Date.now
    }
});

var _member = new Schema({ // 群组成员组件
    _id: {
        type: Schema.Types.ObjectId,
        ref: 'User'
    },
    nickname: String,
    photo: String,
    join_time:{
        type: Date,
        default: Date.now
    },
    // admit_invite:{ // 是否允许群组邀请
    //     type: Boolean,
    //     default: true
    // },
    quit:{ // 是否退出群组
        type: Boolean,
        default: false 
    }
});

var _apply_member = new Schema({ // 申请加入的成员组件
    _id: {
        type: Schema.Types.ObjectId,
        ref: 'User'
    },
    nickname: String,
    photo: String,
    apply_time:{
        type: Date,
        default: Date.now
    },
    admit_join:{
        type: Boolean,
        default: false
    }
});
```

