---
title: hexo 项目部署
date: 2018-07-25 15:59:31
tags:
---
# github相关设置

## 安装git
安装包见群文件

## 新建ssh key
1. 桌面右键选择git bash here
2. 创建本地 ssh key，输入如下命令：
```
ssh-keygen -t rsa -C "邮箱"
```
回车，然后记录下ssh默认路径
3. 后续一路回车，直到出现很多泡沫
4. 打开ssh默认保存路径，找到id_rsa.pub文件，复制里面的内容备用

## 注册github
1. 打开[github](https://www.github.com)点击右上角sign up 注册个人账号 
2. 点击头像倒三角，选择settings
3. 选择左侧ssh and gpk keys
4. 点击右侧 添加ssh key按钮
   title随意，下方粘贴创建好的ssh key
5. 点击下方create ssh 按钮

## 验证ssh key
1. 命令行输入
```
ssh -T git@github.com
```
回车，如果第一次会提示是否continue，输入yes会看到：You've successfully 就表示已经成功连上github
2. 验证github用户名
```
git config --global user.name "用户名"
```
3. 验证邮箱
```
git config --global user.email "邮箱"
```

## 测试github本地连接
1. 点击github主页头像左侧加号选择new repository
2. 创建一个仓库，取名abc（随意）
3. 创建成功后，复制提示代码
4. 在桌面创建任意文件夹并打开
5. 右键 git bash here
6. 右键past刚才复制的代码回车
7. 弹出框内根据提示登录github账号
8. 个别情况下需要在命令行窗口验证github用户名
9. 刷新github的abc仓库，如果本地文件存在，证明连接无误
   否则删除文件夹内所有文件，重复步骤4~8
# 推送本地博客到github
## 配置hexo的_config.yml文件
1. 打开博客项目根目录的_config.yml文件
2. 在文件底部配置如下：
```
deploy:
  type: git
  repository: https://github.com/用户名/用户名.github.io
  ```
  并且保存
  3. 安装deploy 依赖包(仅需操作一次)
  在blog所在路径输入如下命令回车
  ```
  npm install hexo-deployer-git --save
  ```
  4. 添加域名解析文件
  在vscode选中根目录的source文件，右键新建文件，取名为CNAME（无后缀名），打开该文件，填入自己的域名：xwzsqc.cn（格式）
  5. 在blog所在路径依次输入如下命令
  清楚缓存
  ```
  hexo clean
  ```
  编译博客文件
  ```
  hexo g
  ```
  上传代码
  ```
  hexo d
  ```

  ## 域名解析
  1. 打开aliyun域名控制中心
  2. 选中自己购买的域名右侧解析
  3. 删除已有的解析记录
  4. 点击新建解析按钮添加三条记录值

  记录类型|主机记录|解析线路|记录值
  :-:|:-:|:-:|:-:
  CNAME|WWW|默认|用户名.github.io
  A|@|默认|192.30.252.153
  A|@|默认|192.30.252.154
