# Playcat queue简介
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
