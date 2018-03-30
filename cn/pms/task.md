# Task
## 任务进程回调处理
> 事件列表

* onTask \
新任务接入, **等同于** `\Swoole\Server`的 `onTask` 事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,$data = [$task_id,$src_worker_id,$data]){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取
    # 此函数的第三个参数是一个索引数组,包含 $src_worker_id,$data

```


* onWorkerStart \
工作进程开始, **类似于** `\Swoole\Server`的 `onWorkerStart` 事件,但是在此事件在`Server:onWorkerStart`之后产生,是Task进程内的事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,int $worker_id){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取

```

* onPipeMessage \
收到管道消息, **类似于** `\Swoole\Server`的 `onPipeMessage` 事件,但是在此事件在`Server:onPipeMessage`之后产生,是Task进程内的事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,array $data = [$src_worker_id,$message]){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取
    # 此函数的第三个参数是一个索引数组,包含 $src_worker_id,$message

```
