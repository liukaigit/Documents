## U盘安装Win7系统步骤

**0、简介**
- 以本人2009年的华硕笔记本为例，硬盘1G，ddr2的2G内存条，现硬盘已经被折腾安装双系统，
系统运行缓慢卡顿，且概率性异常断电、蓝屏等，现有128G固态硬盘一块，杂牌U盘（32G）和
金士顿（16G）各一个，准备替换硬盘，让笔记本重新飞起来，过程U盘原因坎坷，最终成功。

**1、制作U盘启动盘**
- U盘
  - 选择质量过硬的品牌U盘（例如：金士顿），容量8G以上
    - 杂牌子U盘可能U启制作成功，但实际装机过程大概率出现不可预计错误，亲身尽力被坑惨
- U启制作工具
  - U启动
    - 官网：http://www.uqidong.com/
    - 选择装机版下载 （约500M）
    - 制作参考装机版使用教程：http://www.uqidong.com/upqdpzzjc/upqdzz.html
      - 特别提示需要模拟运行安装完成后的U启验证完整性，同时注意不要选择执行
  - U盘制作OK后，可以查看包含两个目录：GHO和ISO，后续安装主要使用GHO子目录
 
**2、Win7镜像**
- 下载ISO
  - 直接上windows网站下载32位的iso镜像文件，尽量找原始系统
    - 下载地址：http://win.ytwlpos.cn/
    - 上述网址包括:XP、Win7-32/64、Win10-64
    - iso镜像文件大小约3G
- 提取GHO
  - iso镜像文件利用虚拟光驱（Daemon Tool）解压，提取内置的GHO文件，例如：`Windows7_32_2018.GHO`
    - 找Daemon Tool的官网下载软件安装
    
- 拷贝U盘
  - 将GHO文件拷贝到U盘的/GHO/目录
  
 **3、替换硬盘**
 - 网上有许多替换笔记本硬盘的方法，相差无几，下面是百度链接，注意硬盘拆硬盘方法，电池边上，直接拽出
  - https://jingyan.baidu.com/article/fec4bce258d866f2608d8b5b.html

**4、安装系统**
- 连接电源并启动，根据不同品牌不同按键进入启动盘选择，华硕电脑按ESC键，选择U盘启动，等待进入U启界面
根据制作U启时提供的装机参考使用教程，选择进入win PE系统；
- 进入系统后会自动弹出装机指导窗口，选择GHO文件，选择安装分区，选择添加C引导区，可以先高级配置里面
检查GHO文件的完整性，然后选择开始安装且自动重启安装，然后可以喝茶了，等待自动安装完成...

**5、其他**
- U启系统自带磁盘分区工具，可以根据磁盘大小预先进行分区并格式化清理，C盘预留60G管够；
- 一次安装失败，继续重复操作安装，本人安装3次才成功装上系统，老硬件兼容性，毛病多