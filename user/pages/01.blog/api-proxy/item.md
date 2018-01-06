---
title: 'Api Proxy'
date: '16:59 12/13/2017'
taxonomy:
    category:
        - blog
    tag:
        - 'open source'
author: Abel
---

Api Proxy 是一个适用于 Laravel 框架的简单 API 代理工具包。

===

工作中经常需要转发前端对底层 API 的请求，直接使用 Guzzle 来进行 HTTP 调用太过繁琐，因此我在 Guzzle 的基础上，将常用的一系列方法进一步封装，形成调用更简便、更易用的 Api Proxy 包。



## 特性

### 简化的请求语法

```
ApiProxy::get('blog', ['page' => 2]);
```

### 自动解析响应

Api Proxy 会自动从 Guzzle Response 对象中提取 JSON 字符串，将其解析为 PHP 对象、关联数组或 Laravel JSON Response 对象。

### 自动附加 Authorization HTTP 头

可调用 `authorizationHeader` 方法全局附加 Authorization 头，此后每次请求均会带上 Authorization 头。

```
ApiProxy::authorizationHeader('Bearer 592fed5693d3c5de9396c1f6e00da033');
```

### API 调用日志

开启日志记录之后，Api Proxy 会记录每一次请求。

```Php
ApiProxy::enableLog();
```



## Github

[https://github.com/zxz054321/api-proxy](https://github.com/zxz054321/api-proxy)