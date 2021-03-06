---
layout: post
title: 页面提速之——数据缓存
category: 技术
tags: PHP
description: 一些访问量很大的网页，尤其是网站主页，展现过程中如果数据都是现成生成，会导致一些瓶颈，使用数据缓存可以极大减少页面生成时间
---
> 转载自:[https://yansu.readthedocs.io](https://yansu.readthedocs.io),谢谢

### 适用范围

一般需要需要数据缓存的页面，集中在以下几个类别：

- 实时性不是很高
- 页面数据繁杂，生成需要读取数据库或者文件
- 访问量较大

如果符合这几点，基本可以确定，利用数据缓存，在不影响业务的情况下可以减少页面加载时间

### 实现方式

对于PHP而言，我们经常看到的缓存方式有

- Memcache(内存)
- MongoDB(非关系数据库)或MySQL(关系数据库)
- File(文件缓存)

效率依次降低，缓存量依次增大，根据自己的业务情况酌情选择即可

### 代码实现

使用cache()函数来进行缓存和读取，cache()内部实现过期时间判断

    if(!$data = cache('data')){
      $data = .....
      cache('data',$data,60);
    }

### 继续优化可能

缓存之后还有多种优化方法

- 增加缓存队列，固定缓存大小，防止无限缓存
- 多级缓存，防止击穿（例如在memcache后加mongodb缓存，在memcache挂掉以后能负担一部分负荷）