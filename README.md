
开发此系统主要用于国科大研究生同学选课、教师管理开设课程和管理员发布通知

### 此系统针对学生用户、教师用户和管理员用户的功能如下：
- 查询成绩
- 选课退课
- 课程管理
- 用户管理
- 开课管理
- 添加成绩
- 多角色登陆（学生，老师，管理员）
- 管理员发布通知
- 管理员发布校园活动
- 管理员开放/关闭选课系统
- 管理员系统界面的汉化
- 教师对选课学生成绩单导入导出
- 教师开启/关闭选课按钮
- 学生查看课表
- 学生修改是/否学位课属性
- 学生显示修读课程成绩排名

### 截图

<img src="/lib/screenshot1.png" width="700">  

<img src="/lib/screenshot2.png" width="700">

<img src="/lib/screenshot3.png" width="700">   

<img src="/lib/screenshot4.png" width="700">

<img src="/lib/screenshot5.png" width="700">

## 说明

目前使用的库和数据库：

* 使用[Bootstrap](http://getbootstrap.com/)作为前端库
* 使用[Rails_admin Gem](https://github.com/sferik/rails_admin)作为后台管理
* 使用[Postgresql](http://postgresapp.com/)作为数据库

使用前需要安装Bundler，Gem，Ruby，Rails等依赖环境。

## 安装

在终端（MacOS或Linux）中执行以下代码

```
$ git clone https://github.com/muskmelon9527/software
$ bundle install
$ sudo service postgresql start
$ psql
ubuntu=# UPDATE pg_database SET datistemplate = FALSE WHERE datname = 'template1';
ubuntu=# DROP DATABASE template1;
ubuntu=# CREATE DATABASE template1 WITH TEMPLATE = template0 ENCODING = 'UNICODE';
ubuntu=# UPDATE pg_database SET datistemplate = TRUE WHERE datname = 'template1';
ubuntu=# \c template1
template1=# VACUUM FREEZE;
template1=# \q
$ rake db:create:all
$ rake db:migrate
$ rake db:seed
$ rails server -p $PORT -b $IP
```

在浏览器中输入`localhost:3000`访问主页


## 将开发的选课系统部署到Heroku平台
```
$ heroku login//输入账号及密码
$ git init 
$ git add .
$ git commit -m “init”
$ git status 
$ heroku create
$ git config --list | grep heroku
$ git push heroku master 

```
本次部署出现了错误（precompiling assets failed）,经stack overflow也一直未能找到有效的解决办法。

## 使用
1.学生登陆：

账号：`student1@test.com`

密码：`password`

2.老师登陆：

账号：`teacher1@test.com`

密码：`password`


3.管理员登陆：

账号：`admin@test.com`

密码：`password`

账号中数字都可以替换成2,3...等等

## 功能测试及展示

### 管理员功能

- 发布通知以及校园活动公告

- 关闭选课系统

- 设置选课人数限制

### 教师功能

- Excel文件数据导入导出

- 查看通知

### 学生功能

- 查看课程表

- 设置学位课

- 查看修读课程成绩排名


## 测试用例
- 测试1：编辑或添加教务通知

  > Given 学生身份登录的student1
  >
  > when 学生点击“选课通知”
  >
  > then 跳转页面，显示“选课通知”的详细情况，但无“编辑”按钮
  >
  >  
  >
  >  
  >
  > Given 管理员身份登录的admin
  >
  > and 处于“选课通知”的详细情况页面
  >
  > when 管理员点击编辑按钮
  >
  > then 跳转到通知编辑页面，编辑完可选择保存
  >
  >  
  >
  >  
  >
  > Given 管理员身份登录的admin
  >
  > and 处于控制面板中教务通知界面
  >
  > when 管理员点击添加按钮
  >
  > then 跳转到通知编辑页面，保存后生成了新的教务通知



- 测试2:查看教务通知

  > Given 游客身份
  >
  > and 未登录
  >
  > when 用户点击通知栏的“选课通知”
  >
  > then 跳转页面，显示“选课通知”的详细情况





- 测试3：显示课程表

  > Given 学生身份登录的student1
  >
  > and 处于“已选课程”页面
  >
  > when 学生点击右侧“<”按钮
  >
  > then 以课程表的形式显示student1已选课程的课程名和上课教室
  >
  > when 学生再次点击课程表左侧的“>”按钮
  >
  > then 隐藏课程表界面


- 测试4：编辑或添加讲座信息

  > Given 学生身份登录的student1
  >
  > and 处于选课系统主页
  >
  > when 学生点击讲座信息
  >
  > then 无反应（学生无法修改讲座信息）
  >
  >  
  >
  >  
  >
  > Given 管理员身份登录的admin
  >
  > and 处于控制面板中讲座信息界面
  >
  > when 管理员点击添加按钮
  >
  > then 跳转到讲座信息编辑页面，保存后生成了新的讲座信息

- 测试5：开放选课系统

  > Given 学生身份登录的student1
  >
  > and 选课系统处于开放状态
  >
  > and 处于“我的课程”页面
  >
  > when 学生点击“选修课程”按钮
  >
  > then 跳转页面，显示student1可选的所有课程
  >
  > when 学生点击“已选课程”按钮
  >
  > then 显示student1的已选课程，同时显示“删除课程”按钮

- 测试6：处理选课时间冲突

  > Given 学生身份登录的student1
  >
  > and student1已选一门与“模式识别与机器学习”时间冲突的课“编译程序高级原理”
  >
  > and 处于“选修课程”页面
  >
  > when 学生选择“模式识别与机器学习”这门课
  >
  > then 弹出通知窗口“选课失败！模式识别与机器学习 与 编译程序高级原理 上课时间冲突！”并跳转到已选课程界面

- 测试7：显示已获学分

  > Given 学生身份登录的student1
  >
  > and student1共选7门课
  >
  > and student1已有4门课已出成绩
  >
  > and 有3门课成绩不低于60分，共7学分
  >
  > and 处于“我的课程”页面
  >
  > when 学生点击所有成绩
  >
  > then 只显示已获成绩的4门课，并且在成绩列表下方展示学生应或学分数20，和已获学分数7（已获学分只统计成绩不低于60分的课程）

- 测试8：设置课程限选人数

  > Given 管理员身份登录的admin
  >
  > and 处于控制面板中课程界面
  >
  > when 管理员点击课程“计算机体系结构”后的编辑按钮
  >
  > then 跳转到该课程编辑页面，管理员可更改课程限选人数并保存
  >
  >  
  >
  >  
  >
  > Given 老师身份登录的teacher1
  >
  > and 处于课程管理页面
  >
  > when 老师点击已授课程中“计算机体系结构”后的编辑按钮
  >
  > then 跳转到该课程编辑页面，老师可更改该课程限选人数并保存
  >
  >  
  >
  >  
  >
  > Given 学生身份登录的student1
  >
  > and 选课系统处于开放状态
  >
  > and “计算机体系结构”课程选课人数已达限选人数
  >
  > and 处于“选修课程”页面
  >
  > when 学生选课“计算机体系结构”
  >
  > then 弹出通知窗口“选课失败！选课人数已达上限！”


