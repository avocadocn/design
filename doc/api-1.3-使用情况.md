# donler v1.3 api 使用情况

以下路由注释的中括号中，app表示app在使用，hr表示网站企业管理面板在使用。

* [campaigns](#campaigns)
* [chats](#chats)
* [circle](#circle)
* [company](#company)
* [competition_messages](#competition_messages)
* [components](#components)
* [departments](#departments)
* [files](#files)
* [invitecode](#invitecode)
* [messages](#messages)
* [photos](#photos)
* [rank](#rank)
* [region](#region)
* [search](#search)
* [teams](#teams)
* [timeline](#timeline)
* [users](#users)

<a name="campaigns"></a>
## campaigns


* `post /campaigns` - [app, hr]发活动

* `get /campaigns` - [app]首页获取活动，小队页获取最近活动，日历获取活动; [hr]活动管理页面中获取所有活动（公司+小队）、获取单个小队的活动、获取公司活动

* `get /campaigns/:campaignId` - [app]活动详细页、活动详细页中的'详细'跳转后的页面、编辑活动页面、活动公告页；[hr]编辑活动的directive

* `put /campaigns/:campaignId` - [app]编辑活动

* `delete /campaigns/:campaignId` - [app]关闭活动，[hr]关闭活动

* `post /campaigns/:campaignId/users/:userId` - [app]参加活动

* `delete /campaigns/:campaignId/users/:userId` - [app]退出活动

* `put /campaigns/:campaignId/dealProvoke` - [app]处理挑战

* `get /campaigns/mold/:requestType/:requestId` - [app, hr]获取活动类型；

* `get /campaigns/competition/:fromTeamId/:targetTeamId` - 未使用！！！

* `get /campaigns/competition/:teamId` - [app]获取两个小队的共同活动


<a name="chats"></a>
## chats



* `post /chatrooms/:chatroomId/chats` - [app]发聊天消息

* `get /chats` - [app]获取某聊天室的聊天记录

* `delete /chats/:chatId` - 未使用！！！

* `post /chatrooms/actions/read` - [app]读取聊天室提醒，清除未读数

* `get /chatrooms` - [app]获取聊天室列表

* `get /chatrooms/unread` - [app]获取未读数


<a name="circle">
## circle

* `post /circle_contents` - [app]发新消息

* `get /circle_contents/:contentId` - [app]获取某个内容的详情及其评论

* `delete /circle_contents/:contentId` - [app]删除已发消息

* `post /circle_contents/:contentId/comments` - [app]评论或赞

* `delete /circle_comments/:commentId` - [app]撤消评论或取消赞

* `get /circle/company` - [app]获取公司精彩瞬间

* `get /circle/team/:teamId` - [app]获取小队精彩瞬间

* `get /circle/campaign/:campaignId` - [app]获取活动精彩瞬间

* `get /circle/user/:userId` - [app]获取个人精彩瞬间

* `get /circle_reminds/comments` - [app]获取同事圈提醒(被赞、被评论、赞过或评论过的消息有更新)

* `get /circle_reminds` - [app]获取是否有最新消息(红点)，现在不仅仅是获取精彩瞬间的


<a name="comments"></a>
## comments


* `post /comments/host_type/:hostType/host_id/:hostId` - [app]挑战日志、活动讨论

* `get /comments` - [app]挑战日志、活动讨论

* `delete /comments/:commentId` - 未使用！！！


<a name="company"></a>
## company



* `post /companies` - [app]企业注册

* `get /companies/:companyId` - [app]获取公司资料

* `put /companies/:companyId` - [app]获取公司数据

* `put /companies/:companyId/companyCover` - [app]修改公司封面

* `post /companies/validate` - [app]公司注册验证邮件名称等

* `post /companies/forgetPassword` - [app]公司账号忘记密码

* `get /companies/:companyId/undisposed` - [hr]查询公司没有任命队长的小队和待激活的员工

* `get /companies/:companyId/statistics` - [app]获取公司统计数据（app在小队列表里用来获取小队）

* `get /companies/:companyId/charts` - [hr]获取图表的统计数据

* `get /companies/:companyId/members` - 未使用！！！

* `get /companies/:companyId/latestMembers` - [hr]获取最新成员

* `get /companies/:companyId/reportedMembers` - [hr]获取公司被举报的员工

* `get /companies/:companyId/departments` - 未使用！！！

* `get /companies/:companyId/tags` - 未使用！！！

* `post /companies/login` - [app, hr]公司登录

* `post /companies/refresh/token` - [app]更新token

* `post /companies/logout` - [app, hr]退出

* `get /companies/:companyId/hasLeader` - [hr]获取公司是否任命过队长


<a name="competition_messages"></a>
## competition_messages

[app]挑战信相关

* `post /competition_messages`
* `get /competition_messages`
* `get /competition_messages/:messageId`
* `put /competition_messages/:messageId`

<a name="components"></a>
## components

[app]比分板相关
* `post /components/ScoreBoard/:componentId`
* `get /components/ScoreBoard/:componentId`
* `get /components/ScoreBoard/logs/:componentId`
* `put /components/ScoreBoard/:componentId`

[app]投票相关
* `post /components/Vote/:componentId`
* `delete /components/Vote/:componentId`
* `get /components/Vote/:componentId`


<a name="departments"></a>
## departments

以下路由 [hr]部门管理 全部用到
* `get /departmentTree/:companyId`
* `get /departmentTree/:companyId/detail`

* `post /departments`
* `get /departments/:departmentId`
* `put /departments/:departmentId`
* `delete /departments/:departmentId`

* `post /departments/:departmentId/actions/appointManager`


<a name="files"></a>
## files


* `post /files` - [app]上传精彩瞬间照片


<a name="invitecode"></a>
## invitecode

* `get /invitecode` - 未使用！！！


<a name="messages"></a>
## messages

* `post /messages` - [app]发活动公告

* `get /messages` - [app]获取站内信，活动列表

* `put /messages` - 未使用！！！

* `get /messages/:requestType/:requestId` - [app]收取个人站内信

* `get /messages/send/:requestType/:requestId` - 未使用！！！


<a name="photos"></a>
## photos
注：app已经不使用相册功能，下面用到的只是以前未删掉的代码

* `post /photo_albums` - 未使用！！！

* `get /photo_albums` - [app]获取小队相册列表

* `get /photo_albums/:photoAlbumId` - [app]获取某个相册的数据

* `put /photo_albums/:photoAlbumId` - 未使用！！！

* `delete /photo_albums/:photoAlbumId` - 未使用！！！

* `post /photo_albums/:photoAlbumId/photos` - [app]上传照片到某个相册

* `get /photo_albums/:photoAlbumId/photos` - 获取某个相册的所有照片

* `get /photo_albums/:photoAlbumId/photos/:photoId` - 未使用！！！

* `put /photo_albums/:photoAlbumId/photos/:photoId` - 未使用！！！

* `delete /photo_albums/:photoAlbumId/photos/:photoId` - 未使用！！！


<a name="rank"></a>
## rank


* `get /rank` - [app]获取排行榜

* `get /rank/team/:teamId` - [app]获取小队的排行列表

* `get /rank/user` - 未使用！！！

* `post /rank/update` - 未使用！！！


<a name="region"></a>
## region


* `get /region` - 获取省市区域信息


<a name="report"></a>
## report


* `post /report` - [app]举报用户

* `put /report` - [hr]处理举报


<a name="search"></a>
## search


* `post /search/companies` - [app]用户注册时搜索公司

* `post /search/users` - [hr]搜索用户


<a name="teams"></a>
## teams


* `post /teams` - [app, hr]创建小队

* `get /teams` - [app, hr]

* `get /teams/:teamId` - [app, hr]

* `put /teams/:teamId` - [app, hr]

* `delete /teams/:teamId` - [hr]关闭小队

* `post /teams/:teamId/actions/open` - [hr]打开小队

* `post /teams/:teamId/family_photos` - [app, hr]添加小队封面

* `get /teams/:teamId/family_photos` - [app, hr]获取小队封面

* `put /teams/:teamId/family_photos/:familyPhotoId` - [app]小队封面编辑页曾经使用，现在已弃用

* `delete /teams/:teamId/family_photos/:familyPhotoId` - 未使用！！！

* `put /teams/:teamId/users/:userId` - [app]加入小队

* `delete /teams/:teamId/users/:userId` - [app]退出小队

* `get /teams/:teamId/tags` - 未使用！！！

* `get /teams/:teamId/members` - [app]获取小队成员列表

* `get /groups` - [app, hr]获取供新建小队用的全部类型group

* `get /teams/lead/list` - [app]获取管理的小队

* `get /teams/search/:type` - [app]查找小队


<a name="timeline"></a>
## timeline

[app]存在service和TimelineController中，但都已经弃用

* `get /timeline/record/:requestType/:requestId`

* `get /timeline/data/:requestType/:requestId`

* `get /timeline/:requestType/:requestId`


<a name="users"></a>
## users

* `post /users` - [app]

* `post /users/validate` - [app]

* `get /users/:userId` - [app]

* `put /users/:userId` - [app]

* `get /users/list/:companyId` - [app]

* `post /users/forgetPassword` - [app]

* `post /users/sendFeedback` - [app]

* `post /users/:userId/close` - [hr]

* `post /users/:userId/open` - [hr]

* `post /users/:userId/active` - [hr]

* `post /users/actions/invite` - [hr]

* `post /users/actions/batchinvite` - [hr]

* `post /users/login` - [app]

* `post /users/refresh/token` - [app]

* `post /users/logout` - [app]

* `get /users/:userId/photos` - 未使用！！！

* `get /users/:userId/comments` - [hr]获取员工评论，但已经被注释掉了
