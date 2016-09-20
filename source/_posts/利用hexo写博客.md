title: 利用hexo写博客
date: 2016-09-07 12:13:22
tags: "hexo"

---
### 安装node
### 安装hexo
	npm install -g hexo
### 初始化
创建一个用来写博客的目录，并cd到该目录运行:

	hexo init
	hexo g
	npm install hexo-deployer-git --save
	
### 配置git
在github.com上面创建<username>.github.io的仓库
在当前目录下，修改_config.yml最下面，修改如下代码并保存
git地址为自己的仓库地址,注意“：”后面的空格

		deploy:
			type: git
            repository: git@github.com:dujiecn/dujiecn.github.io.git
            branch: master
### 发布
	hexo clean
	hexo g
	hexo d
### 验证
	访问dujiecn.github.io	  
### 插入图片插件
	npm install https://github.com/CodeFalling/hexo-asset-image --save

	MacGesture2-Publish
	├── apppicker.jpg
	├── logo.jpg
	└── rules.jpg
	MacGesture2-Publish.md

这样的目录结构（目录名和文章名一致），只要使用 
	
	![logo](MacGesture2-Publish/logo.jpg) 
就可以插入图片		
  	
	
	


		



