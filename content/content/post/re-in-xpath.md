---
title: "在xpath中使用正则表达式"
date: 2018-09-03
categories:
  - xpath
tags:
  - highlight code
  - xpath
thumbnailImagePosition: right
thumbnailImage: //d1u9biwaxjngwg.cloudfront.net/highlighted-code-showcase/peak-140.jpg
---
# xpath中使用正则表达式
其实我自己也从来没用到过，在此记录一下，万一以后会用到呢。  
比如有个网站正文部分是： `//*[@id='postmessage_32199']`  
另一个同级别页面的正文是： `//*[@id='postmessage_32153']`  
要抓取这种正文其实可以用xpath： `//*[starts-with(@id, 'postmessage_')]`  
或者 `//*[contains(@id, 'postmessage_')]`  
也可以选择在xpath中使用正则表达式：`doc.xpath(r'//*[re:match(@id, "postmessage_\d+")]', namespace={"re": "http://exslt.org/regular-expressions"})`
