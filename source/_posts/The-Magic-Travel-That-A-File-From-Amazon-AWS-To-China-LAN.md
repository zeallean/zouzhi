title: The Magic Travel That A File From Amazon AWS To China LAN
tags: []
date: 2015-08-13 17:22:56
---

Do you know anything about the ‘China LAN’? If don’t,Just open your browser and download something from [amazon aws](http://aws.amazon.com).

<!-- more -->

‘What a F**k’, I just want to say!

The following chapter is about my experience download a template(bought from [ThemeForest](http://themeforest.net/item/metronic-responsive-admin-dashboard-template/4021469)) that hosted on AWS.(PS: I’m just a Netizen from china LAN)

## How to climb out GFW

### Part I:

I log in ThemeForest,and goto the download tab. After click the download link, The download be guided to aws,the link like this:

[`https://s3.amazonaws.com/marketplace-downloads.envato.com/files/126941645/metronic_v3.7.zip?AWSAccessKeyId=AKIAJYG5ROGJ6X7Z3M6Q&amp;amp;Expires=1429197496&amp;amp;Signature=2pq1Z1VUGoLNnvWG4qbPBgpypvo%3D&amp;amp;response-content-disposition=attachment%3B+filename%3Dthemeforest-4021469-metronic-responsive-admin-dashboard-template.zip`](https://s3.amazonaws.com/marketplace-downloads.envato.com/files/126941645/metronic_v3.7.zip?AWSAccessKeyId=AKIAJYG5ROGJ6X7Z3M6Q&amp;Expires=1429197496&amp;Signature=2pq1Z1VUGoLNnvWG4qbPBgpypvo%3D&amp;response-content-disposition=attachment%3B%20filename%3Dthemeforest-4021469-metronic-responsive-admin-dashboard-template.zip)

From the url,there are some key argument for the resource access control.If you don’t have any agent,eg: `goagent`,`openvpn`,`shadowsocks`. Maybe what the result that browser give to you is just ‘Ops,The link is error……..’ or whatever. It is caused by the powerful GFW in China LAN.

Fortunately! I have my `Shadowsocks` server founded by `SUZHOU GDG` and VPS bought from DigitalOcean.The download link redirect normally,and the file is download begin. But the speed is 0~5kb/s…. And the file size is 300MB!

### Part II:

I can’t endure the long long waiting.I logon in my vps and got the file by

    $ wget **the download link with sign and access key**

Wow! the speed is almost 3Mb/s. I got my file less than 1 min. But I must download the file to my local disk.Not the vps. So I try to use the lszrz tool of linux to got it.

    $ sz metronic_v3.7.zip

Unfortunately.The speed is limited. Orz! How can I get my treasure file.

### Part III:

Maybe I can use the Cloud Disk Server service,such as: `BaiduYun`. Search from the google ‘VPS 百度云’. I got this [`bpcs_uploader`](https://github.com/oott123/bpcs_uploader).

Follow the README. I upload the file to my `Baidu Cloud Disk`.Then I download it from the cloud disk.(The upload speed is 125~200kb/s, and download speed from cloud disk is 3~5Mb/s.

### Part IIII:

The travel of the file is so memorable and the experience is so meaningful. So I must try my best to write the procedure in English. (I think there are nobody will read to here)