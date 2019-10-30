# svn库转git库

**1、准备事宜**

- 登录git的web访问页面；
	- http://cs.devops.sangfor.org/users/sign_in
	- 注意采用普通登录，账号为邮箱，密码可以通过邮箱重试；
		- 不要用快捷登录，后续提交和推送会用到账号和密码；
- 新建私有git仓库：
	- 登录后
	- 示例：http://cs.devops.sangfor.org/users/17189/projects，可以新建私有仓库项目；
	
- CSSP4.0.11仓库：
	- 仓库连接：http://cs.devops.sangfor.org/CloudSec/HCI/HCI5.8.5R1_CSSP4.0.11
	- 仓库地址：http://cs.devops.sangfor.org/CloudSec/HCI/HCI5.8.5R1_CSSP4.0.11.git
	- 基线来源于CSSP4.0.10B正式版：http://199.200.0.10/svn/HCI/HCI5.8.5R1_for_CSSP4.0.10B	
		- Revision：

- Xsec5.0.1仓库：
	- 仓库连接：http://cs.devops.sangfor.org/CloudSec/HCI/HCI5.8.5R1_XSec5.0.1
	- 仓库地址：http://cs.devops.sangfor.org/CloudSec/HCI/HCI5.8.5R1_XSec5.0.1.git
	- 基线来源于Xsec5.0.0正式版：http://199.200.0.10/svn/HCI/HCI5.8.5R1_for_XSec5.0.0
		- Revision：
	
**2、注意事项**

- 本地GIT仓库准备事宜：
	- linux环境下载HCI指定分支svn代码；
		- 执行命令：svn checkout [SVN代码路径]
		- linux环境推送目的防止windows上传文件属性丢失（so库软链接变成ASCII格式，导致编译失败）
	- 清理所有.svn文件（踢掉多余文件）
		- for dir in `find -name .svn`;do rm -rf $dir; done
	- 检查所有.svn文件清理（目录名称存在空格上述命令无法自动清理）
		- find ./ -name .svn
		- 拷贝所有检查结果到Notepad上面，利用替换命令快速批量构造命令：rm -rf ./xxx/yyy/78\ xfd/.svn，然后执行所有命令清理；
	- 保留空文件（部分目录名带空格忽略）
		- for dir in `find -type d -empty`;do touch "$dir/.gitkeep";done
	- 清理所有.gitignore文件（避免文件漏推送，不清理部分lib库编译依赖文件漏传，导致编译失败）；
		- for dir in `find -name .gitignore`;do rm -rf $dir;done

- 推送GIT仓库		
	- 获取仓库http格式链接，示例：http://cs.devops.sangfor.org/17189/file-test.git
		- 仓库默认为SSH，这个需要配置publickey，麻烦且不安全；
	- 添加GIT服务器域名解析：
		- echo 199.200.0.41 cs.devops.sangfor.org >> /etc/hosts
	- 本地GIT仓库目录执行如下命令：
	```
		git init 		//初始化
		git remote add origin http://cs.devops.sangfor.org/17189/test.git	//关联远端GIT仓库，这里仓库为示例，改成自己仓库
		git config --global user.name "17189@sangfor.com"		//添加用户名
		git config --global user.email "17189@sangfor.com"		//添加邮箱
		git add .		//添加本目录所有文件
		git commit -m "From Svn: http://199.200.0.10/svn/HCI/HCI5.8.5R1_for_CSSP4.0.10B ,Revision: xxx"		//本地提交，备注SVN支线及版本，便于追溯历史记录
		git push -u origin master
	```

- 预编译初始化：
	- 准备编译环境，这个参考原来svn打包环境通过模板部署调整网络构造HCI编译环境，有相关
