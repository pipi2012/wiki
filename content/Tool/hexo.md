---
title: hexo-使用
layout: page
date: 2016-02-16 14:28
---
[TOC]

##环境要求
	Git
	Node.js（Windows 环境下，仅须下载安装文件并执行即可完成安装）

##Hexo安装（Git Bash下）
###安装
	npm install hexo -g
	或
	npm install -g hexo-cli（官网）
###升级
	npm update hexo -g
###安装依赖包
	npm install

###示例	
	$ hexo init blog
	$ cd blog
	$ npm install

##Hexo使用
###初始化
	cd targetdir
	hexo init
	或
	hexo init <folder>
###生成网站
	hexo generate
###启动服务器
	hexo server
	访问链接：http://localhost:port （port 预设为 4000，可在 _config.yml 设定）

##About页面
###新建about页面
	hexo new page "about"
	菜单显示 about 链接，在 主题配置文件 设置中将 menu 中 about 前面的注释去掉即可。
	menu:
	  home: /
	  archives: /archives
	  tags: /tags
	  about: /about

##写文章
###新建文章
	hexo new [layout] "postName"
	layout：default post
###layout编辑
	layout配置文件在scaffolds目录下，可编辑与新建
	title: { { title } }
	date: { { date } }
	categories:
	tags:
	---
###postName.md文件说明	
	title: postName #文章页面上的显示名称，可以任意修改，不会出现在URL中
	date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
	categories: #文章分类目录，可以为空，注意:后面有个空格
	tags: #文章标签，可空，多标签请用格式[tag1,tag2,tag3]，注意:后面有个空格
	---
	这里开始使用markdown格式输入你的正文。

##Git发布
###Install hexo-deployer-git
	$ npm install hexo-deployer-git --save
###Edit settings
	# Deployment
	## Docs: http://hexo.io/docs/deployment.html
	deploy:
	  type: git
	  repo: <repository url>
	  branch: [branch]
	  message: [message]
	  
	Option	Description
	repo	GitHub repository URL
	branch	Branch name. The deployer will automatically detect the branch automatically if you are using GitHub or GitCafe.
	message	Customize commit message (Default to Site updated: {{ now("YYYY-MM-DD HH:mm:ss") }})
###Example
	deploy:
	  type: git
	  repo: git@github.com:pipi2012/blog.git
	  branch: gh-pages
	  message: 

##命令
###常用命令
	hexo new "postName" #新建文章
	hexo new page "pageName" #新建页面
	hexo generate #生成静态页面至public目录
	hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
	hexo deploy #将.deploy目录部署到GitHub
	hexo help  # 查看帮助
	hexo version  #查看Hexo的版本
	hexo clean #清除缓存

###Commands:
	clean     Removed generated files and cache.
	config    Get or set configurations.
	deploy    Deploy your website.
	generate  Generate static files.
	help      Get help on a command.
	init      Create a new Hexo folder.
	list      List the information of the site
	migrate   Migrate your site from other system to Hexo.
	new       Create a new post.
	publish   Moves a draft post from _drafts to _posts folder.
	render    Render files with renderer plugins.
	server    Start the server.
	version   Display version information.

###复合命令
	hexo deploy -g  #生成加部署
	hexo server -g  #生成加预览
###命令简写
	hexo n == hexo new
	hexo g == hexo generate
	hexo s == hexo server
	hexo d == hexo deploy

##相关问题
###CNAME文件部署问题
hexo deploy命令，会先清空.deploy文件夹，再将public文件夹生成文件拷贝到.deploy文件夹，导致CNAME文件清除。

解决方法

在部署插件hexo-deployer-git的lib/deployer.js中.找到

	log.info('Copying files from public folder...');
	return fs.copyDir(publicDir, deployDir);

在fs.copyDir上面插入

	fs.writeFile(deployDir+'/CNAME', 'blog.starscount.com');

###分类、文章等删除问题
删除后如效果为改变，可以先hexo clean一下缓存，然后再生成发布。

\------------
> 文章修改记录  
> add time 2016-02-16 14:29
