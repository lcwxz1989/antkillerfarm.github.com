---
layout: post
title:  深度学习（四十二）——深度ISP, Spiking Neuron Networks, 深度时间序列, AI可解释性
category: DL 
---

# 迁移学习（续）

https://mp.weixin.qq.com/s/Hok9D8dAzYrBz7XoFmGE2A

AliExpress：在检索式问答系统中应用迁移学习

https://mp.weixin.qq.com/s/f_vB2AXCytnvoZaqfMeIpw

应用TF-Slim快速实现迁移学习

https://mp.weixin.qq.com/s/R1bKmhADfhQAZmhXL9ObiQ

多重预训练视觉模型的迁移学习

https://mp.weixin.qq.com/s/l-l1xbUaPNKc-w5XndjCbQ

通过网络结构迁移学习提高图像识别任务的拓展性

https://mp.weixin.qq.com/s/-KssC3yXsG3ZuV8-I6D_nQ

学习迁移架构用于Scalable图像的识别

https://mp.weixin.qq.com/s/5DtTgc9bIrdXQkmuqRm8CA

谷歌大脑迁移学习：减少调参，直接在数据集中学习最佳图像架构

https://mp.weixin.qq.com/s/fEKc6yFZwTPAHjXJlcHA-w

香港科技大学提出L2T框架：学习如何迁移学习

https://mp.weixin.qq.com/s/pbyByPoZ9SVoP9B7pJMxXg

深度卷积网络迁移学习的脸部表情识别

https://mp.weixin.qq.com/s/aqmeIEVIG-845wiKlyXlsA

小数据、高准确率的文本分类：利用迁移学习创造通用语言模型

https://mp.weixin.qq.com/s/yXF5Cxs_29OBOl41enjfyg

阿里巴巴&浙大Poster论文：基于直推式无偏嵌入的零样本学习

https://mp.weixin.qq.com/s/qYoTgqwjaUlEycuk9LlonA

迁移学习：6张图像vs13000张图像，超越2013 Kaggle猫狗识别竞赛领先水平

http://mp.weixin.qq.com/s/6Urv6TfUfc-BWV1YqTM1PQ

迁移学习+BPE，改进低资源语言的神经翻译结果

https://mp.weixin.qq.com/s/kPFS_4swYEP6Amw8xfXEgg

中科院自动化所-针对小样本问题的学习生成匹配网络方法

https://mp.weixin.qq.com/s/NFziZe6xS_CzVZX_0Den9g

达观数据CTO纪达麒:小标注数据量下自然语言处理实战经验

https://mp.weixin.qq.com/s/6w5S5R_qA0956VMj1isunQ

雷哥带你读论文之深度迁移炼丹！

https://mp.weixin.qq.com/s/wB9skXSWoMHoWnME2JAyIw

基于全局类别表征的小样本学习

https://mp.weixin.qq.com/s/6eHmudo6EG47qBe7xwri6g

ImageNet错误率小于4%，数据量依然不够，N-Shot Learning或是终极解决之道？

https://mp.weixin.qq.com/s/cG0TDIZ3z4lUEQb_N1ysbg

使用迁移学习构建顶尖会话AI

https://mp.weixin.qq.com/s/VGdlOlQh1_4FFTAuUHR_VA

迁移学习中如何利用权值调整数据分布？DATL、L2TL两大方法解析

https://mp.weixin.qq.com/s/V-4d-3yMmQpZUVY-h1eaoA

Barbara Plank-NLP模型的跨语言/跨领域迁移-经验分享

https://mp.weixin.qq.com/s/TUrH7qiZBpmqWN4VL5dhlw

清华大学：用于少次关系学习的神经网络雪球机制

https://mp.weixin.qq.com/s/VlxF7BVk7hUQ9HDiGYpzGA

基于Co-Attention和Co-Excitation的少样本目标检测

https://mp.weixin.qq.com/s/xaKqAhuxaHDPV-VwHE7H2A

零样本学习研究进展综述中文版

# 深度ISP

## 数据集

### HDR+

HDR+是一个使用连拍摄影生成更好的图像的数据集。

官网：

http://hdrplusdata.org

参考：

https://zhuanlan.zhihu.com/p/34391353

机器感知Google推出HDR+连拍摄影数据集

### HDRNet

HDRNet是一个Image Enhancement方面的数据集。

官网：

https://groups.csail.mit.edu/graphics/hdrnet/

## 综述

论文：

《Unprocessing Images for Learned Raw Denoising》

这篇论文虽然不是综述，但有很多内容讲解ISP的流程。

《Deep Learning for Image Denoising: A Survey》

《Deep Learning on Image Denoising: An overview》

这两篇综述都是哈工大深圳分院的作品。

## 参考

https://mp.weixin.qq.com/s/wA85XFQXeypuoqFnmN2P4g

降噪的新时代

https://mp.weixin.qq.com/s/919VEvennHEG3iXKkMZoQQ

不止是去噪---从去噪看AI ISP的趋势

https://zhuanlan.zhihu.com/p/27902193

利用卷积自编码器对图片进行降噪

https://zhuanlan.zhihu.com/p/39512000

Noise2Noise：图像降噪，无需干净样本

https://mp.weixin.qq.com/s/_tvOQPvybqmvLF19kHcbFg

北大开源ECCV2018深度去雨算法：RESCAN

https://mp.weixin.qq.com/s/Wdxkvlz4nLbJS_gWqHwMjw

无需额外硬件，全卷积网络让机器学习学会夜视能力

https://mp.weixin.qq.com/s/iH7gbRn4opLsWgKWoVFpBA

腾讯优图&港科大提出较大前景运动下的深度高动态范围成像

https://mp.weixin.qq.com/s/WXVZkqCGlj6ym5YrSZS3Vg

谷歌普林斯顿提出首个端到端立体双目系统深度学习方案

https://mp.weixin.qq.com/s/NlYgA-A43q4C155kRdWPAQ

论文复现：谷歌实时端到端双目系统深度学习网络stereonet

https://mp.weixin.qq.com/s/9yfTO2jHz69-k1MsUGIM0Q

双目立体放大！谷歌刚刚开源的这篇论文可能会成为手机双摄的新玩法

https://mp.weixin.qq.com/s/z87Wp3yutq1l5bYfJS2YIA

谷歌新研究用深度学习合成运动模糊效果，手抖也能拍出摄影师级照片

https://mp.weixin.qq.com/s/B5XNmFlSnjEh2xAXB42pHQ

超十亿样本炼就的CNN助力图像质量增强，Adobe推出新功能“增强细节”

https://mp.weixin.qq.com/s/MEjZT_41w2cRqIYDi8a1rw

腾讯优图CVPR中标论文：不靠硬件靠算法，暗光拍照也清晰

https://mp.weixin.qq.com/s/Ek2eNeUPzEJiN6E1Yr6sMw

CVPR2019成像类论文拾英

https://mp.weixin.qq.com/s/qbPAQeJr7OWOwysa4_iDIw

基于深度学习的低光照图像增强方法总结（2017-2019）

https://zhuanlan.zhihu.com/p/56263560

单目视觉深度估计测距的前生今世

https://mp.weixin.qq.com/s/0K_NF84wvPJttEARVUGPWA

DeOccNet：国防科大提出阵列相机去除前景遮挡成像新方法

# LSM

liquid state machine (LSM)

http://www.docin.com/p-390935406.html

基于液体状态机的脑运动神经系统的建模研究

# DNC

https://zhuanlan.zhihu.com/p/27773709

浅析至强RNN可微分神经计算机(DNC)

https://zhuanlan.zhihu.com/p/27964341

浅析至强RNN可微分神经计算机(DNC)-2

https://zhuanlan.zhihu.com/p/28209628

DNC-3滚动分类的模式识别

https://zhuanlan.zhihu.com/p/28433712

DNC4广义线性回归

# Spiking Neuron Networks

除了基于BP算法的NN之外，Spiking Neuron Networks也是一大类NN。Spiking NN和人脑结构更相似，功耗也更小，但是相关训练和数据量化的算法尚不成熟，属于潜力股。

![](/images/img2/BrainChip_Fig2.gif)

![](/images/img3/Tianjic.png)

参考：

https://homepages.cwi.nl/~sbohte/publication/paugam_moisy_bohte_SNNChapter.pdf

Computing with Spiking Neuron Networks

https://mp.weixin.qq.com/s/6dpKSaLFVo-ge4gtbG8GQg

简述脉冲神经网络SNN：下一代神经网络

https://mp.weixin.qq.com/s/0n50YO1jIv_mxqe0EeS6kw

综述AI未来：神经科学启发的类脑计算

https://mp.weixin.qq.com/s/5KA7jtlRmnXxijGQhU1k4A

DeepMind哈萨比斯狂推的神经科学，入门需要看什么书？

https://mp.weixin.qq.com/s/TWdeHVCgEf54STvdA1QUPg

DeepMind哈萨比斯长文：伟大的AI离不开神经科学

https://mp.weixin.qq.com/s/8ibcyvyBLYArAMhQElqRzg

Cell研究揭示生物神经元强大新特性，是时候设计更复杂的神经网络了！

https://mp.weixin.qq.com/s/cb6JBlb11xW0Xw0RWI4vFA

浙大&川大提出脉冲版ResNet：继承ResNet优势，实现当前最佳

https://mp.weixin.qq.com/s/yaAuVpuhSGabOswKnv9q5Q

脉冲神经网络与小样本学习

https://mp.weixin.qq.com/s/m7UHX3XL5sC3oBdu3KoyOg

脉冲神经网络（SNN）概述

https://mp.weixin.qq.com/s/vwZfmyIEdEdpqJWKOSKYYw

清华天机AI芯片登Nature封面：全球首款异构融合类脑芯片，实现自行车无人驾驶

https://mp.weixin.qq.com/s/skA3NZIAzTrsnSsNCxCYSA

类脑计算背后的计算神经科学框架

# 深度时间序列

https://mp.weixin.qq.com/s/cChJO6YrE_XAgeInS7J1Vw

130页序列推荐系统教程重磅发布

https://www.intechopen.com/books/time-series-analysis-data-methods-and-applications

开源新书《时间序列分析，数据/方法/应用》，6章110页pdf带你了解最新进展

https://mp.weixin.qq.com/s/zv264-dqDQYRkYmjX_QZpQ

郑宇解读地理传感器时间序列预测问题

https://mp.weixin.qq.com/s/JwRXBNmXBaQM2GK6BDRqMw

Kaggle网站流量预测任务第一名解决方案：从模型到代码详解时序预测

https://mp.weixin.qq.com/s/caXnseARUwLIXdsZ7BXOUw

用于金融时序预测的神经网络：可改善移动平均线经典策略

http://mp.weixin.qq.com/s/9fJT0dMLvYQdfMVvSEiG4A

深度学习的时间序列模型评价

https://mp.weixin.qq.com/s/1Gdx-U3DRZtSJoFyCLnD0w

深度学习之Sequence Learning

https://mp.weixin.qq.com/s/SWKWI7BADnX43e-sCBxRPg

神经网络在算法交易上的应用系列——简单时序预测

https://mp.weixin.qq.com/s/Ux7XjLHzlaGFtM1uSMu2gQ

神经网络在算法交易上的应用系列——时序预测+回测

https://mp.weixin.qq.com/s/fUqQo0m7nMLZO85YG-duRw

神经网络在算法交易上的应用系列——多元时间序列

https://mp.weixin.qq.com/s/PS1SqSWckuHuyZP6d5ZUFw

“深度学习”信号处理和时序分析的最后选择？

https://zhuanlan.zhihu.com/p/54471673

基于前馈神经网络的时间序列异常检测算法

https://mp.weixin.qq.com/s/g9upS70qFOCFBMm-T5nI1A

利用深度学习最新前沿预测股价走势

https://mp.weixin.qq.com/s/otwmDtiDfVVID65RQgT4Uw

教你如何鉴别那些用深度学习预测股价的花哨模型？

https://mp.weixin.qq.com/s/xGUcqs3q3yNpVsJ8P7ag_g

以机器学习的视角来看时序点过程的最新进展

https://mp.weixin.qq.com/s/F0z5aEaigQLtlLfDoFIJXQ

时间序列预测：理论与实践教程，300多页PPT带你了解领域最新动态

https://zhuanlan.zhihu.com/p/83130649

深度学习在时间序列分类中的应用

https://mp.weixin.qq.com/s/09KFXwQLJ-HUJsrTd0B1HA

金融时序预测中的深度学习方法综述: 从2005到2019

https://mp.weixin.qq.com/s/iPpVT2iY4Ec6oYdsRpPeTQ

淘宝推荐系统中的深度序列匹配模型SDM

https://zhuanlan.zhihu.com/p/103012005

序列特征的处理方法之一：基于注意力机制方法

https://zhuanlan.zhihu.com/p/104216734

序列特征的处理方法之二：基于卷积神经网络方法

# AI可解释性

XAI(Explainable Artificial Intelligence)

https://github.com/pbiecek/xai_resources

AI可解释性资源汇总

https://mp.weixin.qq.com/s/XVl6voP5cwdC7DcvTMQvVQ

机器学习可解释性工具箱XAI

https://github.com/jphall663/awesome-machine-learning-interpretability

最全的机器学习可解释性资料

https://mp.weixin.qq.com/s/OV4vXu7TAuyV7qU9BAMF6g

机器学习模型的“可解释性”到底有多重要？

https://mp.weixin.qq.com/s/33VQNVvb7JGlk10Jc3mmeg

从可视化到新模型：纵览深度学习的视觉可解释性

https://github.com/ModelOriented/DrWhy

可解释AI(XAI)工具集—DrWhy

https://mp.weixin.qq.com/s/1OODeAFaRLFK3elECyZcng

机器学习模型可解释性的详尽介绍
