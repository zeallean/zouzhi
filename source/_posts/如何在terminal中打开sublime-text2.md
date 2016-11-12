---
layout: post
title: 如何在terminal中打开sublime text2 ?
tags: [sublime]
date: 2015-08-13 17:44:38
---

Mac的话：

    ln -s '/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl' /usr/local/bin/sublime

或者用`alias`也可以：

    alias sublime='open -a "Sublime Text 2"'

推荐第二种,打开时命令行不会有其他警告输出

来源:[Ruby China](https://ruby-china.org/topics/1033)