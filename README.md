# 简介
 PHP下有很多队列的实现,包括但不局限于webman/queue,think/queue,multi/process/queue等,之所以开发Playcat queue是因为现有的模块各有各的局限性,而事实上队列系统是一个很常规的基础服务,功能不要求很复杂,但至少需要保证数据的可靠和服务的稳定,同时又能方便扩展。
 以此为契机,结合工作需求,才有了本项目.没错,本队列服务已经是在生产环境使用了。

# 选型
Playcat queue目前有2种实现

基于tp和swoole的队列系统
[playcat-queue-tpswoole](https://github.com/nsnake/playcat-queue-tpswoole)

基于webman的队列系统
[playcat-queue-webman](https://github.com/nsnake/playcat-queue-webman)

这2种各有特点.

playcat-queue-webman适合CPU密集型的业务,例如数据处理,视频转码,图片处理等。因为多进程可以充分利用CPU的性能，而且相对开发难度更低.依托于webman的可靠性,就算是进程异常退出也能重新启用新的进程。

playcat-queue-tpswoole适合IO密集型的业务,比如爬虫,短信发送等。以为利用了swoole的协程,一个进程中可以有多个协程序,所以可以用更少的进程处理更多的请求.

# 案例(todo:)


# 生产者实现
目前只实现了php的生产者,其它语言的可以由自己实现
队列中存储的是经过msgpack序列化的数据。
数据格式必须包括以下字段:

| 字段 | 说明 | 类型|
|--------|--------|--------|
|    id  |消息的唯一标识|string|
|channel|任务对应的通道名称|string|
|creattime|创建时间(秒)|int|
|retrycount|已重试次数|int|
|delaytime|重试间隔时长(秒)|int|
|queuedata|提供给消费服务使用的数据|array,hash|


# 鸣谢
webman: 设计思路起源webman/queue
