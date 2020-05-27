+++
title = "Python 日志常用配置代码记录"
author = ["Jack Deng"]
date = 2020-05-26T00:00:00+08:00
tags = ["Python", "logging"]
categories = ["Python代码"]
draft = false
+++

## Python 日志常用配置代码记录 {#python-日志常用配置代码记录}

条件允许，能用 loguru 就用 loguru 吧，方便好使！
<!--more-->


### 标准库 logging {#标准库-logging}

```python
import logging
from logging.handlers import TimedRotatingFileHandler

logpath = "logging file path"
logger = logging.getLogger(logpath)
logger.setLevel(logging.DEBUG)
basicfmt = "%(asctime)s - %(filename)s[line:%(lineno)d] - %(levelname)s:%(message)s"
datefmt = "%Y-%m-%d %H:%M:%S"
formatter = logging.Formatter(basicfmt, datefmt)
chlr = logging.StreamHandler()
chlr.setFormatter(formatter)
chlr.setLevel(conslevel)
fhlr = TimedRotatingFileHandler(logpath,
                                when=when,
                                interval=interval)
fhlr.setFormatter(formatter)
fhlr.setLevel(filelevel)
logger.addHandler(chlr)
logger.addHandler(fhlr)
```


### loguru {#loguru}

```python
from loguru import logger

# No Handler, no Formatter, no Filter: one function to rule them all
logger.add(sys.stderr, format="{time} {level} {message}", filter="my_module", level="INFO")
logger.debug("That's it, beautiful and simple logging!")

logger.add("file_1.log", rotation="500 MB")    # Automatically rotate too big file
logger.add("file_2.log", rotation="12:00")     # New file is created each day at noon
logger.add("file_3.log", rotation="1 week")    # Once the file is too old, it's rotated

logger.add("file_X.log", retention="10 days")  # Cleanup after some time

logger.add("file_Y.log", compression="zip")    # Save some loved space

logger.info("If you're using Python {}, prefer {feature} of course!", 3.6, feature="f-strings")

@logger.catch
def my_function(x, y, z):
    # An error? It's caught anyway!
    return 1 / (x + y + z)

# Pretty logging with colors
logger.add(sys.stdout, colorize=True, format="<green>{time}</green> <level>{message}</level>")

# All sinks added to the logger are thread-safe by default.
# They are not multiprocess-safe, but you can enqueue the messages to ensure logs integrity.
# This same argument can also be used if you want async logging.
logger.add("somefile.log", enqueue=True)
```
