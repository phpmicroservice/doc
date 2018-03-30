# Worker
## 工作进程回调处理
> 事件列表

* onFinish \
task_worker中完成时,**等同于** `\Swoole\Server` 的 `onFinish` 事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server, array $data = [$task_id,$data]){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取
    # 此函数的第三个参数是一个索引数组,包含 $task_id,$data

```

* onWorkerStart \
工作进程开始, **类似于** `\Swoole\Server`的 `onWorkerStart` 事件,但是在此事件在`Server:onWorkerStart`之后产生,是Work进程内的事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,int $worker_id){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取

```

* onWorkerStop \
当工作进程停止, **等同于** `\Swoole\Server`的 `onWorkerStop` 事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,int $worker_id){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取

```
* onWorkerExit \
当工作进程要退出, **等同于** `\Swoole\Server`的 `onWorkerExit` 事件. 
**主要用户停止新请求,完成已有请求** 
回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,int $worker_id){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取

```


* onPipeMessage \
收到管道消息, **类似于** `\Swoole\Server`的 `onPipeMessage` 事件,但是在此事件在`Server:onPipeMessage`之后产生,是Work进程内的事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,array $data = [$src_worker_id,$message]){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取
    # 此函数的第三个参数是一个索引数组,包含 $src_worker_id,$message

```
