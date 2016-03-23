title: How to update the repo from the Fork Github
tags: []
date: 2015-08-13 17:16:43
---

I can’t use Google engine that it search something more professional and targeted than Baidu because of the GFW (Great Firewall of China). The good news is the goagent is very good tool to help me walk out of the mud puddle.

<!-- more -->

I clone the repo from github. [https://github.com/goagent/goagent](https://github.com/goagent/goagent)

It is so convenient, You just need the follow the guide: [https://github.com/goagent/goagent/blob/wiki/InstallGuide.md](https://github.com/goagent/goagent/blob/wiki/InstallGuide.md)

What I want to introduce in this article as the title, so the detail about how to build and config the goagent will be ignore. What i wanted is when i fork the goagent repo to mine, and I clone the repo from my github repo. Then I change the `goagent/local/proxy.ini`. After some days, I want to update the repo from the fork origin.The following steps from [stackoverflow.com](http://stackoverflow.com/questions/15738604/update-the-fork-github) will help me.

    # git remote add parentrepo &lt;url&gt;;
    # git fetch parentrepo 

after update,you can push to your repo

    # git push -u origin {branch_name}

that’s all!