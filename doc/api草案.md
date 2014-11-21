# Donler API 草案
## company
POST /companies 创建一个公司（用于注册公司用户）  
GET /companies/:id 获取公司数据  
PUT /companies/:id 修改公司数据(添加邮箱后缀，创建用户名，创建和修改密码，修改基本信息)  
DELETE /companies/:id 屏蔽公司  

POST /companies/validate 验证某个属性是否有效（邮箱，邀请码，企业官方名，企业用户名)  
GET /companies/:id/teams 获取公司小队数据  
GET /companies/:id/members 获取公司成员列表  
GET /companies/:id/departments 获取部门数据  

###使用场景：
注册时，填写完表单后，`POST /companies`。通过激活邮件进入设置用户名密码的页面，`PUT /companies/:id`，然后完成注册。(创建用户名密码待商榷)


## user
POST /users 注册用户  
GET /users/:id 获取用户数据  
PUT /users/:id 修改用户数据（昵称、密码等基本信息)  
DELETE /users/:id 屏蔽用户  

## team
POST /teams 创建小队  
GET /teams/:id 获取小队数据  
PUT /teams/:id 修改小队数据  
DELETE /teams/:id 关闭小队  

PUT /teams/:id/users/:userId 加入小队  
DELETE /teams/:id/users/:userId 退出小队  

## department
POST /departments 创建部门  
GET /departments/:id 获取部门数据  
PUT /departments/:id 修改部门数据  
DELETE /departments/:id 删除部门  

PUT /departments/:id/users/:userId 加入部门  
DELETE /departments/:id/users/:userId 退出部门  

## campaign
POST /campaigns 发起活动  
GET /campaigns/:id 获取活动数据  
GET /campaigns 获取活动数据（公司的、小队的、个人的活动）  
PUT /campaigns/:id 修改活动数据  
DELETE /campaigns/:id 关闭活动  

PUT /campaigns/:id/users/:userId 参加活动  
DELETE /campaigns/:id/users/:userId 退出活动  

## photo_album
POST /photo_albums 创建相册  
GET /photo_albums/:id 获取相册数据  
PUT /photo_albums/:id 修改相册  
DELETE /photo_albums/:id 删除相册  

POST /photo_albums/:id/photos 上传照片  
GET /photo_albums/:id/photos/:id 获取照片数据  
PUT /photo_albums/:id/photos/:id 修改照片  
DELETE /photo_albums/:id/photos/:id 删除照片  

## comment
POST /comments 发表评论  
GET /comments/:id 获取某条评论  
GET /comments 获取评论  
PUT /comments/:id 修改评论  
DELETE /comments/:id 删除评论  

## message
POST /messages 发站内信  
GET /messages 获取站内信  
PUT /messages/:id 修改站内信数据  
DELETE /messages/:id 删除站内信  

## inventcode
POST /inventcode 创建一个邀请码  
DELETE /inventcode/:id 删除邀请码  

## search
GET /search 搜索  

## region
GET /region 获取区域数据（省市区）  

## logo
GET /logo 获取logo  
PUT /logo 修改logo  

## tags
GET /tags 获取tags  