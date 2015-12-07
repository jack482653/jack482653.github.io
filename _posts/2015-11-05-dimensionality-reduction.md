---
layout: post
title: "Dimensionality Reduction"
description: ""
category: Course
tags: [Machine Learning, Course]
---
{% include JB/setup %}

## Why dimensionality reduction?

* 小資料集（ N 小），降低維度（1000維降到100維）有機會增進分類器的 performance 。

## Dimensionality reduction

* Feature selection
	* 從 d 個維度挑出 k 個維度
* Feature extraction
	* 從 d 個維度用線性組合弄出 k 個維度

*使用 ruduction 要注意是否有破壞模型對 data 的假設*

## Feature selection (supervised)

* Forward selection
	* 實務上比較常用。
	* 當 \\( k \ll d \\) 適合用。
	* 第一個挑錯，第二個會 depend on 第一個（一步錯步步錯）。
* Backward selection
	* 第一個挑錯，第二個不太 depend on 第一個。

*對於人臉辨識，是靠連續的像素組成的 pattern 辨識，如果用feature selection會破壞這種 pattern ，不適合用在處理這個問題*

## Feature extraction

* Principal Component Analysis (Unsupervised, Linear)
	* Principal components: k 個 projection vectors \\(w_1,...,w_k\\)