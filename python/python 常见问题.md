* 解决 Conda SSLError 问题

  >  https://slproweb.com/products/Win32OpenSSL.html 下载 OpenSSL 的 Windows 安装包.当 “安装 DLL 到 System 目录” 的选项出现时,
  > 勾选它

* Python 2.7中文显示与处理

  > \# coding=utf-8  #第一行添加，以下8种写法，默认ascii编码所以要重定义编码格式以支持中文
  >
  > \# coding= utf-8
  >
  > \# encoding=utf-8
  >
  > \# encoding= utf-8
  >
  > \# -*- coding: utf-8 -*-
  >
  > \# -*- coding:utf-8 -*-
  >
  > \# -*- encoding: utf-8 -*-
  >
  > \# -*- encoding:utf-8 -*-

* 解决ConfigParser解析中文问题

  > cfg = ConfigParser()
  >
  > cfg.readfp(codecs.open('config.ini', "r", "utf-8-sig"))