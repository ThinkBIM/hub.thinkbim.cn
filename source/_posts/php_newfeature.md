---
title: PHP7、8新特性
date: 2023-01-01
description: php8新特性，mixed类型、match表达式、nullsafe运算符
keywords: php8|php7|php新特性
tags:
  - PHP8
  - PHP7
categories:
  - PHP
top_img: false
cover: false
---
php7、php8新特性，包含标量、返回值声明，运算符，Match表达式，JIT，构造器等

## PHP7新特性

### 标量类型声明

```php
function foo(int ...$param) {}
```

### 返回值类型声明

```php
function foo(int ...$param): int {}
```

### 合并运算符

```php
$arr = $param['name'] ?? 'nobody';
$arr = $param['name'] ?: 'nobody';
```
### 组合比较符

```php
//大于、等于、小于时，分别返回-1、0、1。
1 <=> 2
```

### 通过 define() 定义常量数组

```php
define('CONST', [1,3,4]);
```

### use 加强

```php
use namespace\{ClassA, ClassB, ClassC as C};
```

### 整除函数 
- intdiv()




## PHP8新特性

### 新mixed类型包含一下任何类型

- array
- bool
- callable
- int
- float
- null
- object
- resource
- string


```php
public function bar(): mixed {}
```

### nullsafe运算符

```php
$user?->user?->getUserInfo()?->info;
```


### 字符串函数
- str_contains() 确定字符串是否包含指定子串
- str_starts_with() 检查字符串是否以指定子串开头
- str_ends_with() 检查字符串是否以指定子串结尾


### Match表达式

match 表达式基于值的一致性进行分支计算。 match表达式和 switch 语句类似， 都有一个表达式主体，可以和多个可选项进行比较。 与 switch 不同点是，它会像三元表达式一样求值。
与 switch 另一个不同点，它的比较是严格比较（`===`）而不是松散比较（`==`）

```php
$food = 'cake';

$return_value = match ($food) {
    'apple' => 'This food is an apple',
    'bar' => 'This food is a bar',
    'cake' => 'This food is a cake',
};

var_dump($return_value); //string(19) "This food is a cake"
```

### 可以在对象上使用 ::class

```php
$class = new Class();

$class::class; // 等同 get_class()
```

### 联合类型

```php
public function foo(Foo|Bar $foo): int|float
public function bar(?Bar $bar): void;
```

### JIT

JIT作为PHP底层编译引擎


### 构造器属性提升

```php
class Money 
{
    public function __construct(
        public Currency $currency,
        public int $amount,
    ) {}
}
```