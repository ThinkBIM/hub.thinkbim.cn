---
title: PHP面试题汇总
date: 2023-04-18
description: 
keywords: PHP面试题
tags:
  - PHP
  - 面试题
categories:
  - 面试题
top_img:
cover:
---

## PHP
### RabbitMQ 基于AMQP协议的消息中间件

#### 如何确保消息正确地发送至RabbitMQ？
RabbitMQ使用发送方确认模式，确保消息正确地发送到RabbitMQ。
发送方确认模式：将信道设置成confirm模式（发送方确认模式），则所有在信道上发布的消息都会被指派一个唯一的ID。
一旦消息被投递到目的队列后，或者消息被写入磁盘后（可持久化的消息），
信道会发送一个确认给生产者（包含消息唯一ID）。
如果RabbitMQ发生内部错误从而导致消息丢失，会发送一条nack（not acknowledged，未确认）消息。
发送方确认模式是异步的，生产者应用程序在等待确认的同时，可以继续发送消息。
当确认消息到达生产者应用程序，生产者应用程序的回调方法就会被触发来处理确认消息。

#### 如何确保消息接收方消费了消息？
接收方消息确认机制：消费者接收每一条消息后都必须进行确认（消息接收和消息确认是两个不同操作）。只有消费者确认了消息，RabbitMQ才能安全地把消息从队列中删除。这里并没有用到超时机制，RabbitMQ仅通过Consumer的连接中断来确认是否需要重新发送消息。也就是说，只要连接不中断，RabbitMQ给了Consumer足够长的时间来处理消息

#### 消息队列的作用与使用场景？
- 异步：批量数据异步处理（批量上传文件）
- 削峰：高负载任务负载均衡（电商秒杀抢购）
- 解耦：串行任务并行化（退货流程解耦）
- 广播：基于Pub/Sub实现一对多通信

#### 使用了消息队列会有什么缺点?
- 1.系统可用性降低:你想啊，本来其他系统只要运行好好的，那你的系统就是正常的。现在你非要加个消息队列进去，那消息队列挂了，你的系统不是呵呵了。因此，系统可用性降低
- 2.系统复杂性增加:要多考虑很多方面的问题，比如一致性问题、如何保证消息不被重复消费，如何保证保证消息可靠传输。因此，需要考虑的东西更多，系统复杂性增大

### PHP垃圾回收
php中的变量存储在变量容器zval中，zval中除了存储变量类型和值外，还有is_ref和refcount字段。
refcount表示指向变量的元素个数，is_ref表示变量是否有别名。如果refcount为0时，就回收该变量容器。
如果一个zval的refcount减1之后大于0，它就会进入垃圾缓冲区。当缓冲区达到最大值后，回收算法会循环遍历zval，判断其是否为垃圾，并进行释放处理

### thinkphp6框架运行流程
应用入口 /index.php `>>` 注册加载 autoload.php `>>` 初始化 think\App `>>` Http::run()

### 正则
- 邮箱 
```
/^[_a-z0-9-]+(\.[_a-z0-9-]+)*@[a-z0-9-]+(\.[a-z0-9-]+)*(\.[a-z]{2,3})$/
```
- URL
```
/^(http|https):\/\/[a-z0-9]+\.[a-z0-9]+[\/=\?%\-&_~`@[\]\’:+!]*([^<>\”])*$/
```

### 排序

#### 冒泡排序
```php
function bubbleSort($arr) {
    $len = count($arr);
    for ($i = 0; $i < $len - 1; $i++) {
        for ($j = 0; $j < $len - 1 - $i; $j++) {
            if ($arr[$j] > $arr[$j+1]) {
                $tmp = $arr[$j];
                $arr[$j] = $arr[$j+1];
                $arr[$j+1] = $tmp;
            }
        }
    }
    return $arr;
}
```
#### 快速排序
```php
function quickSort($arr) {
    if (count($arr) <= 1)
        return $arr;
    $middle = $arr[0];
    $leftArray = [];
    $rightArray = [];
    for ($i = 1; $i < count($arr); $i++) {
        if ($arr[$i] > $middle)
            $rightArray[] = $arr[$i];
        else
            $leftArray[] = $arr[$i];
    }
    $leftArray = quickSort($leftArray);
    $rightArray = quickSort($rightArray);
    return array_merge($leftArray, [$middle],$rightArray);
}
```
#### 插入排序
```php
function insertionSort($arr) {
    $len = count($arr);
    for ($i = 1; $i < $len; $i++) {
        $preIndex = $i - 1;
        $current = $arr[$i];
        while($preIndex >= 0 && $arr[$preIndex] > $current) {
            $arr[$preIndex+1] = $arr[$preIndex];
            $preIndex--;
        }
        $arr[$preIndex+1] = $current;
    }
    return $arr;
}

```

### 状态码
- 200 请求已成功，请求所希望的响应头或数据体将随此响应返回。
- 301 被请求的资源已永久移动到新位置。
- 302 请求的资源现在临时从不同的 URI 响应请求。
- 400 语义有误，当前请求无法被服务器理解。2、请求参数有误。
- 401 当前请求需要用户验证。
- 403 服务器已经理解请求，但是拒绝执行它。
- 404 请求失败，请求所希望得到的资源未被在服务器上发现。
- 500 服务器遇到了一个未曾预料的状况，无法完成对请求的处理，会在程序码出错时出现。
- 501 服务器不支持当前请求所需要的某个功能。无法识别请求的方法。
- 502 作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到无效的响应。
- 503 由于临时的服务器维护或者过载，服务器当前无法处理请求。

## Redis

### redis事务的乐观锁和悲观锁是怎样的？
- 悲观锁
每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会被阻塞，直到它拿到锁。
- 乐观锁
每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号等机制。乐观锁适用于多读的应用类型，这样可以提高吞吐量

## MySQL
### 日志
主要包括错误日志、查询日志、慢查询日志、事务日志、二进制日志几大类。其中，比较重要的还要属二进制日志 binlog（归档日志）和事务日志 redo log（重做日志）和 undo log（回滚日志）
- `redo log` 通常是物理日志，记录的是数据页的物理修改，确保事务的持久性。防止在发生故障的时间点，尚有脏页未写入磁盘，在重启mysql服务的时候，根据redo log进行重做，从而达到事务的持久性这一特性。
- `undo log` 用于事务失败时的回滚操作。undo log一般是逻辑日志，根据每行记录进行记录。
- `binlog` 二进制日志，用于在主从复制中，从库利用主库上的binlog进行重播，实现主从同步。

### 主从同步数据不一致
查看show slave status 中
- Relay_Master_Log_File 当前slave SQL线程读取并执行的relay log的文件中，对应的主服务器二进制日志文件的名称
- Read_Master_Log_Pos 当前I/O线程正在读取的二进制日志的位置。
- Relay_Log_Pos  当前slave SQL线程正在读取并执行的relay log文件中的位置

### 数据类型
 - datatime
以 YYYY-MM-DD HH:MM:SS 格式存储时期时间，精确到秒，占用8个字节得存储空间，datatime类型与时区无关 
 - timestamp 
以时间戳格式存储，占用4个字节，范围小1970-1-1到2038-1-19，显示依赖于所指定得时区，默认在第一个列行的数据修改时可以自动得修改timestamp列得值 
 - date（生日）
占用得字节数比使用字符串.datatime.int储存要少，使用date只需要3个字节，存储日期月份，还可以利用日期时间函数进行日期间得计算 
 - time 
存储时间部分得数据 注意:不要使用字符串类型来存储日期时间数据（通常比字符串占用得储存空间小，在进行查找过滤可以利用日期得函数） 

`使用int存储日期时间不如使用timestamp类型`

### 查看表中定义的所有索引&如何监测MySQL是否命中索引？
```sql
show index from test_name;
explain select * from test_name;
```

### 锁
共享锁
拍他说

## Liunx

### crontab 命令
分 时 日 月 周

### 负载均衡
轮询
权重  weight
ip_hash


# 参考
[https://www.shuzhiduo.com/A/D854YrY2dE/](https://www.shuzhiduo.com/A/D854YrY2dE/)
[https://baijiahao.baidu.com/s?id=1718316080906441023&wfr=spider&for=pc](https://baijiahao.baidu.com/s?id=1718316080906441023&wfr=spider&for=pc)
[https://www.hi-linux.com/posts/34936.html](https://www.hi-linux.com/posts/34936.html)