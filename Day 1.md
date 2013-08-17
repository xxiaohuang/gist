Ruby 学习笔记 
-----
### 第一天笔记



这个 我kao，第一天的学习信息量也是很大的啊！
    
    require 'selenium-webdriver'

    dr = Selenium::WebDriver.for :chrome

    url1="http://www.baidu.com"
    url2="http://www.seleniumcn.cn"
    
    #导航地址，%Q 以双引号的方式打印url
    dr.get url1
    puts %Q(gogogo,let's go to #{url1})

    sleep 2
    
    #页面最大化
    dr.manage.window.maximize()
    sleep 2
    
    #打印当前页面的title和当前页面的url
    puts "now i am the max #{dr.title} in #{dr.current_url}"

    dr.get url2
    sleep 2

    puts "o,NO! i am go to #{url2}."
    
    #页面向后
    dr.navigate.back()
    sleep 2
    puts "Yes! i am back, i am in #{dr.current_url}"
    
    #设置页面大小 %q 以单引号方式打印信息
    dr.manage.window.resize_to(320,480)
    sleep 2
    puts %q(what happen , i am changing smale size... )
    
    #页面向后
    dr.navigate.forward()

    puts %Q(shit, small and back, what a fucking day! sleep,tomorrow will a good day!)
    sleep 2
    
    #退出
    dr.quit




