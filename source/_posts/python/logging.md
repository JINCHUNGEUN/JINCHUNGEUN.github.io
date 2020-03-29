---
title: Python's logging module
date: 2020-03-28 16:46:52
tags:
- python
---

<em>这篇文章不会详细讲logging的各个功能，详细的可以参考[官方文档](https://docs.python.org/2/howto/logging.html)，官方文档写的已经很详细了，虽然是用英文写的，但是词汇都是简单的词汇。本篇涉及到的内容都是个人认为比较重要的知识点，望不要吐槽~~</em>

概念：Python的logging模块是用来打印日志信息便于追踪代码运行情况的工具。可以用不同的级别(严重性)来表达事件信息，有低到高有 debug()、info()、warning()、error()、critical()。  

刚接触python不久，都会有疑问，什么时候用logging，什么时候用print，官方给了一些建议，如下：

|要打印的日志信息|建议|
|:-------------------: |:-------:|
|打印命令行工具或程序的用途到控制台|print()|
|程序运行期间的事件信息(比如状态监控或者错误检查)|使用logging.info()或者logging.debug()来打印详细信息|
|上报关于特定运行期间的警告事件|logging.warning()|
|上报关于特定运行期间的错误事件|Raise an exception|
|无需抛出异常，只需打印错误信息|logging.warning()、loggin.error()、logging.critical()|

在简单说明一下logging的各个日志级别的使用场景：

|级别|场景|
|:--:|:--:|
|DEBUG|仅仅用于开发阶段调试目的，线上环境应该避免出现debug日志|
|INFO|确认代码正常运行|
|WARNING|在程序某处有意外发生|
|ERROR|程序错误|
|CRITICAL|严重错误，程序无法继续运行|



### 四个重要概念(一定要搞明白这四个概念)

- loggers：给应用程序代码提供接口
- handlers：接收loggers传递过来的日志记录，转发到相应的目的地，包括流，文件，socket地址等等
- filters：日志筛选
- formatters：日志格式

### Logging flow

![](./logging/logging-flow.png)
