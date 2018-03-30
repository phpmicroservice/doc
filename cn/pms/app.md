# App
## 客户端交互的回调处理
> 事件列表

* onConnect \
有新的连接进入时,**等同于** `\Swoole\Server` 的 `onConnect` 事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server, array $data = [$fd,$reactorId]){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取
    # 此函数的第三个参数是一个索引数组,包含 $fd,$reactorId

```

* onReceive \
有新的连接进入时,**类似于** `\Swoole\Server` 的 `onReceive` 事件.回调函数原型
```php 

    function(\Phalcon\Events\Event $event,\pms\Server $server, array $data = [$fd,$reactorId]){

    }
    # 函数的参数没有 \Swoole\Server ,可以通过 $server->swoole_server 来获取
    # 此函数的第三个参数是一个索引数组,包含 $fd,$reactorId

```
