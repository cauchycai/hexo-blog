---
layout: post
title: "PHP单元测试 - 一个例子"
description: ""
category: tutorial
tags: [php, testing, tutorial]
---

本文使用PHPUnit作为测试框架，以一个实际的例子来演示一些单元测试的编写方法。

### 测试代码放在哪？ ###

### 开始写代码 ###

这里要实现的功能是一个商城下单的程序。添加如下源代码和它对应的测试代码：

`mall/code/app/lib/Order.php => mall/tests/app/lib/OrderTest.php`

1. 首先编写Order.php, 定义好这个类的public方法：

```PHP
<?php
namespace Mall;

class Order
{
    public function placeOrder() { }
    public function addOrderItem(OrderItem $orderItem) { }
}
```

```PHP
namespace Mall;

class OrderItem
{
    public function __construct($productId, $quantity) { }
}
```
placeOrder 是实际下单逻辑的调用，如果成功则返回订单id。

addOrderItem 用来添加订单项。

2. 编写测试

```PHP
<?php

use \Mall\Order;
use \Mall\OrderItem;

class OrderTest extends PHPUnit\_Framework\_TestCase
{
    public function testPlaceOrderWorks();
}
```
