Git安装手册及使用说明
安装步骤：
1、检查Git
命令行输入git检测系统是否安装如下：
# git
The program 'git' is currently not installed....       表示没有安装Git
usage: git [--version] [--help] [-c name=value].....    表示已经安装Git
若是安装了Git则输入命令git --version可查看当前版本，git --help可获取帮助信息等等。
  
  1. Ubuntu或者Debian安装Git
命令行输入sudo apt-get install git即可自动完成安装；
 
  1. Windows按装Git
资源下载地址：http://msysgit.github.io/
下载成功后直接双击安装即可，然后开始菜单找到“Git”->”Git Bash”，弹出一个类似命令行窗口，说明Git安装成功；
用户名信息注册：
# git config --global user.name "Your Name"
# git config --global user.email "email@example.com"
 
  1. 简易操作
  2. 选择GitHub远程仓库管理代码，登录GitHub官方网站：https://github.com注册账号；安装SSH key  ->     ssh-keygen -t rsa -C "youremail@example.com"
  3. 加密设置，首先查看是否创建了SSH Key，Linux打开终端主要查看/root/.ssh该文件是否存在，而Windows系统则是打开Git Bash，在当前用户目录下面查看是否存在.ssh/目录如下图所示：
 
 
可以看到该目录下有两个文件id_rsa（私钥）和id_rsa.pub（公钥）；
登录GitHub，打开右上角的“Settings”选择左边栏目中的“SSH and GPG keys”:
 
然后选择NewSSH key添加公钥，添加完成好进行保存即可，至此加密完成，这样确保你的推送不会被别人冒充。
  1. 创建远程仓库
登录你的GitHub账号，在主界面中右上角有“New repository”创建新的仓库，点击后进入界面：
 
输入仓库名称，然后点击“Create repository”这样一个空的仓库就创建成功了：
 
当然也可在“Settings”选项页面最下端有删除仓库的选项：
 
  1. 仓库准备完成，开始本地与远程仓库之间信息交互，先测试Linux系统，打开命令行终端，创建自己的/home/mygit目录
# git clone git@github.com:/liukaigit/testproject.git   将刚才在github网站创建的testproject仓库克隆到mygit目录中，这过程可能需要输入密码，完成后可以看到testproject目录，进入该目录
现在添加文件，并推送到github网站中的testproject仓库中
# touch README.txt
# git add README.txt       添加README.txt文件
# git commit -m “提交信息” 提交README.txt变动信息
# git remote   查看远程登录客户端名称默认origin
# git push origin master 推送当前修改的信息，输入密码，等待推送完成
这时候可以到github网站testproject仓库目录下查看，已经存在了README.txt文件。
 
  1. 常用命令
# git init 建立本地仓库使用
# git branch 查看所有分支，当前分支*标记
# git branch dev  创建新分支dev
# git branch -d dev 删除分支dev
# git chechout -b dev origin/dev   同时创建本地和远程分支
# git branch --set-upstream dev origin/dev   关联本地和远程分支
# git pull  从远程仓库获取最新提交信息
# git add 添加新增文件
# git commit -m “.....”   提交变动信息，并做简要说明
# git push origin master   master分支推送信息，也可以其他分支
# git status 查看当前本地仓库状态信息，是否需要做相应操作
# git remote   查看远程仓库信息，主要是客户端名称
# git log --pretty=oneline   按行显示日志所有提交记录
# git reset --hard HEAD^  退回上一个版本
# git reset --hard 版本号
# git reflog   显示记录下来的每一个提交命令，包含版本号
# git merge dev   合并dev分支到master主分支，有时候需要手动解决冲突
# git log --graph --pretty=oneline --abbrev-commit    查看分支合并情况
# git merge --no-ff -m “merge whit no-ff” dev   参数--no-ff在合并时保存分支信息
# git rm filename    删除文件
 
6）参考教程：http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
 
