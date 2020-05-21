---
title: "Python中的日志设置与使用"
date: 2020-05-21
categories:
  - Python
tags:
  - highlight code
  - Python
thumbnailImagePosition: left
thumbnailImage: //github.com/zhaoolee/ChineseBQB/blob/master/024Programmer_%E7%A8%8B%E5%BA%8F%E5%91%98%F0%9F%91%A9%F0%9F%8F%BF%E2%80%8D%F0%9F%92%BB%F0%9F%91%A8%F0%9F%8F%BE%E2%80%8D%F0%9F%92%BB%F0%9F%91%A9%F0%9F%8F%BC%E2%80%8D%F0%9F%92%BB%F0%9F%91%A8%F0%9F%8F%BD%E2%80%8D%F0%9F%92%BB%F0%9F%91%A9%F0%9F%8F%BB%E2%80%8D%F0%9F%92%BB%F0%9F%91%A9%F0%9F%8F%BB%E2%80%8D%F0%9F%92%BB%F0%9F%91%A8%E2%80%8D%F0%9F%92%BB%E2%80%8DBQB/Programmer00017.png
---

记录下 Python 中常用的日志相关代码操作。
<!--more-->

<!-- toc -->

# 标准库 logging

{{< codeblock "initlog.py" "python" "initlog.py" >}}
import logging
from logging.handlers import TimedRotatingFileHandler
logpath = "logfilepath"
when = "D" # 按天分割日志
interval = 1
logger = logging.getLogger(logpath)
logger.setLevel(logging.DEBUG)
basicfmt = "%(asctime)s - %(filename)s[line:%(lineno)d] - %(levelname)s:%(message)s"
datefmt = "%Y-%m-%d %H:%M:%S"
formatter = logging.Formatter(basicfmt, datefmt)
chlr = logging.StreamHandler() # 标准输出
chlr.setFormatter(formatter)
chlr.setLevel(conslevel)
fhlr = TimedRotatingFileHandler(logpath,
                                when=when,
                                interval=interval)
fhlr.setFormatter(formatter)
fhlr.setLevel(filelevel)
logger.addHandler(chlr)
logger.addHandler(fhlr)
{{< /codeblock >}}

# loguru
