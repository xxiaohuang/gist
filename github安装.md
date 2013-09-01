####A、获取安装包

官方网址：  http://railsinstaller.org 

下载安装包：
http://rubyinstaller.org/downloads/ 
http://rubyforge.org/frs/download.php/75894/railsinstaller-2.1.0.exe
http://rubyforge.org/frs/download.php/76054/rubyinstaller-1.9.3-p194.exe
####B、安装
运行`railsinstaller-2.1.0.exe`,用默认选项下一步安装即可
 
检查ruby是否安装成功

	D:\Sites>ruby -v
 
检查rubygem是否安装

	D:\Sites>gem -v
 
更新rubygem

	D:\Sites>gem update --system  
 
命令行中再次输入：

	D:\Sites>gem -v
 
返回：1.8.24 说明已更新至最新版本
 
####1.1.2安装Devkit

获取安装包：
http://rubyinstaller.org/downloads/ 
https://github.com/downloads/oneclick/rubyinstaller/DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe

双击下载的7z文件，指定解压路径，路径中不能有空格。如`D:\Devkit`。
命令行中执行命令：


	D:\Sites>cd D:\Devkit 
	D:\Devkit>ruby dk.rb init 
	D:\Devkit>ruby dk.rb install 

```
验证是否安装成功
命令行中输入如下命令：
`D:\Sites>gem install rdiscount --platform=ruby`  
 
####1.1.3安装Selenium-webdriver
安装
命令行中输入命令：

	D:\Sites>gem install selenium-webdriver 
 
验证是否安装成功
命令行中输入命令：
	
	D:\Sites>gem list selenium-webdriver  
 
####1.1.4安装rspec
安装
命令行中输入如下命令：

	D:\Sites>gem install rspec 
 
验证是否安装成功

	D:\Sites>gem list rspec  