title: 更改windows下的cmd的字符集编码
tags: []
date: 2015-08-13 02:06:03
---

在window下做golang的开发时，由于golang全部采用utf8编码。因此需要将基础教程学习的开发测试所用到cmd环境需要进行字符编码的设定（原生的编码为：936 ANSI 简体中文）。

通过下面的cmd指令便可以更改windows下的cmd的字符集编码

    chcp 437 /* 英文*/   

    chcp 932 /* 日文*/ 

    chcp 936 /* 简体中文*/ 

    chcp 949 /* 韩文*/ 

    chcp 950 /* 繁体中文*/ 

    chcp 65001 UTF-8 
    