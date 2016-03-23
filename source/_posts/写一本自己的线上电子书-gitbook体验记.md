title: 写一本自己的线上电子书--gitbook体验记
tags: []
date: 2015-08-13 02:06:03
---

酝酿了很久,一直想通过自己的力量,将自己这一路走来的经历和感想汇集起来,其实算不上要写成一本书,只是希望将自己这些年的所思,所想,所得做一个小结.也算是给自己的一个交代.只希望自己的这段从校园到职场,再走出职场的时光能在今后的回望中仍能留下些印记来怀念罢了.

散文部分结束,下面是一个工科男针对上面的意图开展的一系列折腾经历.这个电子书成文的过程可能要分为好几个阶段和较长一段时间来完成.此文为开篇.也即是题中的后半部分gitbook体验记. 其实就是介绍一个超简介,能博得广大开发小伙伴喜欢的线上电子书平台,也是工具. 好了,进入正题.

<!-- more -->

gitbook官网:[https://www.gitbook.io/](https://www.gitbook.io/)

注册神马的很简单,就不多说了(推荐用github帐号登录).

创建好帐号后,进入管理后台会要求你下载官网的一个客户端工具:[https://www.gitbook.io/editor/download](https://www.gitbook.io/editor/download).

*注意:该链接会将下载目标导向Amazon AWS(亚马逊的云主机,在国内可能需要番羽土啬),链接类似:([https://s3.amazonaws.com/github-cloud/releases/18655678/9cec5b80-3a70-11e4-9dc8-815d88da4259.dmg?response-content-disposition=attachment%3B%20filename%3Dgitbook-mac.dmg&amp;AWSAccessKeyId=AKIAISTNZFOVBIJMK3TQ&amp;Expires=1411291614&amp;Signature=CiK0QMyphEsDphyVon3aNod9Kn4%3D](https://s3.amazonaws.com/github-cloud/releases/18655678/9cec5b80-3a70-11e4-9dc8-815d88da4259.dmg?response-content-disposition=attachment;%20filename=gitbook-mac.dmg&amp;AWSAccessKeyId=AKIAISTNZFOVBIJMK3TQ&amp;Expires=1411291614&amp;Signature=CiK0QMyphEsDphyVon3aNod9Kn4=))

前面的下载链接会判断当前请求客户端系统版本(win,linux,mac),然后跳转到对应版本客户端.并且是带有gitbook专属的访问密钥和签名的,也就是说你通过上面的连接是无法直接下载的.必须通过这个:[https://www.gitbook.io/](https://www.gitbook.io/)完成跳转. 考虑到部分童鞋对于番羽土啬等会出现的麻烦.特此记录下我自己遇到的问题以及解决办法.

直接通过链接跳转,被屏蔽! Orz.

![QQ20140921-1@2x.png](http://zozorz-typechoupload.stor.sinaapp.com/572277827.png)

![QQ20140921-2@2x.png](http://zozorz-typechoupload.stor.sinaapp.com/25836662.png)

开启goagent, 通过代理进行下载.

![QQ20140921-3@2x.png](http://zozorz-typechoupload.stor.sinaapp.com/2225234406.png)

NO!!,Oops,再次Orz.

![QQ20140921-4@2x.png](http://zozorz-typechoupload.stor.sinaapp.com/1564496995.png)

下载一部分后没反应了,有时候goagent也是靠不住的.本来想着继续通过vpngate上的公共vpn再试试的.但是自己有[DigitalOcean](https://www.digitalocean.com/?refcode=f32c6f23f408)的VPS,那就算了.直接通过VPS来下载吧(本来是在VPS上架设有PPTP的vpn的.不过速度实在是对不起观众.放弃).

登录上VPS,直接通过上面的链接用wget进行下载:

![QQ20140921-6@2x.png](http://zozorz-typechoupload.stor.sinaapp.com/3330346230.png)

下载是OK,但是由于gitbook下载服务器会针对客户端类型(win,linux,mac)分别跳转到响应的版本.vps的OS是centos 6.5\. 所以wget获取的客户端类型为linux版本.显然不是我要的mac版. 没办法,折腾到底. 为wget加一个http头设定吧.

    wget --header=&amp;quot;Referer:https://www.gitbook.io/book/zoorz/how-to-be-a-web-developer&amp;quot; --header=&amp;quot;User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2062.122 Safari/537.36&amp;quot; https://www.gitbook.io/editor/download

这回顺利获取到了mac版本的客户端,并顺利的完成了下载,然后通过ftp,或者sz(yum install lrzsz 进行工具安装)将文件同步到本地.VPS每月流量过多,而且文件不大.因此就这样干了.^_^.

有遇到上面下载链接获取不到客户端的小伙伴,我已经将当前最新版本(version 1.1.0)上传至网盘:[http://pan.baidu.com/s/1hq5S0HA](http://pan.baidu.com/s/1hq5S0HA)

三个版本都已经下载好,小伙伴们自行选择吧.^_^.

好了,客户端安装文件获取到了,安装过程就so easy了.

MAC版安装好之后的界面.

![QQ20140921-7@2x.png](http://zozorz-typechoupload.stor.sinaapp.com/1360097587.png)

好了,选择电子书类型后就开始享受文字之旅吧. 关于Gitbook editor的使用和最终的电子书同步和线上发布,这次的文字有点多了.下次再分享吧.