---
layout: post
title:  "机器学习笔记（一）"
categories: 机器学习
tags: 《机器学习（周志华）》
excerpt: 机器学习包括符号学习和统计学习等方式。机器学习模型的评估和选择。
---

## 序言
* 符号学习、统计学习
* 认知科学研究
* 深度学习、迁移学习

## 第一章 绪论
### 1.1 引言
* 机器学习研究的主要内容，是关于在计算机上从数据中产生模型的算法
### 1.2 基本术语
* 数据集；示例（样本）；属性（特征）；属性值；属性空间（样本空间）；特征向量
* 例子：令$$D={x_{1}, x_{2}, ..., x_{m}}$$是包含m个示例的数据集。$$x_{i}=(x_{i1}; x_{i2}; ...; x_{id})$$是d纬样本空间X中的一个向量
* 学习（训练）：从数据中学得模型的过程；
* 训练数据、训练样本、训练集
* 假设(hypothesis)：学得模型对应了数据的某种潜在规律
* 真相（真实）(ground-truth)：潜在规律自身
* 样例：拥有标记信息的示例，一般用$$(x_{i}, y_{i})$$表示第i个样例，$$y_{i}∈Y$$是示例$$x_{i}$$的标记，Y是所有标记的集合
* 分类(classification)：离散值；回归(regression)：连续值。二分类(binary classfication)：正类、反类。
* 监督学习、无监督学习，分类和回归是前者的代表，聚类是后者的代表
* 泛化能力
### 1.3 假设空间
* 归纳和演绎是科学推理的两大基本手段
* 我们把学习过程看作一个从所有假设组成的空间中进行搜索的过程
* 版本空间：与训练集一致的“假设集合”
### 1.4 归纳偏好
* 机器学习算法在学习过程中对某种类型的假设的偏好，称为“归纳偏好”
* 归纳偏好可以看作学习算法自身在一个可能能庞大的假设空间中对假设进行选择的启发式或“价值观”
* 奥卡姆剃刀：若有多个假设和观察一致，选最简单的那个
* 没有免费午餐定理(NFL定理)：无论学习算法A多么聪明、学习算法B多笨拙，他们的期望竟然相同。
* 脱离具体问题，空泛地谈论“学习什么
### 1.5 发展历程
* 深度学习，狭义地说就是“很多层”的神经网络
* 深度学习呦大量的参数，若数据样本少，很容易“过拟合”
### 1.6 应用现状
### 1.7 阅读材料
* 多释原则：主张保留与经验观察一致的所有假设

## 第2章 模型评估与选择
### 2.1 经验误差与过拟合
* 错误率、精度；误差：实际预测输出与样本的真实输出之间的差异；训练误差：学习器在训练集上的误差；泛化误差：新样本上的误差
* 过拟合、欠拟合；欠拟合容易克服，例如在决策树学习中扩展分支，在神经网络学习中增加轮数；过拟合是无法彻底避免
### 2.2 评估方法
* 测试集尽可能与训练集互斥
#### 2.2.1 留出法
* 将数据集D划分成两个互斥的集合（训练集S和测试集T），划分尽量保持数据分布的一致性，通常为分层采样
* 一般需要若干次随机划分、重复多次试验评估后取平均值作为留出法的评估结果
* 训练集S包含绝大多数样本，则训练的模型更接近D训练的模型，但评估不太准确；若T多包含一些样本，则训练的模型会有较大差别。常见将2/3～4/5的数据用于训练，其余用于测试
#### 2.2.2 交叉验证法
* 将数据集D划分成k个大小相似的互斥子集，用k-1个子集的并集训练，余下的子集测试，最终返回k个测试的均值。常见的10次10折交叉验证
* 特殊的，留一法：数据集中有m个样本，k=m。
#### 2.2.3 自助法
* 随机从D中选择一个样本放入D'中，再将该样本放回D中。无穷多次采样后，D中有36.8%的样本未出现在D'中。
* D'作为训练集，D-D'作为测试集
* 自助法在数据集较小、难以有效划分训练／测试集时有用；然而自助法产生的数据集改变了原始数据集的分布，引入估计误差
#### 2.2.4 调参与最终模型
* 算法的参数，数目常在10以内；模型的参数，数目往往很多
### 2.3 性能度量
#### 2.3.1 错误率与精度
#### 2.3.2 查准率、查全率与F1
* TP（真正例）、FN（假反例）、FP（假正例）、TN（真反例）
* 查准率$$P=\frac{TP}{TP+FP}$$；查全率$$R=\frac{TP}{TP+FN}$$，P与R是一对矛盾的度量
* P-R曲线：一条曲线将另一条曲线完全“包住”，前者优于后者；也可以比较面积
* 平衡点：P=R的点，平衡点高的性能好
* $$F1=\frac{2*P*R}{P+R}$$,$$F_{\beta}=\frac{(1+\beta^2)*P*R}{(\beta^2*P)+R)}$$；$$\beta>1$$查全率影响大，$$\beta<1$$查准率影响大
* 宏、微
#### 2.3.3 ROC与AUC
* TPR真正例率、FPR假正例率：$$TPR=\frac{TP}{TP+FN}$$、$$FPR=\frac{FP}{TN+FP}$$。TPR大好，FPR小好
* ROC曲线下的面积是AUC。AUC考虑的是样本预测排序的质量，排序损失是AUC上的面积
#### 2.3.4 代价敏感错误率与代价曲线
* 为衡量不同类型错误所造成的不同损失，为错误赋予“非均等代价”
### 2.4 比较检验
#### 2.4.1 假设检验
#### 2.4.2 交叉验证t检验
#### 2.4.3 McNemar检验
#### 2.4.4 Friedman检验与Nemenyi后续检验
### 2.5 偏差与方差
* 泛化误差可分解为偏差、方差与噪声，偏差度量了学习算法的预期预测与真实结果的偏差程度，方差度量了同样大小的训练集的变动所导致的学习性能的变化，噪声表达了当前任务上任何学习算法的期望泛化误差的下界，刻画了学习问题本身的难度
