---
layout: post
title:  Attention（四）——BERT（2）
category: Attention 
---

# BERT

## ERNIE（续）

https://mp.weixin.qq.com/s/FoX2bXCJlFYjb9U6JcZCqg

超详细中文预训练模型ERNIE使用指南

https://mp.weixin.qq.com/s/EYQXM-1WSommj9mKJZVVzw

百度正式发布ERNIE 2.0，16项中英文任务超越BERT、XLNet，刷新SOTA

https://mp.weixin.qq.com/s/PwiVCgN8dDWXTGZsiqM-2g

最新NLP架构的直观解释：多任务学习–ERNIE 2.0

https://mp.weixin.qq.com/s/yZvKMaBZyodr8SLvcAn7Mg

深度剖析知识增强语义表示模型——ERNIE

## XLNet

https://mp.weixin.qq.com/s/29y2bg4KE-HNwsimD3aauw

20项任务全面碾压BERT，CMU全新XLNet预训练模型屠榜

https://mp.weixin.qq.com/s/itNtDuQS4KF_sLnfiwdyNg

拆解XLNet模型设计，回顾语言表征学习的思想演进

https://mp.weixin.qq.com/s/2zuR0x-Cb1NTeRHYeTjrHQ

一文详解Google最新NLP模型XLNet

https://mp.weixin.qq.com/s/t8XDCPOYna8mZ1Iqk_g7Zw

最新语言表示方法XLNet

https://zhuanlan.zhihu.com/p/70257427

XLNet:运行机制及和Bert的异同比较

https://mp.weixin.qq.com/s/SAiIIa9_-16dqRMKASsuhw

追溯XLNet的前世今生：从Transformer到XLNet

https://mp.weixin.qq.com/s/qzAN6VlKcfqmpX9kQCJ7Gg

XLnet：GPT和BERT的合体，博采众长，所以更强

https://zhuanlan.zhihu.com/p/80216580

XLnet：集合了GPT和BERT的预训练模型

https://mp.weixin.qq.com/s/7ZTDJmsOxOwJ7fYUxK6eTw

XLNet详解

## 轻量化BERT

| Paper | Prune | Factor | Distill | W. Sharing | Quant. | Pre-train | Downstream |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| Compressing BERT: Studying the Effects of Weight Pruning on Transfer Learning | Y |  |  |  |  | Y | Y |
| Are Sixteen Heads Really Better than One? | Y |  |  |  |  |  | Y |
| Pruning a BERT-based Question Answering Model | Y |  |  |  |  |  | Y |
| Reducing Transformer Depth on Demand with Structured Dropout | Y |  |  |  |  | Y |  |
| Reweighted Proximal Pruning for Large-Scale Language Representation | Y |  |  |  |  | Y |  |
| Structured Pruning of Large Language Models |  | Y |  |  |  |  | Y |
| ALBERT: A Lite BERT for Self-supervised Learning of Language Representations |  | Y |  | Y |  | Y |  |
| Extreme Language Model Compression with Optimal Subwords and Shared Projections |  |  | Y |  |  | Y |  |
| DistilBERT, a distilled version of BERT: smaller, faster, cheaper and lighter |  |  | Y |  |  | Y |  |
| Distilling Task-Specific Knowledge from BERT into Simple Neural Networks |  |  | Y |  |  |  | Y |
| Distilling Transformers into Simple Neural Networks with Unlabeled Transfer Data |  |  | Y |  |  |  | Y |
| Attentive Student Meets Multi-Task Teacher: Improved Knowledge Distillation for Pretrained Models |  |  | Y |  |  | Multi-task  | Y |
| Patient Knowledge Distillation for BERT Model Compression |  |  | Y |  |  |  | Y |
| TinyBERT: Distilling BERT for Natural Language Understanding |  |  | Y |  |  | Y | Y |
| MobileBERT: Task-Agnostic Compression of BERT by Progressive Knowledge Transfer |  |  | Y |  |  | Y |  |
| Q8BERT: Quantized 8Bit BERT |  |  |  |  | Y |  | Y |
| Q-BERT: Hessian Based Ultra Low Precision Quantization of BERT |  |  |  |  | Y |  | Y |

https://www.zhihu.com/question/347898375

如何看待瘦身成功版BERT——ALBERT？

https://mp.weixin.qq.com/s/a0d0b1jSm5HxHso9Lz8MSQ

小版BERT也能出奇迹：最火的预训练语言库探索小巧之路

https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650771134&idx=2&sn=012082a897dbf125000e38b73520c51d

TinyBERT：模型小7倍，速度快8倍，华中科大、华为出品

https://mp.weixin.qq.com/s/i82wGiSOlA4l4ozimrE2gg

加速BERT模型有多少种方法？从架构优化、模型压缩到模型蒸馏最新进展详解！

https://mp.weixin.qq.com/s/R2MW_5kskvXyuSOh7kfJaA

ALBERT：更轻更快的NLP预训练模型

https://mp.weixin.qq.com/s/dWzpqP_U8Y5DyfWHVTl5Vg

BERT瘦身之路：Distillation，Quantization，Pruning

https://mp.weixin.qq.com/s/DAsY9-Dl5T6peo_71ICOtw

基于ALBERT的文本相似度计算

http://mitchgordon.me/machine/learning/2019/11/18/all-the-ways-to-compress-BERT.html

15篇论文全面概览BERT压缩方法

https://mp.weixin.qq.com/s/5tYuP09dtkmYYGX2R-mCPQ

从transformer到albert

## AR vs AE

**AR**: Aotoregressive Lanuage Modeling，又叫自回归语言模型。它指的是，依据前面(或后面)出现的tokens来预测当前时刻的token，代表模型有ELMO、GTP等。

$$\text{forward:}p(x)=\prod_{t=1}^Tp(x_t|x_{<t})$$

$$\text{backward:}p(x)=\prod_{t=T}^1p(x_t|x_{>t})$$

- 缺点：它只能利用单向语义而不能同时利用上下文信息。ELMO通过双向都做AR模型，然后进行拼接，但从结果来看，效果并不是太好。

- 优点：对自然语言生成任务(NLG)友好，天然符合生成式任务的生成过程。这也是为什么GPT能够编故事的原因。

**AE**:Autoencoding Language Modeling，又叫自编码语言。通过上下文信息来预测当前被mask的token，代表有BERT，Word2Vec(CBOW)。

$$p(x)=\prod_{x\in Mask}p(x_t|context)$$

- 缺点：由于训练中采用了MASK标记，导致预训练与微调阶段不一致的问题。此外对于生成式问题，AE模型也显得捉襟见肘，这也是目前BERT为数不多没有实现大的突破的领域。

- 优点：能够很好的编码上下文语义信息，在自然语言理解(NLU)相关的下游任务上表现突出。

## 参考

https://www.zhihu.com/question/298203515

如何评价BERT模型？

https://mp.weixin.qq.com/s/Fao3i99kZ1a6aa3UhAYKhA

全面超越人类！Google称霸SQuAD，BERT横扫11大NLP测试

https://mp.weixin.qq.com/s/INDOBcpg5p7vtPBChAIjAA

最强预训练模型BERT的Pytorch实现

https://mp.weixin.qq.com/s/SZMYj4rMneR3OWST007H-Q

解读谷歌最强NLP模型BERT：模型、数据和训练

https://mp.weixin.qq.com/s/8uZ2SJtzZhzQhoPY7XO9uw

详细解读谷歌新模型BERT为什么嗨翻AI圈

https://zhuanlan.zhihu.com/p/66053631

BERT

https://mp.weixin.qq.com/s/CofeiL4fImq98UeuJ4hWTg

预训练BERT，官方代码发布前他们是这样用TensorFlow解决的

https://mp.weixin.qq.com/s/vFdm-UHns7Nhbmdoiu6jWg

谷歌终于开源BERT代码：3亿参数量，机器之心全面解读

https://mp.weixin.qq.com/s/dV4RkxZOC9o2BxNi0GljKQ

谷歌最强NLP模型BERT官方中文版来了！多语言模型支持100种语言

https://mp.weixin.qq.com/s/fz-bQMAi5bs2_bvRhf3ERg

从Word Embedding到Bert模型—自然语言处理中的预训练技术发展史

https://mp.weixin.qq.com/s/k_33UK1RkMyHn6TSudU6Kg

详解谷歌最强NLP模型BERT

https://mp.weixin.qq.com/s/d2MZQbamdo0EC_MVtf-HZA

BERT详解：开创性自然语言处理框架的全面指南

https://mp.weixin.qq.com/s/pD4it8vQ-aE474uSMQG0YQ

两行代码玩转Google BERT句向量词向量

https://mp.weixin.qq.com/s/osmUZxAAX3x-oTHYJbzemA

谷歌BERT模型fine-tune终极实践教程

https://mp.weixin.qq.com/s/XmeDjHSFI0UsQmKeOgwnyA

小数据福音！BERT在极小数据下带来显著提升的开源实现

https://mp.weixin.qq.com/s/HXYDO5PM8UIoXgEPGe8p-w

图解当前最强语言模型BERT：NLP是如何攻克迁移学习的？

https://mp.weixin.qq.com/s/zz3j9HEuzw5e92MQXxSQsA

遗珠之作？谷歌Quoc Le这篇NLP预训练模型论文值得一看

https://mp.weixin.qq.com/s/IN4YfoZnlBozwEFdhSvLZg

用可视化解构BERT，我们从上亿参数中提取出了6种直观模式

https://mp.weixin.qq.com/s/nIT3GIU0dUIYyGChxsiOWw

Google BERT应用之《红楼梦》对话人物提取

https://mp.weixin.qq.com/s/dcp_ANYijRmicMYX7OpJmA

如何用最强模型BERT做NLP迁移学习？

https://mp.weixin.qq.com/s/DR4SkgOfUT7KYiaXm5NynQ

跨语言版BERT：Facebook提出跨语言预训练模型XLM

https://mp.weixin.qq.com/s/epjjHmlmMFhWtRO_cCUITA

用BERT进行多标签文本分类

https://mp.weixin.qq.com/s/Wk6gvOS_Qnud6ib1esMFXA

加入Transformer-XL，这个PyTorch包能调用各种NLP预训练模型！

https://mp.weixin.qq.com/s/GqqU3Ixht1BzMnQeRYQEqQ

谷歌NLP深度学习模型BERT特征的可解释性表现怎么样？

https://mp.weixin.qq.com/s/2f91Ksj19rk_emoFpEmPfA

从BERT看大规模数据的无监督利用

https://mp.weixin.qq.com/s/g6-NjoFMPpxjsh38X-wTFQ

BERT，GPT-2这些顶尖工具到底该怎么用到我的模型里?

https://mp.weixin.qq.com/s/N6xBFZ82dkSGCbj6vC5nLQ

上下文预训练模型最全整理：原理、应用、开源代码、数据分享

https://mp.weixin.qq.com/s/-6XpuO7_ve_EdSPCMeWE7g

Attention isn’t all you need！BERT的力量之源远不止注意力

https://mp.weixin.qq.com/s/Y2bs2QegRadSR7lbiFFnWg

BERT一作Jacob Devlin斯坦福演讲PPT：BERT介绍与答疑

https://zhuanlan.zhihu.com/p/58425003

从Word2Vec到Bert，聊聊词向量的前世今生（一）

https://mp.weixin.qq.com/s/SfMIKfF_B4agFCHN_U_mzQ

BAM！利用知识蒸馏和多任务学习构建的通用语言模型

https://mp.weixin.qq.com/s/6G5Mu7-1omGtQ_9Gt9lUBw

基于预训练自然语言生成的文本摘要方法

https://mp.weixin.qq.com/s/yysnPauB22YgprpOi1ZWSQ

深入理解BERT Transformer，不仅仅是注意力机制

https://mp.weixin.qq.com/s/kFABJJ3fBC48-4DXK8PERQ

10大任务超越BERT，微软提出多任务深度神经网络MT-DNN

https://mp.weixin.qq.com/s/jlGfxkT_o9sgFlUuR_x5Tw

微软开源用于学习通用语言嵌入的MT-DNN模型

https://mp.weixin.qq.com/s/D68YzjYvpc2epGWFBP6rIQ

谷歌实习生新算法提速惊人！BERT训练从三天三夜，缩短到一个小时

https://mp.weixin.qq.com/s/iDGofh_ycWJzfqQriPEXGQ

如何用Python和BERT做中文文本二元分类？

https://zhuanlan.zhihu.com/p/62308732

浅谈Bert：语言理解中的预训练编码器

https://mp.weixin.qq.com/s/1Cz6js4kYdvc8g4oKjVPeA

BERT烹饪之法：fintune的艺术

https://mp.weixin.qq.com/s/nVM2Kxc_Mn7BAC6-Pig2Uw

BERT模型的标准调优和花式调优

https://mp.weixin.qq.com/s/FwmEIZ3ugeZBbLIGHmH-_g

BERT之后，GLUE基准升级为SuperGLUE：难度更大

https://mp.weixin.qq.com/s/SDVxn3Ra1dKmr-XgKNg5IA

罗玲：From Word Representation to BERT

https://mp.weixin.qq.com/s/-bh8BL4LxnevS8xnW5U9ZA

中科院自动化所提出BIFT模型：面向自然语言生成，同步双向推断

https://mp.weixin.qq.com/s/7yCnAHk6x0ICtEwBKxXpOw

序列到序列自然语言生成任务超越BERT、GPT！微软提出通用预训练模型MASS

https://mp.weixin.qq.com/s/7sIUaSON53hsXUJjq8uVUA

马聪：NLP中的生成式预训练模型

https://mp.weixin.qq.com/s/s1bQFdA6gtoHeeQMJKQ8UQ

Bert时代的创新：Bert应用模式比较及其它

https://mp.weixin.qq.com/s/zqlWx3e4LOJ3_Zy2DEbCjw

从语言模型看Bert的善变与GPT的坚守

https://mp.weixin.qq.com/s/LngE10Hnqe9bgFzpNfUwLQ

NLP中的词向量对比：word2vec/glove/fastText/elmo/GPT/bert
