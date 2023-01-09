---
title: PHP8特性
date: 2023-01-01
description: php8新特性，mixed类型、match表达式、nullsafe运算符
keywords: Git|命令|处理分支|更改URL
tags:
  - PHP8
categories:
  - PHP
---

## 新mixed类型包含一下任何类型

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

## nullsafe运算符

```php
$user?->user?->getUserInfo()?->info;
```

## Match表达式
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

## ::class

```php
$class = new Class();

$class::class;
```

## 联合类型

```php
public function foo(Foo|Bar $foo): int|float
public function bar(?Bar $bar): void;
```