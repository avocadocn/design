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
```js

// [app, hr]发活动
app.post('/campaigns', token.needToken, ctrl.postCampaign);

// [app]首页获取活动，小队页获取最近活动，日历获取活动; [hr]活动管理页面中获取所有活动（公司+小队）、获取单个小队的活动、获取公司活动
app.get('/campaigns', token.needToken, ctrl.getCampaigns.switcher, ctrl.getCampaigns.filter, ctrl.getCampaigns.getHolder, ctrl.getCampaigns.auth, ctrl.getCampaigns.queryAndFormat);

// [app]活动详细页、活动详细页中的'详细'跳转后的页面、编辑活动页面、活动公告页；[hr]编辑活动的directive
app.get('/campaigns/:campaignId',token.needToken, resources.getCampaignByParamId, auth.authMiddleware(['getCampaigns']), ctrl.getCampaign);

// [app]编辑活动
app.put('/campaigns/:campaignId',token.needToken, resources.getCampaignByParamId, ctrl.updateCampaign);

// [app]关闭活动，[hr]关闭活动
app.delete('/campaigns/:campaignId', token.needToken, resources.getCampaignByParamId, ctrl.closeCampaign);

// [app]参加活动
app.post('/campaigns/:campaignId/users/:userId', token.needToken, resources.getCampaignByParamId, ctrl.joinCampaign);

// [app]退出活动
app.delete('/campaigns/:campaignId/users/:userId', token.needToken, resources.getCampaignByParamId, ctrl.quitCampaign);

// [app]处理挑战
app.put('/campaigns/:campaignId/dealProvoke',token.needToken, resources.getCampaignByParamId, ctrl.dealProvoke);

// [app, hr]获取活动类型；
app.get('/campaigns/mold/:requestType/:requestId',token.needToken, ctrl.getCampaignMolds);

// 未使用！！！
app.get('/campaigns/competition/:fromTeamId/:targetTeamId', token.needToken, ctrl.getCompetitionOfTeams);

// [app]获取两个小队的共同活动
app.get('/campaigns/competition/:teamId', token.needToken, getById.getTeamById, ctrl.getCompetitionOfCompanyWithTeam);
```

<a name="chats"></a>
## chats

```js

// [app]发聊天消息
app.post('/chatrooms/:chatroomId/chats', token.needToken, ctrl.canPublishChat, ctrl.uploadPhotoForChat, ctrl.searchRecommandTeam, ctrl.createChat);

// [app]获取某聊天室的聊天记录
app.get('/chats', token.needToken, ctrl.getChats);

// 未使用！！！
app.delete('/chats/:chatId', token.needToken, ctrl.deleteChat);

// [app]读取聊天室提醒，清除未读数
app.post('/chatrooms/actions/read', token.needToken, ctrl.readChatRoomChats);

// [app]获取聊天室列表
app.get('/chatrooms', token.needToken, ctrl.getChatRooms);

// [app]获取未读数
app.get('/chatrooms/unread', token.needToken, ctrl.getChatroomsUnread);
```

<a name="circle">
## circle

```js
// [app]发新消息
app.post('/circle_contents', token.needToken, ctrl.singleImgUploadSwitcher, ctrl.getFormData, ctrl.uploadPhotoForContent, ctrl.createCircleContent);

// [app]获取某个内容的详情及其评论
app.get('/circle_contents/:contentId', token.needToken, ctrl.getCircleContent);

// [app]删除已发消息
app.delete('/circle_contents/:contentId', token.needToken, ctrl.getCircleContentById, ctrl.deleteCircleContent);

// [app]评论或赞
app.post('/circle_contents/:contentId/comments', token.needToken, ctrl.getCircleContentById, ctrl.createCircleComment);

// [app]撤消评论或取消赞
app.delete('/circle_comments/:commentId', token.needToken, ctrl.deleteCircleComment);

// [app]获取公司精彩瞬间
app.get('/circle/company', token.needToken, ctrl.getCompanyCircle);

// [app]获取小队精彩瞬间
app.get('/circle/team/:teamId', token.needToken, ctrl.getTeamCircle);

// [app]获取活动精彩瞬间
app.get('/circle/campaign/:campaignId', token.needToken, ctrl.getCampaignCircle);

// [app]获取个人精彩瞬间
app.get('/circle/user/:userId', token.needToken, ctrl.getUserCircle);

// [app]获取同事圈提醒(被赞、被评论、赞过或评论过的消息有更新)
app.get('/circle_reminds/comments', token.needToken, ctrl.getCircleComments);

// [app]获取是否有最新消息(红点)，现在不仅仅是获取精彩瞬间的
app.get('/circle_reminds', token.needToken, ctrl.getReminds);
```

<a name="comments"></a>
## comments

```js

// [app]挑战日志、活动讨论
app.post('/comments/host_type/:hostType/host_id/:hostId', token.needToken, ctrl.canPublishComment, ctrl.getCampaignPhotoAlbum, ctrl.uploadPhotoForComment, ctrl.createComments);

// [app]挑战日志、活动讨论
app.get('/comments', token.needToken, ctrl.getComments);

// 未使用！！！
app.delete('/comments/:commentId', token.needToken, ctrl.getCommentById, ctrl.deleteComment);
```

<a name="company"></a>
## company

```js

// [app]企业注册
app.post('/companies', ctrl.registerValidate, ctrl.register, ctrl.registerSave);

// [app]获取公司资料
app.get('/companies/:companyId', token.needToken, ctrl.getCompany);

// [app]获取公司数据
app.put('/companies/:companyId', token.needToken, ctrl.getCompanyById, ctrl.updateCompanyValidate, ctrl.updateCompanyLogo, ctrl.updateCompany);

// [app]修改公司封面
app.put('/companies/:companyId/companyCover', token.needToken, ctrl.getCompanyById, ctrl.updateCompanyCover);

// [app]公司注册验证邮件名称等
app.post('/companies/validate', ctrl.companyInfoValidate);

// [app]公司账号忘记密码
app.post('/companies/forgetPassword', ctrl.forgetPassword);

// [hr]查询公司没有任命队长的小队和待激活的员工
app.get('/companies/:companyId/undisposed', token.needToken, ctrl.getCompanyUndisposed);

// [app]获取公司统计数据（app在小队列表里用来获取小队）
app.get('/companies/:companyId/statistics', token.needToken, ctrl.getCompanyStatistics);

// [hr]获取图表的统计数据
app.get('/companies/:companyId/charts', token.needToken, ctrl.getCompanyCharts);

// 未使用！！！
app.get('/companies/:companyId/members', token.needToken, ctrl.getCompanyMembers);

// [hr]获取最新成员
app.get('/companies/:companyId/latestMembers', token.needToken, ctrl.getLatestMembers);

// [hr]获取公司被举报的员工
app.get('/companies/:companyId/reportedMembers', token.needToken, ctrl.getCompanyReportedMembers);

// 未使用！！！
app.get('/companies/:companyId/departments', token.needToken, ctrl.getCompanyDepartments);

// 未使用！！！
app.get('/companies/:companyId/tags', token.needToken, ctrl.getCompanyTags);

// [app, hr]公司登录
app.post('/companies/login', ctrl.login);

// [app]更新token
app.post('/companies/refresh/token', token.needToken, ctrl.refreshToken);

// [app, hr]退出
app.post('/companies/logout', token.needToken, ctrl.logout);

// [hr]获取公司是否任命过队长
app.get('/companies/:companyId/hasLeader', token.needToken, ctrl.hasLeader);
```

<a name="competition_messages"></a>
## competition_messages

```js
// [app]挑战信相关
app.post('/competition_messages', token.needToken, ctrl.sendMessageValidate, ctrl.createMessage);
app.get('/competition_messages', token.needToken, ctrl.getMessages.filter, ctrl.getMessages.queryAndFormat);
app.get('/competition_messages/:messageId', token.needToken, ctrl.getMessage);
app.put('/competition_messages/:messageId', token.needToken, ctrl.dealValidate, ctrl.dealCompetition);
```


<a name="components"></a>
## components

```js
// [app]比分板相关
app.post('/components/ScoreBoard/:componentId', token.needToken, ctrl.ScoreBoard.setScoreValidate, ctrl.ScoreBoard.setScore);
app.get('/components/ScoreBoard/:componentId', token.needToken, ctrl.ScoreBoard.getScore);
app.get('/components/ScoreBoard/logs/:componentId', token.needToken, ctrl.ScoreBoard.getLogs);
app.put('/components/ScoreBoard/:componentId',token.needToken, ctrl.ScoreBoard.confirmScore);

// [app]投票相关
app.post('/components/Vote/:componentId',token.needToken, ctrl.Vote.vote);
app.delete('/components/Vote/:componentId',token.needToken, ctrl.Vote.cancelVote);
app.get('/components/Vote/:componentId',token.needToken, ctrl.Vote.getVote);
```

<a name="departments"></a>
## departments

```js
// 以下路由 [hr]部门管理 全部用到
app.get('/departmentTree/:companyId', token.needToken, ctrl.getDepartmentTree);
app.get('/departmentTree/:companyId/detail', token.needToken, ctrl.getDepartmentTreeDetail);

app.post('/departments', token.needToken, ctrl.createDepartment);
app.get('/departments/:departmentId', token.needToken, ctrl.getDepartment);
app.put('/departments/:departmentId', token.needToken, ctrl.updateDepartment);
app.delete('/departments/:departmentId', token.needToken, ctrl.deleteDepartment);

app.post('/departments/:departmentId/actions/appointManager', token.needToken, ctrl.appointManager);
```

<a name="files"></a>
## files

```js
// [app]上传精彩瞬间照片
app.post('/files', token.needToken, ctrl.upload);
```

<a name="invitecode"></a>
## invitecode
```js
// 未使用！！！
app.get('/invitecode', ctrl.checkInviteCode);
```

<a name="messages"></a>
## messages
```js
// [app]发活动公告
app.post('/messages', token.needToken, ctrl.sendMessage);

// [app]获取站内信，活动列表
app.get('/messages', token.needToken, ctrl.getMessageList);

// 未使用！！！
app.put('/messages', token.needToken, ctrl.updateMessageList);

// [app]收取个人站内信
app.get('/messages/:requestType/:requestId', token.needToken, ctrl.receiveMessage);

// 未使用！！！
app.get('/messages/send/:requestType/:requestId', token.needToken, ctrl.getSendMessage);
```

<a name="photos"></a>
## photos
注：app已经不使用相册功能，下面用到的只是以前未删掉的代码
```js
// 未使用！！！
app.post('/photo_albums', token.needToken, ctrl.createPhotoAlbumValidate, ctrl.createPhotoAlbum);

// [app]获取小队相册列表
app.get('/photo_albums', token.needToken, ctrl.getPhotoAlbumsValidate, ctrl.getPhotoAlbums);

// [app]获取某个相册的数据
app.get('/photo_albums/:photoAlbumId', token.needToken, ctrl.getPhotoAlbumById, ctrl.getPhotoAlbum);

// 未使用！！！
app.put('/photo_albums/:photoAlbumId', token.needToken, ctrl.getPhotoAlbumById, ctrl.editPhotoAlbumValidate, ctrl.editPhotoAlbum);

// 未使用！！！
app.delete('/photo_albums/:photoAlbumId', token.needToken, ctrl.getPhotoAlbumById, ctrl.deletePhotoAlbum);

// [app]上传照片到某个相册
app.post('/photo_albums/:photoAlbumId/photos', token.needToken, ctrl.getPhotoAlbumById, ctrl.uploadPhoto);

// 获取某个相册的所有照片
app.get('/photo_albums/:photoAlbumId/photos', token.needToken, ctrl.getPhotoAlbumById, ctrl.getPhotos);

// 未使用！！！
app.get('/photo_albums/:photoAlbumId/photos/:photoId', token.needToken, ctrl.getPhoto);

// 未使用！！！
app.put('/photo_albums/:photoAlbumId/photos/:photoId', token.needToken, ctrl.editPhotoValidate, ctrl.editPhoto);

// 未使用！！！
app.delete('/photo_albums/:photoAlbumId/photos/:photoId', token.needToken, ctrl.getPhotoAlbumById, ctrl.deletePhoto);
```

<a name="rank"></a>
## rank

```js
// [app]获取排行榜
app.get('/rank',token.needToken, ctrl.getRank);、

// [app]获取小队的排行列表
app.get('/rank/team/:teamId', token.needToken, getById.getTeamById, ctrl.getTeamRank);

// 未使用！！！
app.get('/rank/user', token.needToken, ctrl.getUserTeamRank);

// 未使用！！！
app.post('/rank/update', token.needToken, ctrl.update);
```

<a name="region"></a>
## region

```js
// 获取省市区域信息
app.get('/region', ctrl.getRegions);
```

<a name="report"></a>
## report

```js
// [app]举报用户
app.post('/report',token.needToken, ctrl.pushReport);

// [hr]处理举报
app.put('/report',token.needToken, ctrl.dealReport);
```

<a name="search"></a>
## search

```js
// [app]用户注册时搜索公司
app.post('/search/companies', ctrl.searchCompanies);

// [hr]搜索用户
app.post('/search/users', token.needToken, ctrl.searchUsers);
```

<a name="teams"></a>
## teams

```js
// [app, hr]创建小队
app.post('/teams', token.needToken, ctrl.createTeams);

// [app, hr]
app.get('/teams', token.needToken, ctrl.getTeamsValidate, ctrl.getTeamsSetQueryOptions, ctrl.getTeams);

// [app, hr]
app.get('/teams/:teamId', token.needToken, getById.getTeamById, ctrl.getTeam);

// [app, hr]
app.put('/teams/:teamId', token.needToken, getById.getTeamById, ctrl.updateTeamLogo, ctrl.editTeamData);

// [hr]关闭小队
app.delete('/teams/:teamId', token.needToken, getById.getTeamById, ctrl.deleteTeam);

// [hr]打开小队
app.post('/teams/:teamId/actions/open', token.needToken, getById.getTeamById, ctrl.openTeam);

// [app, hr]添加小队封面
app.post('/teams/:teamId/family_photos', token.needToken, getById.getTeamById, ctrl.uploadFamilyPhotos);

// [app, hr]获取小队封面
app.get('/teams/:teamId/family_photos', token.needToken, getById.getTeamById, ctrl.getFamilyPhotos);

// [app]小队封面编辑页曾经使用，现在已弃用
app.put('/teams/:teamId/family_photos/:familyPhotoId', token.needToken, getById.getTeamById, ctrl.toggleSelectFamilyPhoto);

// 未使用！！！
app.delete('/teams/:teamId/family_photos/:familyPhotoId', token.needToken, getById.getTeamById, ctrl.deleteFamilyPhoto);

// [app]加入小队
app.put('/teams/:teamId/users/:userId', token.needToken, getById.getUserById, getById.getTeamById, ctrl.joinTeam);

// [app]退出小队
app.delete('/teams/:teamId/users/:userId', token.needToken, getById.getUserById, getById.getTeamById, ctrl.quitTeam);

// 未使用！！！
app.get('/teams/:teamId/tags', token.needToken, ctrl.getTeamTags);

// [app]获取小队成员列表
app.get('/teams/:teamId/members', token.needToken, ctrl.getMembers);

// [app, hr]获取供新建小队用的全部类型group
app.get('/groups', token.needToken, ctrl.getGroups);

// [app]获取管理的小队
app.get('/teams/lead/list', token.needToken, ctrl.getLedTeams);

// [app]查找小队
app.get('/teams/search/:type', token.needToken, ctrl.getSearchTeamsOptions, ctrl.getSearchTeams);
```
<a name="timeline"></a>
## timeline

```js
// [app]存在service和TimelineController中，但都已经弃用
app.get('/timeline/record/:requestType/:requestId',token.needToken, ctrl.getTimelineRecord);
app.get('/timeline/data/:requestType/:requestId', token.needToken, ctrl.getTimelineData);
app.get('/timeline/:requestType/:requestId', token.needToken, ctrl.getTimeline);
```

<a name="users"></a>
## users
```js
// [app]
app.post('/users', ctrl.getCompanyByCid, ctrl.registerValidate, ctrl.register);

// [app]
app.post('/users/validate', ctrl.userInfoValidate);

// [app]
app.get('/users/:userId', token.needToken, ctrl.getUserById);

// [app]
app.put('/users/:userId', token.needToken, getById.getUserById, ctrl.updateValidate, ctrl.updatePhoto, ctrl.update);

// [app]
app.get('/users/list/:companyId', token.needToken, ctrl.getCompanyUsers);

// [app]
app.post('/users/forgetPassword', ctrl.forgetPassword);

// [app]
app.post('/users/sendFeedback', token.needToken, ctrl.sendFeedback);

// [hr]
app.post('/users/:userId/close', token.needToken, getById.getUserById, ctrl.close);

// [hr]
app.post('/users/:userId/open', token.needToken, getById.getUserById, ctrl.open);

// [hr]
app.post('/users/:userId/active', token.needToken, getById.getUserById, ctrl.activeUser);

// [hr]
app.post('/users/actions/invite', token.needToken, ctrl.inviteUser);

// [hr]
app.post('/users/actions/batchinvite', token.needToken, ctrl.batchinviteUser);

// [app]
app.post('/users/login', ctrl.login);

// [app]
app.post('/users/refresh/token', token.needToken, ctrl.refreshToken);

// [app]
app.post('/users/logout', token.needToken, ctrl.logout);

// 未使用！！！
app.get('/users/:userId/photos', token.needToken, ctrl.getUserPhotosValidate, ctrl.getUserPhotos);

// [hr]获取员工评论，但已经被注释掉了
app.get('/users/:userId/comments', token.needToken, getById.getUserById, ctrl.getUserComments);
```
