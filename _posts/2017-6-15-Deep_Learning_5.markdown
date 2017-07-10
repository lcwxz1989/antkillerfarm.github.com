---
layout: post
title:  深度学习（五）——Attention, seq2seq, DMN, CNN进化史
category: theory 
---

# Attention

倒序句子这种方法属于“hack”手段。它属于被实践证明有效的方法，而不是有理论依据的解决方法。

大多数翻译的基准都是用法语、德语等语种，它们和英语非常相似（即使汉语的词序与英语也极其相似）。但是有些语种（像日语）句子的最后一个词语在英语译文中对第一个词语有高度预言性。那么，倒序输入将使得结果更糟糕。

还有其它办法吗？那就是Attention机制。

![](/images/article/attention.png)

上图是Attention机制的结构图。y是编码器生成的译文词语，x是原文的词语。上图使用了双向递归网络，但这并不是重点，你先忽略反向的路径吧。重点在于现在每个解码器输出的词语$$y_t$$取决于所有输入状态的一个权重组合，而不只是最后一个状态。a是决定每个输入状态对输出状态的权重贡献。因此，如果$$a_{3,2}$$的值很大，这意味着解码器在生成译文的第三个词语时，会更关注于原文句子的第二个状态。a求和的结果通常归一化到1（因此它是输入状态的一个分布）。

Attention机制的一个主要优势是它让我们能够解释并可视化整个模型。举个例子，通过对attention权重矩阵a的可视化，我们能够理解模型翻译的过程。

![](/images/article/attention_2.png)

我们注意到当从法语译为英语时，网络模型顺序地关注每个输入状态，但有时输出一个词语时会关注两个原文的词语，比如将“la Syrie”翻译为“Syria”。

如果再仔细观察attention的等式，我们会发现attention机制有一定的成本。我们需要为每个输入输出组合分别计算attention值。50个单词的输入序列和50个单词的输出序列需要计算2500个attention值。这还不算太糟糕，但如果你做字符级别的计算，而且字符序列长达几百个字符，那么attention机制将会变得代价昂贵。

attention机制解决的根本问题是允许网络返回到输入序列，而不是把所有信息编码成固定长度的向量。正如我在上面提到，我认为使用attention有点儿用词不当。换句话说，attention机制只是简单地让网络模型访问它的内部存储器，也就是编码器的隐藏状态。在这种解释中，网络选择从记忆中检索东西，而不是选择“注意”什么。不同于典型的内存，这里的内存访问机制是弹性的，也就是说模型检索到的是所有内存位置的加权组合，而不是某个独立离散位置的值。弹性的内存访问机制好处在于我们可以很容易地用反向传播算法端到端地训练网络模型（虽然有non-fuzzy的方法，其中的梯度使用抽样方法计算，而不是反向传播）。

论文：

《Learning to combine foveal glimpses with a third-order Boltzmann machine》

《Learning where to Attend with Deep Architectures for Image Tracking》

《Neural Machine Translation by Jointly Learning to Align and Translate》

参考：

http://blog.csdn.net/malefactor/article/details/50550211

自然语言处理中的Attention Model

https://yq.aliyun.com/articles/65356

图文结合详解深度学习Memory & Attention

http://www.cosmosshadow.com/ml/%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C/2016/03/08/Attention.html

Attention

http://geek.csdn.net/news/detail/50558

深度学习和自然语言处理中的attention和memory机制

https://zhuanlan.zhihu.com/p/25928551

用深度学习（CNN RNN Attention）解决大规模文本分类问题-综述和实践

http://blog.csdn.net/leo_xu06/article/details/53491400

视觉注意力的循环神经网络模型

https://mp.weixin.qq.com/s/xr_1ZYbvADMMwgxLEAflCw

如何在语言翻译中理解Attention Mechanism？

# seq2seq

seq2seq最早用于Neural Machine Translation领域（与之相对应的有Statistical Machine Translation）。训练后的seq2seq模型，可以根据输入语句，自动生成翻译后的输出语句。

![](/images/article/seq2seq.png)

上图是seq2seq的结构图。可以看出seq2seq实际上是一种Encoder-Decoder结构。

在Encoder阶段，RNN依次读入输入序列。但由于这时，没有输出序列与之对应，因此这仅仅相当于一个对隐层的编码过程，即将句子的语义编码为隐层的状态向量。

从中发现一个问题：状态向量的维数决定了存储的语义的内容上限（显然不能指望，一个200维的向量，能够表示一部百科全书。）因此，seq2seq通常只用于短文本的翻译。

在Decoder阶段，我们根据输出序列，反向修正RNN的参数，以达到训练神经网络的目的。

参考：

https://github.com/ematvey/tensorflow-seq2seq-tutorials

一步步的seq2seq教程

http://blog.csdn.net/sunlylorn/article/details/50607376

seq2seq模型

http://datartisan.com/article/detail/120.html

Seq2Seq的DIY简介

http://www.cnblogs.com/Determined22/p/6650373.html

DL4NLP——seq2seq+attention机制的应用：文档自动摘要（Automatic Text Summarization）

http://blog.csdn.net/young_gy/article/details/73412285

基于RNN的语言模型与机器翻译NMT

http://karpathy.github.io/2015/05/21/rnn-effectiveness/

The Unreasonable Effectiveness of Recurrent Neural Networks

https://mp.weixin.qq.com/s/8u3v9XzECkwcNn5Ay-kYQQ

基于Depthwise Separable Convolutions的Seq2Seq模型_SliceNet原理解析

# DMN

Question answering是自然语言处理领域的一个复杂问题。它需要对文本的理解力和推理能力。大部分NLP问题都可以转化为一个QA问题。Dynamic Memory Networks可以用来处理QA问题。DMN的输入包含事实输入，问题输入，经过内部处理形成片段记忆，最终产生问题的答案。

DMN可进行端到端的训练，并在多种任务上取得了state-of-the-art的效果：包括QA（Facebook 的 bAbI 数据集），情感分析文本分类（Stanford Sentiment Treebank）和词性标注（WSJ-PTB）。

![](/images/article/DMN.png)

参考：

http://blog.csdn.net/javafreely/article/details/71994247

动态记忆网络

# CNN进化史

## 计算机视觉

![](/images/article/computer_vision.jpg)

6大关键技术：

![](/images/article/computer_vision_2.jpg)

**图像分类**：根据图像的主要内容进行分类。数据集：MNIST, CIFAR, ImageNet

**物体定位**：预测包含主要物体的图像区域，以便识别区域中的物体。数据集：ImageNet

**物体识别**：定位并分类图像中出现的所有物体。这一过程通常包括：划出区域然后对其中的物体进行分类。数据集：PASCAL, COCO

**语义分割**：把图像中的每一个像素分到其所属物体类别，在样例中如人类、绵羊和草地。数据集：PASCAL, COCO

**实例分割**：把图像中的每一个像素分到其所属物体实例。数据集：PASCAL, COCO

**关键点检测**：检测物体上一组预定义关键点的位置，例如人体上或者人脸上的关键点。数据集：COCO

## CNN简史

![](/images/article/computer_vision_3.jpg)

![](/images/article/CNN_3.png)

## AlexNet

2012年，ILSVRC比赛冠军的model——Alexnet（以第一作者Alex命名）的结构图如下：

![](/images/article/AlexNet.png)

换个视角：

![](/images/article/AlexNet_2.png)

AlexNet的caffe模板：

https://github.com/BVLC/caffe/blob/master/models/bvlc_alexnet/deploy.prototxt

其中的LRN（Local Response Normalization）层也是当年的遗迹，被后来的实践证明，对于最终效果和运算量没有太大帮助，因此也就慢慢废弃了。

虽然，LeNet-5是CNN的开山之作（它不是最早的CNN，但却是奠定了现代CNN理论基础的模型），但是毕竟年代久远，和现代实用的CNN相比，结构实在过于原始。

AlexNet作为第一个现代意义上的CNN，它的意义主要包括：

1.Data Augmentation。包括水平翻转、随机裁剪、平移变换、颜色、光照变换等。

2.Dropout。

3.ReLU激活函数。

4.多GPU并行计算。

5.当然最应该感谢的是李飞飞团队搞出来的标注数据集合ImageNet。

>注：ILSVRC（Large Scale Visual Recognition Challenge）大赛，在2016年以前，一直是CV界的顶级赛事。但随着技术的成熟，目前的科研重点已经转移到了其他领域。

## VGG

Visual Geometry Group是牛津大学的一个科研团队。他们推出的一系列深度模型，被称作VGG模型。

VGG的结构图如下：

![](/images/article/vgg.png)

该系列包括A/A-LRN/B/C/D/E等6个不同的型号。其中的D/E，根据其神经网络的层数，也被称为VGG16/VGG19。

从原理角度，VGG相比AlexNet并没有太多的改进。其最主要的意义就是实践了“**神经网络越深越好**”的理念。也是自那时起，神经网络逐渐有了“深度学习”这个别名。

## GoogleNet

GoogleNet的进化道路和VGG有所不同。VGG实际上就是“大力出奇迹”的暴力模型，其他地方不足称道。

而GoogleNet不仅继承了VGG“越深越好”的理念，对于网络结构本身也作了大胆的创新。可以对比的是，AlexNet有60M个参数，而GoogleNet只有4M个参数。

因此，在ILSVRC 2014大赛中，GoogleNet获得第一名，而VGG屈居第二。

![](/images/article/GoogleNet.jpg)

上图是GoogleNet的结构图。从中可以看出，GoogleNet除了AlexNet的基本要素之外，还有被称作Inception的结构。

![](/images/article/inception.png)

上图是Inception的结构图。它的原理实际上就是**将不同尺寸的卷积组合起来，以提供不同尺寸的特征**。

原始的GoogleNet也被称作Inception-v1。在后面的几年，GoogleNet还提出了几种改进的版本，最新的一个是Inception-v4（2016.8）。

论文：

《Inception-v4, Inception-ResNet and the Impact of Residual Connections on Learning》

Inception系列的改进方向基本都集中在构建不同的Inception模型上。

GoogleNet的另一个改进是**减少了全连接层**（Full Connection, FC），这是减少模型参数的一个重要改进。事实上，在稍后的实践中，人们发现去掉VGG的第一个FC层，对于效果几乎没有任何影响。

## 参考

http://mp.weixin.qq.com/s/ZKMi4gRfDRcTxzKlTQb-Mw

计算机视觉识别简史：从AlexNet、ResNet到Mask RCNN

http://mp.weixin.qq.com/s/kbHzA3h-CfTRcnkViY37MQ

详解CNN五大经典模型:Lenet，Alexnet，Googlenet，VGG，DRL

https://zhuanlan.zhihu.com/p/22094600

Deep Learning回顾之LeNet、AlexNet、GoogLeNet、VGG、ResNet

http://www.leiphone.com/news/201609/303vE8MIwFC7E3DB.html

Google最新开源Inception-ResNet-v2，借助残差网络进一步提升图像分类水准

http://mp.weixin.qq.com/s/2TUw_2d36uFAiJTkvaaqpA

解读Keras在ImageNet中的应用：详解5种主要的图像识别模型

https://zhuanlan.zhihu.com/p/27642620

YJango的卷积神经网络——介绍

https://www.zybuluo.com/coolwyj/note/202469

ImageNet Classification with Deep Convolutional Neural Networks

http://simtalk.cn/2016/09/20/AlexNet/

AlexNet简介

http://simtalk.cn/2016/09/12/CNNs/

CNN简介

http://www.cnblogs.com/Allen-rg/p/5833919.html

GoogLeNet学习心得
