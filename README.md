#工大野生助手

##访问量

![](http://7xku3h.com1.z0.glb.clouddn.com/16-7-16/85684382.jpg)

##预览

![](http://7xku3h.com1.z0.glb.clouddn.com/16-7-23/12366574.jpg)
![](http://7xku3h.com1.z0.glb.clouddn.com/16-7-23/47965690.jpg)

##功能

- 查某学期的各科成绩。
- 查所有学期总的加权平均分和平均GPA。

##运行模式

- 这两个PHP页面运行在Apache中；
- Apache安装在我的电脑上；
- 电脑连了学校的内网，也就是bjut-wifi或者插网线；
- 将自己电脑的80端口映射到外网。映射的方法很多，我用的是ngrok这个开源工具，也可以用花生壳等。
- 【手机端(扫二维码访问登陆页面)】<--->【外网映射服务器】<--(学校网关)-->【内网电脑,运行着Apache】<--->【教务网站】

##细节

- `login_grade.php`负责登陆，`require_grade.php`负责具体的查询。

###login_grade.php

- UI用的是「WeUI」，微信团队做的，和微信的视觉效果一致；
- 每个学校的正方教务都不太一样，我的代码中的各种http header参数、post参数基本符合北工大的教务网站。
- 教务系统的默认登陆页面是`default2`，可以换换default后面的数字，可以有不需要验证码的登陆页面。

###require_grade.php

- 中文编码容易出现乱码，涉及到本地IDE的编码、PHP的编码和网站的编码；
- 有两种post，第一种是登陆，第二种是获取成绩信息。获取成绩信息的时候有多次post，分别是获取某学期的成绩和获取总成绩；
- 构造POST的思路：打开浏览器开发者工具，先正常走一遍查询成绩的流程，观察POST数据的key和value，并在代码中构造；
- 由于页面返回的是一坨DIV，而且既没有name属性也没有id属性，所以需要将table标签整个转成array，并观察所需要的信息的位置，通过数组下标的方式访问；
- 总的平均GPA无法区分主修专业和二专业/辅修专业，因为查询所有科目的总成绩页面中没有任何标签能区分这两者。


##其他

- 其实就是个爬虫，模拟了登陆正方教务系统并查询成绩的过程。Python写爬虫的话可能更方便，Python有个库requests，非常好用。
- PHP中嵌入HTML感觉很不优雅，但HTML中嵌入PHP也好不到哪里去，有什么更好的办法吗？
- 网上有很多关于正方教务的东西，虽然不太容易直接照搬，但学习价值很大。table转html的函数我就是从网上找的。
- 交流请联系 807103724@qq.com，微信同QQ。
- 欢迎提交Issue和Pull Request！

##LICENSE(假装我写出了一个开源的东西)

MIT