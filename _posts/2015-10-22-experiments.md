---
layout: post
title: "Experiments"
description: ""
category: Course
tags: [Machine Learning, Course]
---
{% include JB/setup %}
<!-- more -->
## Data Preprocessing

* p6
  * input dimension: 還沒預處理過的data的維度
  * feature dimension: 餵進演算法的資料的維度（因為可能會做過預處理等等）

* p7
  * 資料不完整(incomplete)
  * noise(Attribute)
    * 年齡：不知道填的人是虛歲還是實歲
  * outlier(Label)
    * 一個軍隊的人都穿白色的突然有一個人穿黑色的
  * 資料不一致(Inconsistent)
    * 不同的資料來源可能用不同的資料格式。（可能無法一對一對應）

* p8
  * Data Tranformation 的 aggregation: 例如要一季的資料，就要把逐日的資料整理成一季的。
  * Data Reduction: 減少資料大小，同時維持搞準確率。

### Data Integration

* 需要很強的 Domain knowledge

### Filling Missing Values

* 遺失的資料可能是 Attribute 或 Label
* How?
  * 踢掉data
    * 通常是沒 Label
    * 如果資料很少呢？
  * ...

### Identify Outliers and Smooth-Out Noises

* Binning
  * 步驟
    * 把可能有noise的attribute做sorting，切成一格一格（Bin）
    * 把在同一格內的data attribute 的值改成同一格內的 attribute 中間值。
  * 切法
    * equalwidth
    * equaldepth
* Clustering
* Train Regression to predict

### Normalization

* Linear Normalization
* Z-Normalization
* Why Normalization?
  * 當有很多 attribute ，數值比較大的 attribute 會把數值比較小的 attribute 蓋掉。
* How about Discrete attribute?
  * ex RGB

  | id | RGB |
  | - | - |
  | 1 | R |
  | 2 | G |
  | 3 | B |

  轉換成：

  | id | R | G | B |
  | - | - | - | - |
  | 1 | 1 | 0 | 0 |
  | 2 | 0 | 1 | 0 |
  | 3 | 0 | 0 | 1 |

### Aggregation

* 把多個 attribute 合併成一個 attribute

### Aggregation Construction / Augmentation

* 當某個 pattern 同時跨 attribute 和 instance
* 演算法沒辦法看跨 instance 間的關係

### Data Reduction

* Sampling (減少Instance)
  * ex 反恐 anomaly detection，異常得很少，不太可能透過 Sampling
  * 不是 data 很大就是 big data ，很多問題可以用 Sampling 搞定
* Reduce Number of Attributes (減少Attribute)
* Principle Component Analysis (降低維度)
* Discretization
  * Unsupervised
    * Binning
    * Clustering
  * Supervised
    * Binning 時切，使得同一個bin內資料的label盡可能一樣。
    * Information-based Concept Hierarchies

## Performance Measures

### Metrics for Classi􏰃cation

  * false positive: 預測出positive，但其實是錯的。
  * false negative: 預測出negative，但其實是錯的。
  * Confusion Matrix
  * ROC Curve
    * 很多分類器 raw ouput 是一個連續數值，用一個 threshold \\(\theta\\)，如果大於 \\(\theta\\) 就預測成1，否則為-1。
    * 根據不同的 \\(\theta\\) 計算 TP-Rate 和 FP-Rate 。
    * 45度直線
      * 亂猜，當 \\(\theta\\) 增加，猜對 TP-Rate 增加（往上走），猜錯 FP-Rate 增加（往右走）。
    * P31：真理：沒有絕對好的 Classifier ，只有特定狀況選擇適當的分類器。
  * AUC: ROC Curve 底下面積
    * AUC \\( \in [0.5, 1]\\)

### Metrics for Regression
  * \\( E_{RSE} \\)：使用的分類器和Baseline（永遠猜\\( \bar{r} \\)）比較

### Generalization Performance
  * Generalization error: 沒看過的data的error
    * 知道x和r的joint distribution
    * p(x, r): x和r的出現機率
    * d(x, r): x和r的出現次數？
    * \\( E_{J x L}[l(h(x), r)] \\)等於error function的期望值
    * R*: 實際的f的error
      * 為什麼f會有error？
        * 因為f是目前維度下的ground truth，可能有其他維度你不知道，造成noise。
    * Estimation error (variance): h（特定training data產生）vs h*（不特定的）
    * Approximation error(bias): 跟hypothesis有關，如果H跟實際的f差太多（一次式 vs 二次式），這個error越大。
    * |H|太小：很快就找到最好的h*，但會跟f差很多。
    * underfitting: |H|太小導致學不到f，高bias，低variance。
    * overfitting: |H|太大導致學到特定的data set的特性，低bias，高variance。

## Model Selection

* state of art: 選擇一個超複雜最好無限維度的model（降低bias），訓練的時候加regularizer（降低variance）
* 把資料投射到無窮維度（泰勒展開式）
* 動hyperparameters會改變Model complexity嗎？
  * 會，例如動regularization term \\( \lambda \\)，會傾向找比較平的平面。
* How to determine good hyperparameters?
  * hold-out: 把一些東西遮起來（ex: test data不會再training用）
  * grid search（查）
  * Three-Way Data Splits
    * training 再切出一塊validation set，用來tuning hyperparameters
    * 但原本資料已經夠少了你還這樣搞...
    * 而且可能抽樣抽得不好（或是抽太好），error失真

## Cross-Validation

* training data 切成 k 份，k份輪流當validation set，validation set 的 error取平均。
* 也可以運用到 test data
* How many folds (K) we need?
  * K 越大，每個phase都看到差不多的資料，Covariance增加，Variance上升


## Ensemble Methods

* 術語
  * weak leaner: 準確率高於1/2的（比丟銅板好）
  * strong learner: 準確率八九成的
* Voting
  * Expected Value and Variance
    * 假設learner的決策互不干擾(i.i.d)，Voting可以降低Variance
    * 但如果不是i.i.d，Covariance增加，Variance會上升
      * 特別是正相關的～
* Bagging: 降低Covariance
* Boosting: 把上一個預測錯的點用來訓練下一個model
  * Original Boosting
    * \\( d_2 \\)餵 \\( d_1 \\) 在 \\( X_1 \\) 預測不正確 +  \\( d_1 \\) 在 \\( X_2 \\) 預測正確的部分
    * \\( d_3 \\)餵 \\( d_1 \\) 和 \\( d_2 \\) 預測不正確
    * 但data size變小了... bias 增加
  * 改良：Adaboost (每個learner的data size都一樣)
