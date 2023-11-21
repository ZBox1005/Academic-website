---
title: Paper Reading - Multi-Modal Classifiers for Open-Vocabulary Object Detection
subtitle: ''

# Summary for listings and search engines
summary: 论文的主要贡献有三：
  1.  提出了一个LLM来生成目标类别的高质量语言描述，并建立了一个强大的文本分类器。
  2.  采用了一个图像示例聚合器，可以接收任意数量的图像作为输入，构建视觉分类器。
  3.  提出了一个简单的方法来融合语言描述和图像示例的信息，得到了一个多模态分类器。

# Link this post with a project
projects: []

# Date published
date: '2023-11-03T00:00:00Z'

# Date updated
lastmod: '2023-11-03T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Paper Reading

categories:
  - MLLM
---
## Abstract

离群点暴露（OE）在分布外（OOD）检测中非常强大，它通过使用代理 OOD 数据对模型进行微调来提高检测能力。然而，代理数据通常偏离测试 OOD 数据。因此，在面对未见过的 OOD 数据时，OE 的性能会被削弱。

为了解决这个问题，我们提出了一种基于 OE 的新方法，该方法能使模型在不可见的 OOD 情况下表现良好。它提出了一种最小-最大学习方案--搜索并综合导致最差判断的 OOD 数据，并从这些 OOD 数据中学习，以获得统一的 OOD 检测性能。

在我们的实现过程中，这些最差的 OOD 数据是通过转换原始代理数据而合成。具体来说，相关的转换函数是基于我们对模型扰动导致数据转换的新见解而隐式学习。我们的方法提供了一种合成 OOD 数据的有效途径，除了代理 OOD 数据外，它还能使检测模型进一步受益。我们在各种 OOD 检测设置下进行了广泛的实验，证明了我们的方法与先进的同类方法相比的有效性。

## Introduction

开放世界中的深度学习系统经常会遇到分布外（OOD）数据，这些数据的标签空间与分布内（ID）样本的标签空间是不相交的。

对于许多安全关键型应用来说，深度模型应该对 ID 数据做出**可靠的预测**，而 OOD 情况则应作为**异常情况**报告。这就导致了众所周知的 OOD 检测问题，该问题在可信机器学习领域引起了广泛关注。

由于深度模型在面对 OOD 数据时可能过于自信，因此 OOD 检测仍然不是一件容易的事。在判别模型的基础上，现有的 OOD 检测方法一般可分为两类，即posthoc方法和fine-tuning方法。

1. Posthoc事后方法：假定在 ID 数据上有一个训练有素的模型及其固定参数，利用模型响应设计各种**评分函数**来表示 ID 和 OOD 情况。
2. fine-tuning微调方法：允许调整目标模型，通过正则化提高其检测能力。通常，微调方法得益于训练过程中对**未知因素**的明确了解，因此通常能在各种实际情况下显示出可靠的性能。

微调方法中，离群点暴露（OE）是最有效的方法之一，它在训练过程中使用代理 OOD 数据来辨别 ID 和 OOD 模式。通过使这些代理OOD 数据以低置信度预测，OE使检测模型能够学习有效检测 OOD 的知识。

需要注意，我们很难知道在部署模型时会遇到什么样的 OOD 数据，因而在代理（训练时间）和未见（测试时间）OOD 案例之间存在分布差距。从根本上说，这种分布差距对 OOD 检测是有害的，因为当测试时的OOD 数据与训练时OOD 数据有很大偏差时很难保证模型的性能。

对于 OE 而言，解决 **OOD 分布差距**问题至关重要也极具挑战性。与该问题相关的几项研究通常通过让模型从**额外的** OOD 数据中学习来缩小差距。如，

1. Lee 等人（2018a）合成生成模型判别出错的OOD 数据，这部分合成数据由检测模型作**低置信度预测**。然而，合成未见数据在一般情况下是难以实现的（Du 等人，2022 年），这意味着相应的数据可能无法完全有益于 OE 训练。
2. 相反，Zhang 等人（2023 年）将 ID 和代理 OOD 数据**混合**起来，以扩大 OOD 案例的覆盖范围；Du 等人（2022 年）从**低维特征空间**中类条件分布的低似然区采样 OOD 数据。然而，前者的**线性插值**难以覆盖各种 OOD 情况，而后者的特征空间数据生成可能无法使**底层特征提取器**充分受益。因此，要解决 OE 中的 OOD 分布差距问题，还有很长的路要走。

为了克服上述弊端，我们提出了一种简单而强大的方法来获取额外的 OOD 数据，将现有的代理数据转换为新的 OOD 数据，使我们的检测模型进一步受益。其关键在于，**模型扰动会隐含地导致数据转换**，而检测模型可以在扰动后通过**模型更新**从这些隐含数据中学习。相关的变换函数摆脱了繁琐的人工设计（Zhang 等人，2023；Huang 等人，2023）和复杂的生成模型（Lee 等人，2018b），同时对于偏离原始数据的合成 OOD 数据保持灵活性。在此，有两个因素支持我们的数据合成的有效性：

1. 隐含数据遵循与原始数据不同的分布
2. 考虑到我们的检测模型足够深入，原始数据和转换后的数据分布之间的差异可以非常大。这表明，我们可以有效地合成与原始数据**大不相同的**额外 OOD 数据。然后，我们可以从这些数据中学习，进一步完善检测模型。

因此，我们提出了**分布无关的离群点检测**（*Distributional-agnostic Outlier Exposure*，DOE），这是一种基于隐式数据转换的新型离群点检测方法。“分布无关”一词反映了我们的最终目标，即在训练过程中只访问 ID 和代理 OOD 数据，使检测模型在各种未见（测试阶段）的OOD 分布情况下表现一致。

在 DOE 中，我们用候选 OOD 分布集的**最差** OOD 遗憾值（*worst OOD regret*, WOR）来衡量模型在 OOD 检测中的性能，从而得出如公式 6 所示的**最小-最大学习方案**。然后，基于我们系统化的隐式数据合成方法，我们在以下两个方面进行迭代：1）通过**模型扰动**搜索导致大 WOR 的隐式 OOD 数据；2）从这些数据中学习检测模型的均匀检测能力。

DOE 与分布稳健优化（*distributionally robust optimization,* DRO）相关，后者同样是从最坏情况分布中学习。图 1 总结了它们的概念比较。其中，DRO 考虑的是封闭世界环境，力求在支持中的**各种数据分布方面表现一致**（Sagawa 等人，2020 年）。然而，在需要检测未见数据的**开放世界 OOD** 设置中（参见第 5.3 节），也就是图 1（b）中与代理数据不相交的测试支持部分，它却失效了。相比之下，我们的数据转换提供了一种从未曾见过的数据中学习的有效方法，考虑到了区域在**支持之外**的均匀性能。因此，DOE 可以在一定程度上缓解分布差距问题，图 1(c) 中的不相交区域小于 DRO 案例就反映了这一点。

性能提升：在普通 OOD 检测(common OOD detection)方面，与 CIFAR-10、CIFAR-100 和 ImageNet 数据集上的原始 OE 相比，我们的 DOE 将平均 **FPR95** 降低了 7.26%、20.30% 和 13.97%。

在困难OOD 检测(hard OOD detection)方面，与各种困难OOD 数据集上的先进方法相比，我们的 DOE 将 **FPR95** 降低了 7.45%、7.75% 和 4.09%。

## Preliminary

$D_{ID}$：$X*Y$

$D_{OOD}$: 无关分布，其label和Y没有交集，在训练阶段也不可见

### Softmax Scoring

利用maximum softmax prediction，设定了一个阈值来在测试阶段判断输入是来自$D_{ID}$还是$D_{OOD}$。
$$
s_{\mathrm{MSP}}(\boldsymbol{x} ; h)=\max _{k} \operatorname{softmax}_{k} h(\boldsymbol{x}),
$$
由于OOD的label与Y没有交集，其softmax的结果会小于来自$D_{ID}$的样本。

### Outlier Exposure

MSP可能会对某些OOD数据做出**过于自信（置信度不低反高）**的预测，不利于有效的OOD检测。

因此，OE通过学习代理OOD分布$D_{OOD}^s$来提升MSP模型h(-)的检测性能。

![image-20231111181051383](static/uploads/paper-ood/formula1.png)

l_CE为交叉熵，l_OE为均匀分布的KL散度，可以写成：

![image-20231111181323822](static/uploads/paper-ood/formula2.png)

l_OE使得h(-)学习代理OOD数据为低置信度。由于模型可以在训练阶段看到部分OOD数据，OE在OOD检测中的性能是可信的。

然而，代理的OOD数据$D_{OOD}^s$与真实世界的$D_{OOD}$区别相当大，这也导致了训练-$D_{OOD}^s$与测试-$D_{OOD}$之间存在gap。在部署时，模型会继承这种数据偏差，可能会对与代理OOD不同的真实OOD又做出过于自信的预测（OE在真实OOD下是失效的）。