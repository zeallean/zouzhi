title: VPS迁移日志
tags: []
date: 2015-08-13 17:52:07
---

个人的手头在管理的一系列站点,由于之前野心勃勃的想着能整出多大一动静,处于完美主义的通病,出于未雨绸缪,提前搞了个Linode_2048配置的VPS来作为站点硬件架构.在沉下心来观察自己实力与现实的差距,很多是不是光靠想法和三两个好友就可以推进下去的. 在离职,组建团队折腾了几个月,烧掉一些资金后幡然醒悟.其实很多时候确实是自己不知天高地厚.沉下心来,朋友各自重新觅职的觅职,上班的上班,打酱油的接着打酱油.一返如常.零零碎碎的扯了一堆. 重点是要交代下此次迁移的背景条件.

<!-- more -->

原本放弃Linode之后,准备直接就用SAE来作为已有站点应用的临时落脚地. 不过思来想去还是难免太不自由. 正好赶上DigitalOcean搞活动,最低配的VPS(512M,20G SSD存储,2T流量)用来假设个站点也算是绰绰有余了.主要是价格便宜($5的月租,前两个月免单).那就先用着吧.

接下来就是一些列的迁移相关工作.

DO的VPS还是同样采用的Linode的相同linux版本,CentOS 6.5 x86 32位.建立droplet的过程很方便和快捷.就不做过多介绍了

## VPS 迁移

### 1\. 基础web环境搭建(LAMP)

这里可以直接参照DO的官方指导[How To Install Linux, Apache, MySQL, PHP (LAMP) stack On CentOS 6

]([https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-centos-6),相信可以轻松而愉快的搞定](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-centos-6),相信可以轻松而愉快的搞定)

### 2\. 文件迁移

文件迁移最便捷的办法就是采用rsync来同步了.方便快捷.而且VPS间带宽充足.同步基本按秒记.这也就是VPS的好处.(如果是买的虚拟空间的话, 单文件同步,估计整个人都会不好了).

CentOS采用yum安装rsync,so easy:

    sudo yum install rsync

安装好了rsync之后,只需为相关的项目配置好vhost以及对应目录.然后在源VPS(linode VPS上)采用rsync命令:

    rsync -avz *source_dir* *USER*@*DO_VPS_Host*:*target_dir*
    

回车,刷刷的屏幕滚动,整个世界都安静了!如上把各个项目代码按照此步骤分别完成同步.

### 3\. 数据库迁移

mysql的迁移主要是迁出相关的项目数据库,已经对应的用户及授权.

主要分为两部:

a. 采用mysqldump将各个数据库分别导出到sql文件,然后rsync同步

    mysqldump -u*mysql_admin* -p*mysql_passwd* *db_name* &gt; *target_sql_file_name*
    

b. 将用户及授权导出在新VPS的mysql中完成导入.这里原本想直接按照上面操作导出mysql库,在导入即可.考虑到新mysql中存在例如日志记录的库表冲突问题.参照[Migrate MySQL Databases, Users, and Privileges to Different Server](http://geroldm.com/2012/10/migrate-mysql-databases-users-and-privileges-to-different-server/). 中规中矩的完成了用户及权限的迁移.

至此mysql的迁移就做完了.好像很简单.

### 4\. 相关配置

考虑到VPS上有好几个项目,而且有好几个人分别分管不同的项目.因此在配置各个应用时特意留了个心眼. 将项目同一安置在/www/web目录下.

为每一个项目开设一个ftp帐号,ftp采用TLS认证确保安全(关于FTP的安装和配置参见DO的教程:[How To Configure vsftpd to Use SSL/TLS on a CentOS VPS](https://www.digitalocean.com/community/tutorials/how-to-configure-vsftpd-to-use-ssl-tls-on-a-centos-vps)).

ftp帐号的home目录为对应项目目录.这样不同的参与者管理各自的项目就不会混乱了.同时这里要提醒的一点是关于创建ftp帐号时,考虑到安全性,应该讲账户类型设置为ssh不可登录,只能采用基于FTP的TLS来进行文件传输.相关创建账户命令:

    useradd -d /www/web/*ftp_username* -s /sbin/nologin *ftp_username*
    passwd *ftp_username*

如上便可以创建一个不可直接登录,但能进行ftp访问的用户.so good!!

一切迁移完毕,接下来就进行一些相关的web配置,如vhost配置,.htaccess配置,防盗链配置,缺失模块安装等等.本地绑定IP进行测试,问题逐一排除,确认无误后,dnspod重置解析. 一切都是那么的方便和简单.大赞dnspod提供的免费DNS解析服务和七牛云存储提供的免费CDN服务.开发者的大爱.

OK,基本上也就这些了,有看不懂或不明白的直接留言或者邮件吧.