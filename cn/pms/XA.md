# 全局事务/多服务事务/分布式事务

&nbsp; &nbsp; &nbsp; &nbsp;框架的全局事务采用事务协调器协调,异步执行,因涉及到多服务的协调通讯较多,一个事务的完成时间大约为0.7秒-3秒,多事务并行,并行运行能力取决于事务相关服务并行处理能力最小的服务.

## 事务task的编写
 &nbsp; &nbsp; &nbsp; &nbsp;事务的task一般为一个单独的类,这里面包含了事务的逻辑,事务协调工作在事务task基类中已经定义,集成TxTask基类即可,实例如下:

~~~php
<?php

namespace app\task;

use app\model\tmdemo;
use pms\Task\TaskInterface;

class AdemoTx extends \pms\Task\TxTask implements TaskInterface
{

    public function end()
    {

    }
    /**
     * 在依赖处理之前执行,没有返回值
     */
    protected function b_dependenc()
    {
        $data = $this->trueData;
        $this->add_dependenc('article', 'demo', $data['data']);
    }

    /**
     * 事务逻辑内容,返回逻辑执行结果,
     * @return bool false失败,将不会再继续进行;true成功,事务继续进行
     */
    protected function logic(): bool
    {
        $data = $this->trueData;
        $md = new tmdemo();
        $ere = $md->save($data['data']);
        return $ere;

    }

}

~~~

 &nbsp; &nbsp; &nbsp; &nbsp; 如上实例,这是一个事务task类,应存放于 *app\task* 命名空间之下,pms框架的task机制会自动找到这个类

 > add_dependenc 添加事务依赖方法  

 &nbsp; &nbsp; &nbsp; &nbsp; 方法原型
 ~~~php
 add_dependenc(string  $servername, string $txname,array $data)
 ~~~
* $servername 服务的名字
* $txname 事务的名字
* $data 事务所需的数据



## 事务的使用

&nbsp; &nbsp; &nbsp; &nbsp;事务的启动就是将事务发送到task任务中,实例如下:  

```php

$task_data = [
    'name' => ucfirst('ademo') . 'Tx',
    'data' => [
        'name'=>time(),
        'title' => uniqid()
    ],
    'tx_name' => 'ademo'
];
$connect = $this->counnect;
$this->swoole_server->task($task_data, -1, function ($ser, $wid, $re) use ($connect) {
    var_dump($re);
    $connect->send_succee($re);
});

```

> &nbsp; &nbsp; &nbsp; &nbsp;以上代码是在控制器中的,__*$taskdata*__ 的内容可参考"task使用"章节,具体 *data* 部分的就是这个事务所需要的数据,在事务内使用




## 服务内调度控制器

~~~php


<?php

namespace app\controller;

/**
 * 事务控制器
 * Class Transaction
 * @package app\controller
 */
class Transaction extends \app\Controller
{
    public function create()
    {
        var_dump(1414.3);
        $name = $this->getData('name');
        $data = $this->getData('data');
        $xid = $this->getData('xid');
        $class_name='app\\task\\'.ucfirst($name).'Tx';
        var_dump($class_name);
        if(!class_exists($class_name)){
            $this->send('class_not_exists');
        }
        $task_data=[
            'xid'=>$xid,
            'name'=>ucfirst($name).'Tx',
            'data'=>$data
        ];
        $re = $this->swoole_server->task($task_data, -1);
        var_dump($re);
        $this->send(true);
    }

}


~~~

> 以上是服务内的调度控制器,负责处理事务调度服务发出的事务创建请求






