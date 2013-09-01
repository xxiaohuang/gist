###ruby webdriver 启动firefox driver时，加载firebug的扩展

在官方wiki上看到
>Adding an extension
It's often useful to have Firebug available in the Firefox instance launched by WebDriver:

 

	profile = Selenium::WebDriver::Firefox::Profile.new
	profile.add_extension("/path/to/firebug.xpi")
	driver = Selenium::WebDriver.for :firefox, :profile => profile
 

 于是乎自己尝试了下，但是呢每次都是提示我firebug.xpi找不到

今天有空倒腾了，问题解决了
其实是之前的理解错了，因为__dr =Selenium::WebDriver.for:ff__
启动ff时，都是初始化一个最简单的profile，里面不带有firebug插件的，也就是说，哪怕我们原先在firefox上面安装了firebug，也是启动不了的，所以当我们需要使用firebug时,才需要加载一个firebug的扩展


	profile.add_extension("/path/to/firebug.xpi")
 至于“/path/to/firebug.xpi”就是firebug.xpi的存放路径了，我们可以去网上下载一个firebug.xpi（对应版本， 我的ff是14，可以使用firebug-1.10.4.xpi，最好使用非firefox浏览器下载，不然提示你直接安装到firefox）
我们可以直接把firefox.xpi存放在我们脚本所存放的路径，相对路径和绝对路径都可以
举个百度的例子


	require 'selenium-webdriver'
 
	#dr = Selenium::WebDriver.for :ff
	profile = Selenium::WebDriver::Firefox::Profile.new
	profile.add_extension("path/to/firebug-1.10.4.xpi")  <font color="DarkOrchid">#firefox-1.10.4.xpi存放在与脚本同级的path/to下面</font>
	dr = Selenium::WebDriver.for :firefox, :profile => profile
	dr.get "http://www.baidu.com"

 这样子当我们需要查看dom结构时，我们就可以直接在打开的测试页面上调试啦，不用去新开个firefox去查看dom结构了。