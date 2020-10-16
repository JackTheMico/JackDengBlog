+++
title = "ELK报错日志与后续优化"
author = ["Jack Deng"]
date = 2020-06-01T00:00:00+08:00
tags = ["ELK", "logging"]
categories = ["ELK"]
draft = false
+++

记录下ELK 相关的错误日志与处理、优化方法。
<!--more-->


## Elasticsearch 警告、错误日志 {#elasticsearch-警告-错误日志}

1.  <span class="timestamp-wrapper"><span class="timestamp">[2020-05-29 五]</span></span>[WARN ][o.e.m.j.JvmGcMonitorService] ... overhead, spent [670ms] collecting in the last [1s]
    该日志是由于垃圾回收时间过长产生的，ES 内存使用和GC指标默认情况下，主节点每30秒会去检查其他节点的状态，如果任何节点的垃圾回收时间超过30秒（Garbage collection duration），则会导致节点脱离集群。解决方案：通过增加ping\_timeout的时间，和增加ping\_retries的次数来防止节点错误的脱离集群，可以使节点有充足的时间进行full GC。

    ```dot
         discovery.zen.fd.ping_timeout: 1000s
         discovery.zen.fd.ping_retries: 10
    ```

    [参考链接](https://my.oschina.net/u/3625378/blog/1793796)

2.  <span class="timestamp-wrapper"><span class="timestamp">[2020-05-29 五]</span></span>[WARN ][o.e.c.r.a.DiskThresholdMonitor] [node-26] high disk watermark <code>[90%]</code> ......, shards will be relocated away from this node
    节点机器磁盘空间不足了，可以通过监控此日志中出现的关键字来及时告警。

3.  ... org.elasticsearch.transport.RemoteTransportException: [node-123][xx.xxx.xxx.xxx:9200]
    表明 node 123 这个节点出现了问题，需要及时检查并处理


## Logstash 警告、错误日志 {#logstash-警告-错误日志}

1.  [INFO ]... Retrying individual bulk actions that failed or were rejected by the previous bulk request.
    Elasticsearch 节点出现问题导致 logstash 无法插入数据时会出现此日志，后续可以监控此日志中的关键字来进行及时告警通知。
2.  此外，出现 1 中的情况后，在重启 logstash 时可能会出现 logstash 依然在不断地重试之前错误的请求而导致无法正常工作的情况，此时删除 "--path.data" 参数对应目录中的文件，再重启 logstash 即可使其正常工作。
