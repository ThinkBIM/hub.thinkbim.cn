---
title: PHP面向对象面试题
date: 2022-11-07 10:59:31
description:
keywords: PHP面试题|面向对象|单例
tags:
  - OOP
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


