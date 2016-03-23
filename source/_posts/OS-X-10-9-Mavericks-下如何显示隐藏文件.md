title: OS X 10.9 Mavericks 下如何显示隐藏文件
tags: []
date: 2015-08-13 17:21:42
---

在MAC中,我们通常需要针对一些系统隐藏文件(通常以.开头文件名)进行查看和操作.同Win下,默认系统对这些文件是保护和隐藏的.在MAC OS X 10.9 Mavericks 中可以通过如下命令实现隐藏文件的显示与隐藏.

<!-- more -->

    defaults write com.apple.finder AppleShowAllFiles Yes && killall Finder //显示隐藏文件
    defaults write com.apple.finder AppleShowAllFiles No && killall Finder //不显示隐藏文件
    