BugFree
=======
BugFree基于PHP和MySQL开发，是免费且开发源代码的缺陷管理系统。服务器端在Linux和Windows平台上都可以运行；客户端无需安装任何软件，通过IE，FireFox等浏览器就可以自由使用。

如何有效地管理软件产品中的 Bug，是每一家软件企业必须面临的问题。遗憾的是很多软件企业还是停留在作坊式的研发模式中，其研发流程、研发工具、人员管理不尽人意，无法有效的保证质量、控制进度，并使产品可持续发展。

针对这个问题， 我们使用BugFree来管理Bug，不断提高产品质量的.

官网地址
=======
http://www.bugfree.org.cn

新特性
=======
1. case支持导出导入注释
2. bug支持新增导入功能
3. 我的查询增加“抄送给我”的默认查询
4. 添加产品用户组管理员静态页面
5. 支持case、result等tab页面隐藏功能(如何修改)
6. 详情页上方toolbar栏固定显示
7. 注释栏和复现步骤栏可展开折叠显示
 
易用性
=======
1. 安装检测json_encode支持情况
2. 运行环境ldap模块检查
 
修复3.0.3版已知的bug
=======
1. 邮件通知不要发给已经禁用的用户
2. simple_html_dom使用错误
3. 特定情况下不能添加用户到某些用户组
4. 2.1.3升级到3时在升级product_module时出现duplicate id问题
5. case运行，保存时会报错
6. ie6,7,8,9浏览器下载中文名称的附件，名字会是乱码
7. 安装时，如果数据库名非法，不会给出任何出错信息
8. 激活Bug下，自定义字段不可编辑
 
Centos Nginx配置
=======
server {  
	# nginx 端口  
	listen 9090;  
	# bugfree服务器IP  
	server_name 192.168.10.211;  
	location / {  
		# 开户URL重写  
		if (!-e $request_filename) {  
			rewrite ^([_0-9a-zA-Z-]+)?(/wp-.*) $2 last;  
			rewrite ^([_0-9a-zA-Z-]+)?(/.*.php)$ $2 last;  
			rewrite ^ /bugfree/index.php last;  
		}  
		index index.html index.htm index.php;  
	}  
	# 支持PHP  
	location ~ .php$ {  
		root html;  
		fastcgi_pass 127.0.0.1:9000;  
		fastcgi_index index.php;  
		fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;   
		include fastcgi_params;  
	}  
}
