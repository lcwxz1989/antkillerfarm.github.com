---
layout: post
title:  深度学习（二十八）——SOM, 多模态学习
category: DL 
---

# RBM & DBN & Deep Autoencoder（续）

## DBN

RBM不仅可以单独使用，也可以堆叠起来形成Deep Belief Nets(DBNs)，其中每个RBM层都与其前后的层进行通信。单个层中的节点之间不会横向通信。

深度置信网络可以直接用于处理无监督学习中的未标记数据聚类问题，也可以在RBM层的堆叠结构最后加上一个Softmax层来构成分类器。

除了第一个和最后一个层，深度置信网络中的每一层都扮演着双重角色：既是前一层节点的隐藏层，也是后一层节点的输入（或“可见”）层。深度置信网络是由多个单层网络组成的。

深度置信网络常用于图像、视频序列和动作捕捉数据的识别、聚类与生成。

参考：

https://mp.weixin.qq.com/s/7V0GSWcKZGyXeLeMPhE9fQ

神经网络简史：BP算法后的又一突破—信念网络

https://zhuanlan.zhihu.com/p/40100223

深度学习与TensorFlow：关于DBN的一些认识

## Deep Autoencoder

![](/images/img2/deep_autoencoder.png)

Deep Autoencoder由两个对称的DBN组成，其中一个DBN通常有四到五个浅层，构成负责编码的部分，另一个四到五层的网络则是解码部分。

让我们用以下的示例来描绘一个编码器的大致结构：

784 (输入) ----> 1000 ----> 500 ----> 250 ----> 100 -----> 30

假设进入网络的输入是784个像素（MNIST数据集中28x28像素的图像），那么深度自动编码器的第一层应当有1000个参数，即相对较大。

这可能会显得有违常理，因为参数多于输入往往会导致神经网络过拟合。

在这个例子当中， 增加参数从某种意义上来看也就是增加输入本身的特征，而这将使经过自动编码的数据最终能被解码。

其原因在于每个层中用于变换的sigmoid置信单元的表示能力。sigmoid置信单元无法表示与实数数据等量的信息和差异，而补偿方法之一就是扩张第一个层。

各个层将分别有1000、500、250、100个节点，直至网络最终生成一个30个数值长的向量。这一30个数值的向量是深度自动编码器负责预定型的前半部分的最后一层，由一个普通的RBM生成，而不是一个通常会出现在深度置信网络末端的Softmax或逻辑回归分类输出层。

解码的DBN是一个完全相反的结构。

相比Autoencoder，Deep Autoencoder显然能够“消化”更复杂的数据。

## 参考

https://deeplearning4j.org/cn/restrictedboltzmannmachine

受限玻尔兹曼机基础教程

http://txshi-mt.com/2018/02/04/UTNN-11-Hopfield-Nets-and-Boltzmann-Machines/

Hopfield网和玻尔兹曼机

https://mp.weixin.qq.com/s/hnmKM-_zgb5m80NTd_b8gw

能量学习之Hopfield Networks

>John Joseph Hopfield，1933年生，美国科学家。Cornell University博士（1958），先后执教于UCB、Princeton和Caltech。美国科学院、美国艺术科学院院士。   
>他爸也叫John Joseph Hopfield，波兰物理学家。

http://txshi-mt.com/2018/02/10/UTNN-12-Restricted-Boltzmann-Machines/

受限玻尔兹曼机

https://mp.weixin.qq.com/s/pWhJR6_6lRtDBl1MnYSIiw

深度学习来一波，受限玻尔兹曼机原理及在推荐系统中的应用 

http://www.cnblogs.com/kemaswill/p/3269138.html

基于受限玻尔兹曼机(RBM)的协同过滤

http://www.cnblogs.com/kemaswill/p/3203605.html

受限波尔兹曼机简介

https://mp.weixin.qq.com/s/MqnJ39GPrzP4xJWDZi9gnQ

博士生开源深度学习C++库DLL：快速构建卷积受限玻尔兹曼机

http://www.cs.toronto.edu/~fritz/absps/cogscibm.pdf

A Learning Algorithm for Boltzmann Machines

http://www.cs.toronto.edu/~hinton/absps/dbm.pdf

Deep Boltzmann Machines

http://www.cs.toronto.edu/~hinton/absps/guideTR.pdf

A Practical Guide to Training Restricted Boltzmann Machines

http://www.taodocs.com/p-62206829.html

《受限波尔兹曼机简介》张春霞著

https://mp.weixin.qq.com/s/mXJthyETebtww5TvEljuoQ

预测电影偏好？如何利用自编码器实现协同过滤方法

https://blog.csdn.net/hanlin_tan/article/details/62078935

机器学习中的玻尔兹曼分布——最小代价和极大似然

# SOM

Self Organizing Maps (SOM)（也叫kohonen network）是一种无监督算法，主要用于聚类和可视化。

>Teuvo Kohonen，1934年生，芬兰科学家。Helsinki University of Technology博士和教授。

![](/images/img2/SOM.png)

上图是一个SOM可视化的案例。左边的六角形网格被称作SOM的map space。其中，越相似的国家，在map space上的颜色和位置越接近。

下面来说一下SOM的具体训练方法。

## 构建map space

首先，map space是有拓扑关系的。这个拓扑关系需要我们确定，如果想要一维的模型，那么隐藏节点依次连成一条线；如果想要二维的拓扑关系，那么就组成一个平面网格。换句话说，SOM的目标就是**将任意维度的输入离散化到一维或者二维(更高维度的不常见)的离散空间上。**

网格的形状一般是矩形或六角形。网格中的每个node关联一个weight vector，其中的值表示一个input space中的点，因此weight vector和input vector的维度是相同的。

## 初始化weight vector

![](/images/img2/SOM_2.png)

上图展示了SOM的训练过程。SOM训练的目的就是使map space尽量贴合样本分布。

因此，通常有两种初始化weight vector的方法：

1.用小的随机值初始化。

2.从最大的两个主特征向量上进行采样。

显然，第2种训练起来要快的多。因为它已经是SOM weights的一个很好的近似了。

## 训练SOM

1.对于每一个输入数据，找到与它最相配的node，这个node一般被称作best matching unit(BMU)。这里一般使用Euclidean distance作为相似度的度量。

2.更新BMU的weight，使之更接近输入数据。同时也要更新BMU周围的node的weight，离BMU越近，更新幅度越大。更新公式为：

$$W_{v}(s + 1) = W_{v}(s) + \theta(u, v, s) \cdot \alpha(s) \cdot (D(t) - W_{v}(s))$$

其中，D(t)是输入数据，u表示BMU的index，v是被更新node的index，s是迭代的次数，$$\alpha(s)$$是更新率，一般为一个单调递减函数。$$\theta(u, v, s)$$是时空衰减因子，公式通常为：

$$\theta(u, v, s)=\exp \left(-\frac{dist(u,v)}{2\sigma^2(s)}\right)$$

反复多次进行以上2步的迭代之后，SOM会趋于收敛。

## 与K-Means的比较

同样是无监督的聚类方法，SOM与K-Means有什么不同呢？

1.K-Means需要事先定下类的个数，也就是K的值。SOM则不用，隐藏层中的某些节点可以没有任何输入数据属于它。所以，K-Means受初始化的影响要比较大。

2.K-means为每个输入数据找到一个最相似的类后，只更新这个类的参数。SOM则会更新临近的节点。所以K-mean受noise data的影响比较大，SOM的准确性可能会比k-means低（因为也更新了临近节点）。

3.SOM的可视化比较好。优雅的拓扑关系图。

![](/images/img2/SOMsPCA.png)

上图中蓝线表示PCA的主轴，而红点是SOM的node结点，可见SOM对数据的贴合程度要高于PCA。

## 参考

http://chem-eng.utoronto.ca/~datamining/Presentations/SOM.pdf

Self-Organizing Maps

http://www.cnblogs.com/sylvanas2012/p/5117056.html

Self Organizing Maps (SOM): 一种基于神经网络的聚类算法

http://blog.csdn.net/Loyal2M/article/details/11225987

聚类算法实践（3）——PCCA、SOM、Affinity Propagation

http://www.ai-junkie.com/ann/som/som1.html

Kohonen's Self Organizing Feature Maps

# 多模态学习

https://github.com/HuaizhengZhang/Awsome-Deep-Learning-for-Video-Analysis

深度学习视频分析/多模态学习资源大列表

https://mp.weixin.qq.com/s/ruRkqBEdyj2Dx0WTO5Jhcw

多模态学习研究进展综述

https://mp.weixin.qq.com/s/g3rwPsusYi7gQopOHvdNrA

多模态学习调研

https://mp.weixin.qq.com/s/xzeNAuuDt_VLHDgvIkc-Mg

多模态情感分析简述

https://mp.weixin.qq.com/s/vpBPkjuCebSWh5qPLYHCkw

上海交大提出多模态框架“EmotionMeter”，更精准地识别人类情绪

https://mp.weixin.qq.com/s/BBg04rDtiqU-XrWortufNA

康奈尔&英伟达提出多模态无监督图像转换新方法

http://mp.weixin.qq.com/s/khOINUyrNV3TFfgNRheH0A

卷积神经网络压缩、多模态的语义分析研究

https://mp.weixin.qq.com/s/ywU4L659iRcmIgmV6RtbXA

DeepMind新研究连接听与看，实现“听声辨位”的多模态学习

https://mp.weixin.qq.com/s/1qhcyTXttgKWlw-Oy556Tw

TPAMI2019最新《多模态机器学习综述》

https://mp.weixin.qq.com/s/BczgUuh2FIvP5MG9xh87wQ

多模态多任务学习新论文

https://mp.weixin.qq.com/s/ipj8qpYRiYbIeXn2PZb1SQ

5G时代下多模态理解做不到位注定要掉队

https://mp.weixin.qq.com/s/UghgWBN7mE8oJdMUvjAjcQ

何晖光：多模态情绪识别及跨被试迁移学习

https://mp.weixin.qq.com/s/EMWpBP5iB1Qrleo3XNjbuQ

IEEE Fellow何晓东&邓力：多模态智能论文综述：表示学习，信息融合与应用

https://mp.weixin.qq.com/s/Yus55s1utTrjuzsrebJu_w

让机器读懂视频：亿级淘宝视频背后的多模态AI算法揭秘

https://mp.weixin.qq.com/s/4AzF6utrQhhEweRIM6zV3A

文本+视觉，跨模态预训练新进展

# Capsule

https://jhui.github.io/2017/11/14/Matrix-Capsules-with-EM-routing-Capsule-Network/

“Understanding Matrix capsules with EM Routing (Based on Hinton's Capsule Networks)”

https://zhuanlan.zhihu.com/p/42864711

胶囊网络到底是什么东东？

https://zhuanlan.zhihu.com/p/32106577

酉变换与递归神经网络

https://github.com/freefuiiismyname/capsule-mrc

基于capsule的观点型阅读理解模型

https://mp.weixin.qq.com/s/cskdgsysD7R_FKChAKmlDg

利用Capsule重构过程，Hinton等人实现对抗样本的自动检测

https://mp.weixin.qq.com/s/7fBXMvT4eyZrKhPKQTAIZQ

你听说过胶囊网络吗？

https://mp.weixin.qq.com/s/F9SGZPZj6gup_nOVuDel6A

与胶囊网络异曲同工：Bengio等提出四元数循环神经网络

https://mp.weixin.qq.com/s/4o9XHGwx5lYsJ7YfUNHSoQ

百年老图难倒谷歌AI，网友：是鸭是兔？连我都不能确定

https://mp.weixin.qq.com/s/dN1p7nuv6xtnIsSuY73CcA

基于GNN，强于GNN：胶囊图神经网络的PyTorch实现

https://mp.weixin.qq.com/s/lcJcaiMtYXGVOwa_sVsVfA

Hinton老爷子CapsNet再升级，结合无监督，接近当前最佳效果

https://mp.weixin.qq.com/s/A0m3lkIBCTFf5bzTQlYbgQ

基于胶囊网络的计算机视觉应用

https://mp.weixin.qq.com/s/BqsFIUrVEVz5kOFh3W93gQ

胶囊网络升级新版本，推特2000+赞
