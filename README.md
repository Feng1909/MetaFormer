# MetaFormer

论文地址：[MetaFormer is Actually What You Need for Vision](https://arxiv.org/abs/2111.11418)
项目地址：https://aistudio.baidu.com/aistudio/projectdetail/4216419

## 简介
Transformer已经证明在计算机视觉任务中有非常大的潜力，一种普遍的看法是基于attention的**token mixer**模块使transformer具有竞争力。但是将attention用**spatial MLP**替代后，模型仍然具有非常好的效果。那么是不是**transformer的结构**而不是attention使其有效呢？作者使用**池化层**代替transformer中的**attention**，构建了**PoolFormer**模型，取得了非常好的效果，ImageNet-1k准确率达到82.1%。证明了Transformer结构的有效性，而非attention。

本文提出**MetaFormer**：一种从Transformer中抽象出来的**通用架构**，没有指定token mixer，并提出PoolFormer基线在分类、检测和分割任务上进行验证。本次复现在**分类任务**上进行验证实验。各种模型的对比如下图：

![](https://ai-studio-static-online.cdn.bcebos.com/e084fdecc43c4b989783b938f85fe76163d7a9aa69304ef2b6a197a4d6adb43c)

PoolFormer的网络结构非常简单，只需要把Transformer的Attention模块换成Pooling就可以：

![](https://ai-studio-static-online.cdn.bcebos.com/e8eb1384155f42fab8642779150f8fc67d7b2413673e4e2481fe358690a17d69)

不同的Pooling模块可以有不同的配置：

![](https://ai-studio-static-online.cdn.bcebos.com/4a3ef9fc51a844f8a0485da4808ac1b5cf199f56caf4420b87953a6052ad523e)

针对PoolFormer的复现在AiStudio中已经存在，本复现针对**MetaFormer**，并完整复现不同大小网络的MetaFormer

## Cifar10数据集

链接：http://www.cs.toronto.edu/~kriz/cifar.html

![](https://ai-studio-static-online.cdn.bcebos.com/15a8790a113d41418d6fc8563aeb4acd10da73b4b8c6488599fa9e7a01cc0833)

**CIFAR-10**是一个更接近普适物体的彩色图像数据集。CIFAR-10 是由Hinton 的学生Alex Krizhevsky 和Ilya Sutskever 整理的一个用于识别普适物体的小型数据集。一共包含10 个类别的RGB彩色图片：**飞机**(airplane)、**汽车**(automobile)、**鸟类**(bird)、**猫**(cat)、**鹿**(deer)、**狗**(dog)、**蛙类**(frog)、**马**(horse)、**船**(ship)和**卡车**(truck).

每个图片的尺寸为 $32\times 32$，每个类别有**6000**个图像，数据集中一共有**50000**张训练图片和**10000**张测试图片。
