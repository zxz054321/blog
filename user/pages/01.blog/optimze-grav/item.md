---
title: 'Grav 优化指南'
date: '19:00 01/11/2018'
taxonomy:
    category:
        - blog
    tag:
        - grav
author: Abel
---

Grav 内置了许多特性，使得 Grav 站长可以轻松优化网站的访问速度。

===

## Asset Manager

Asset Manager 是 Grav 的一个内置模块，可针对托管的 CSS / JS 文件进行优化。

这是系统默认配置文件  `system.yaml` 中的片段：

```yaml
assets:                                # Configuration for Assets Manager (JS, CSS)
  css_pipeline: false                  # If true, enables the CSS pipeline, combining multiple CSS resources into one
  css_pipeline_include_externals: true # Include external CSS resources from the pipeline
  css_pipeline_before_excludes: true   # Renders pipelined CSS resources before non-pipelined CSS resources
  css_minify: true                     # Minify the CSS during pipelining
  css_minify_windows: true             # If false, blocks minifying on Windows servers
  css_rewrite: true                    # Rewrite any CSS relative URLs during pipelining
  js_pipeline: false                   # If true, enables the JS pipeline, combining multiple JS resources into one
  js_pipeline_include_externals: true  # Include external JS resources from the pipeline
  js_pipeline_before_excludes: true    # Renders pipelined JS resources before non-pipelined JS resources
  js_minify: true                      # Minify the JS during pipelining
  enable_asset_timestamp: false        # If true, adds a URL query parameter to each asset link for cache invalidation
```

在默认配置中，Asset Manager 的管道功能没有开启，即其优化特性不会生效。当页面当中引入了多个 CSS / JS 文件时（主题、插件都会引入），庞大的资源文件会增加传输时间，重复建立 TCP 连接将会一定程度地拖慢加载速度。

可按以下配置开启优化：

```Yaml
assets:
  # 开启 CSS 管道
  css_pipeline: true
  # 不建议把外部(网络上的) CSS 加入管道，可能会有问题
  css_pipeline_include_externals: false
  # 开启后，管道出来的文件将先于未经管道的文件加载，请酌情配置
  css_pipeline_before_excludes: false
  # 开启 CSS 压缩(如启用了 gzip 压缩，可能不会有实际优化效果)
  css_minify: true
  # Windows 服务器请酌情配置
  css_minify_windows: false
  # 重写 CSS 中的 URL
  css_rewrite: true
  # 开启 JS 管道
  js_pipeline: true
  # 不建议把外部(网络上的) JS 加入管道，可能会有问题
  js_pipeline_include_externals: false
  # 开启后，管道出来的文件将先于未经管道的文件加载，请酌情配置
  js_pipeline_before_excludes: false
  # 开启 JS 压缩(如启用了 gzip 压缩，可能不会有实际优化效果)
  js_minify: true
  # 在引用 CSS / JS 时加上时间戳(如在 CDN 或浏览器配置了缓存静态资源，建议开启，以确保静态资源及时更新)
  enable_asset_timestamp: true
```
优化之后，使用 Asset Manager 管理静态资源的页面将会只有 1 个 CSS 文件和 1 个 JS 文件，由此而来还有一个隐藏效果：可避免 CSS / JS 文件泄漏主题、插件路径。

## 适配 CDN

  `system.yaml` 中有一项 `append_url_extension`，其作用是设置页面后缀，俗称 “伪静态”。建议采用以下配置：

```yaml
append_url_extension: .html
```

html 后缀拥有广泛的支持，且便于配置缓存规则。

## 系统缓存

Grav 默认启用了缓存，请务必不要关闭，除非你清楚自己在干什么。

YAML 解析、Markdown 解析、Twig 模板编译、Asset Manager 优化处理、索引等过程都是很慢的。

## 图片无损压缩

这不属于 Grav 内置特性，但跟 Grav 系统很多地方都息息相关。图片通常都是网页加载时对速度影响最大的，未经优化的图片会严重拖慢速度且耗费流量。

macOS 推荐使用 [ImageOptim](https://imageoptim.com/mac)