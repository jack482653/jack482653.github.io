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
  * Hard vs Fuzzy
    * Hard
      * 演算法直接分配點到一個 cluster。
    * Fuzzy
      * 每一個點可能屬於一個或多個 cluster。
      * 演算法計算點屬於哪一群的可能性。
      * 取可能性最大的群加入 -> 退化成Hard。
  * 最佳化 error function（下的標題很奇怪）
    * Deterministic
      * Given a dataset, always arrive at the same clustering.
    * Stochastic
      * 有些參數是隨機的，因此每次結果可能不一樣。
  * Incremental vs Non-incremental
    * dataset 大小、執行時間或記憶體空間的限制
    * 或是 data stream，需要逐步更新
    * 因此分群演算法設計上必須減少
      * 掃過整個 dataset 的次數
      * 運算過程中 data point 被用到的次數
      * 演算法的操作中所使用的資料結構大小

### Hierarchical Clustering Algorithms

![]({{ site.url }}/assets/{{ page.title }}/The dendrogram obtained using the single-link algorithm.png)

* 產生X軸表資料點，Y軸表相似度的樹狀圖。相似度越小，群的數量越多，群內的資料點也越少。
* 三大類型
  * Single-Link
    * 兩群的相似性：\\( distance(C_1, C_2) = min \text{ } distance(a, b) \text{, } \forall a \in C_1 \text{, } b \in C_2 \\)
    * Chaining effect: a tendency to produce clusters that are straggly or elongated.
  * Complete-Link
    * 兩群的相似性：\\( distance(C_1, C_2) = max \text{ } distance(a, b) \text{, } \forall a \in C_1 \text{, } b \in C_2 \\)
  * Minimum-Variance
