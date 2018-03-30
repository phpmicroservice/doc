# Server
## 服务器启动类
> 事件列表

* onStart \
主进程开始,**等同于** `\Swoole\Server` 的 `onStart` 事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,\Swoole\Server $swooleServer){

    }

```
* onWorkerStart \
工作进程开始, **类似于** `\Swoole\Server`的 `onWorkerStart` 事件,但是在此事件后会再次产生一个`Task:onWorkerStart`或`Work:onWorkerStart`,指的是不同进程内的事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,int $worker_id){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取

```
* onShutdown \
主进程结束, **等同于** `\Swoole\Server`的 `onShutdown` 事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,\Swoole\Server $swooleServer){

    }
```

* onPipeMessage \
收到管道消息, **类似于** `\Swoole\Server`的 `onPipeMessage` 事件,但是在此事件后会再次产生一个`Task:onPipeMessage`或`Work:onPipeMessage`,指的是不同进程内的事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,array $data = [$src_worker_id,$message]){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取
    # 此函数的第三个参数是一个索引数组,包含 $src_worker_id,$message

```

* onWorkerError \
进程出错, **类似于** `\Swoole\Server`的 `onWorkerError` 事件,但是在此事件后会再次产生一个`Task:onWorkerError`或`Work:onWorkerError`,指的是不同进程内的事件.回调函数原型
```php 
    # 暂不可用,该事件暂不可用
```

* onManagerStart \
当管理进程启动时调用它, **等同于** `\Swoole\Server`的 `onManagerStart` 事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,\Swoole\Server $swooleServer){

    }
```

* onManagerStop \
当管理进程结束时调用它, **等同于** `\Swoole\Server`的 `onManagerStop` 事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server,\Swoole\Server $swooleServer){

    }
```
