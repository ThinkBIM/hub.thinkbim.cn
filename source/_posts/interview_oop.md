---
title: PHP面向对象面试题
date: 2022-11-07 10:59:31
description:
keywords: PHP面试题|面向对象|单例
tags:
  - OOP
  - 面试题
categories:
  - 面试题
top_img:
cover:
---

## 静态类static和self区别
- {% label static::class orange %}  如果有继承的话 默认调用子类 ，否则调用的是自身
- {% label self::class orange %}    如果有继承的话，默认调用父类，否则调用自身


## 单例
```php
class Singleton
{
    private static $instances = [];

    protected function __construct() { }

    protected function __clone() { }

    public function __wakeup()
    {
        throw new \Exception("Cannot unserialize singleton");
    }

    public static function getInstance()
    {
        $subclass = static::class;
        if (!isset(self::$instances[$subclass])) {
            self::$instances[$subclass] = new static();
        }
        return self::$instances[$subclass];
    }
}
```



## 魔术方法
![图片1.png](https://s2.loli.net/2022/11/07/ZHWxuCqgAvF8fXL.png)

## 魔术方法
- `construct` 构造函数
- `destruct` 析构函数
- `call` 在对象中调用一个不可访问方法时调用
- `callStatic` 用静态方式中调用一个不可访问方法时调用
- `get` 获得一个类的成员变量时调用
- `set` 设置一个类的成员变量时调用
- `isset` 当对不可访问属性调用isset()或empty()时调用
- `unset` 当对不可访问属性调用unset()时被调用
- `sleep` 执行serialize()时，先会调用这个函数
- `wakeup` 执行unserialize()时，先会调用这个函数
- `toString` 类被当成字符串时的回应方法
- `invoke` 调用函数的方式调用一个对象时的回应方法
- `clone` 当对象复制完成时调用
- `debugInfo` 打印所需调试信息
