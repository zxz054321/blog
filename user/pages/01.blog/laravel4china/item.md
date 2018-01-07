---
title: 'Laravel 中国版'
date: '17:35 08/26/2016'
taxonomy:
    category:
        - blog
    tag:
        - 'open source'
author: Abel
---

Laravel 中国版是更符合国情、更适合作为新项目基石的中国版 Laravel

===

## 主要特性

1. 基于 Laravel 5.4 （版本选择的原则是：最新的稳定）
2. Laravel 安装器可一键安装框架依赖、一键执行优化、自动设置符号链接以及自动设置权限
3. Node 模块安装器可一键安装 Laravel Mix 并执行 Mix 任务
4. 自动生成 APP_KEY
5. 内置中文语言包
6. 时区默认为中国上海
7. 更优秀的 IDE 代码提示
8. .gitignore 忽略 IDE 相关文件
9. 演示页面去除 Google 字体引用

## Laravel 安装器

此安装器脚本针对 Ubuntu 系统编写，可自动完成以下操作：

1. 全局安装 PHP Composer
2. 复制 `.env` 文件
3. 执行 `composer install --no-dev` 安装依赖
4. 执行 `php artisan key:generate` 生成App key
5. 执行优化
6. 创建符号链接（将` public/storage` 目录链接去 `storage/app/public`目录）
7. 设置应用目录用户为 `www`
8. 赋予 `bootstrap/cache` 目录和 `storage` 目录读写权限

### 使用方法

在应用根目录下执行命令：

```
sudo chmod 777 install.sh && ./install.sh
```

### 参数说明

| 参数   | 说明                                       |
| ---- | ---------------------------------------- |
| -q   | 安静模式，脚本将静默执行，适用于自动部署的场景                  |
| -e   | （安静模式下必填）指定 env 文件。示例： `-e .env.example` |
| -k   | （可选）执行 `php artisan key:generate`        |
| -o   | （可选）执行 autoload、路由、配置优化                  |

## Node 模块安装器

此安装器脚本针对 Ubuntu 系统编写，可自动完成以下操作：

1. 全局安装 Node.js v6.x LTS
2. 设置 npm 使用淘宝镜像，大大提高下载速度
3. 安装 Laravel Mix
4. 执行 `npm run production` 编译前端资源

### 使用方法

在应用根目录下执行命令：

```
sudo chmod 777 install-node.sh && ./install-node.sh
```


## Github

[https://github.com/zxz054321/laravel4china](https://github.com/zxz054321/laravel4china)