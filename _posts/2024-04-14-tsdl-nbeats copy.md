---
layout:       post
title:        "TSF-nbeats"
author:       "cyalcher"
header-style: text
catalog:      true
tags:
    - time series forecast
    - nbeats
---

# 一、背景
对已知的深度时间序列模型知道，但是总是不能很好知道其适应的问题及能力边界，现在通过经典时间序列样本对齐能力边界进行探索；

# 二、目标
完成基础应用，尝试复现论文结果，尝试其他的数据集；
# 三、实施过程
## 3.1 理论总结
从网上资源找到已有的模型能力总结：
1. 模型是加法；可以对应到cv领域的resnet架构；
2. 作者心得：① 2个stack ② 3个block ④ 参数可共享 ⑤ 再加1个 generic block ⑥ 经验公式：输入历史时序长度是预测长度1-7倍 input_length=N*output_length；
3. 
# 参考
[如何快速搭建自己的github.io博客](https://keysaim.github.io/post/blog/2017-08-15-how-to-setup-your-github-io-blog/)
