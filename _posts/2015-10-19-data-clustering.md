---
layout: post
title: "Data Clustering"
description: ""
category:
tags: []
---
{% include JB/setup %}

原文多達60頁，所以我暫時挑我想看，之後再慢慢把它看完。

<!-- more -->

## Clustering Techniques

![]({{ site.url }}/assets/{{ page.title }}/A taxonomy of clustering approaches.png)

| hierarchical（階層式）| partitional（分割式） |
| - | - |
| Produce a nested series of partitions. | Produce only one partition. |

### 用不同面向去觀察分群演算法

* 根據演算法結構和運算方式
  * Agglomerative（聚合式）
    * 從每一個點視為一個 cluster 開始不斷合併。
  * divisive
    * 所有點視為一個 cluster，慢慢切成多個 cluster。
* 使用feature的方式
  * Polythetic
    * 一次看所有feature（也就是所有的feature都拿去算兩個點間的距離）
    * 大部分演算法屬於此類型
  * Monothetic
    * 一個一個feature看
    * 缺點：點的維度為\\(d\\)，會產生\\(2^d\\)個群，維度很大的時候就會崩潰了。
    * 例子
      ![Monothetic partitional clustering]({{ site.url }}/assets/{{ page.title }}/Monothetic partitional clustering.png)
      1. 根據 feature \\(X_1\\)，找到一直線\\(V\\)，分割出1、2和3、4兩塊。
      2. 再根據 feature \\(X_2\\)，找到兩直線\\(H_1\\)和\\(H_2\\)，分成1、2、3、4共四塊。
