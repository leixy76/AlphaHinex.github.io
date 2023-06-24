---
id: a-survey-of-large-language-models
title: "《A Survey of Large Language Models》论文 v4 中文版摘抄"
description: "可作为了解当前大语言模型发展情况的材料进行阅读"
date: 2023.05.21 10:34
categories:
    - Book
tags: [Others]
keywords: LLM, ICL, CoT, Transformer, RLHF, 大语言模型, 涌现能力, 适配微调, 应用, 对齐, 能力评估
cover: /contents/covers/a-survey-of-large-language-models.png
---

# 摘要

> 有趣的是，当参数规模超过一定水平时，这些规模扩大的语言模型的性能不仅得到了显著提升，而且还表现出一些小规模语言模型(如 BERT)所不具备的特殊能力(如上下文学习)。

# 1 引言

> 语言建模是提高机器语言智能的主要方法之一

> 可以分为四个主要发展阶段
> 1. 统计语言模型（SLM）
> 1. 神经语言模型（NLM）
> 1. 预训练语言模型（PLM）
> 1. 大语言模型（LLM）

> 本综述从四个主要方面对 LLM 的最近进展进行文献综述，包括预训练(如何预训练出一个有能力的 LLM)、适应微调(如何从有效性和安全性两个角度有效地微调预训练的 LLM)、使用(如何利用 LLM 解决各种下游任务)以及能力评估(如何评估 LLM 的能力和现有的经验性发现)

# 2 概述

## 背景

## 大语言模型的涌现能力

> LLM 的“涌现能力”被正式定义为“在小模型中不存在但在大模型中出现的能力”，这是区分 LLM 与以前的 PLM 最突出的特征之一。

> 三个代表性的 LLM 涌现能力
> 1. 上下文学习
> 1. 指令遵循
> 1. 逐步推理

## LLM 关键技术

### 扩展

> 预训练数据的质量在实现良好性能方面起着关键作用，因此在扩展预训练语料库时，数据收集和清洗策略非常重要。

### 训练

### 能力引导

### 对齐微调

### 工具操作

# 3 大语言模型资源

## 3.1 公开可用的模型检查点或 API

### 百亿参数量级别的模型

> CodeGen(11B)是一个为生成代码设计的自回归语言模型，可用作探索代码生成能力的候选模型，其提出了一个新的基准测试 MTPB [76]，专门用于多轮程序合成，由 115 个专家生成的问题组成，为了解决这些问题，需要大语言模型获得足够的编程知识(例如数学、数组操作和算法)。

> 百亿参数量级别的模型通常需要数百甚至上千个 GPU 或 TPU。 例如，GPT-NeoX-20B 使用了 12 个微服务器，每个服务器配备了 8 个 NVIDIA A100-SXM4-40GB GPU，LLaMA 使用了 2048 个 A100-80G GPU。

### 千亿参数量级别的模型

### 大语言模型的公共 API

## 3.2 常用语料库

> - Books
> - CommonCrawl
> - Reddit Links
> - Wikipedia
> - Code
> - Others

## 3.3 算法库资源

> - Transformers
> - DeepSpeed
> - Megatron-LM
> - JAX
> - Colossal-AI
> - BMTrain
> - FastMoE

# 4 预训练

## 4.1 数据收集

### 4.1.1 数据来源

> 通用文本数据
> - 网页
> - 对话文本
> - 书籍

> 专用文本数据
> - 多语言文本
> - 科学文本
> - 代码

### 4.1.2 数据预处理

#### 质量过滤

> - 基于语言的过滤
> - 基于度量的过滤
> - 基于统计的过滤
> - 基于关键词的过滤

#### 去重

#### 隐私去除

#### 分词

### 4.1.3 预训练数据对大语言模型的影响

#### 混合来源

> 单独训练过多的某个领域的数据会影响大语言模型在其他领域的泛化能力

#### 预训练数据的数量

> 建议研究人员在扩展模型参数时，尤其要注意高质量数据的数量， 以充分训练模型。

#### 预训练数据的质量

## 4.2 架构

### 4.2.1 主流架构

> 由于 Transformer 架构的出色并行性和容量，Transformer 架构已成为开发各种大语言模型的事实标准骨干，使得将语言模型扩展到数百亿或数千亿个参数成为可能

> 一般来说， 现有大语言模型的主流架构可以大致分为三种类型

#### 编码器-解码器架构

> 目前，只有少数大语言模型是基于编码器-解码器架构构建的

#### 因果解码器架构

> GPT 系列模型 [26, 55, 119] 是基于因果解码器架构开发的。

> 因果解码器和前缀解码器都属于仅解码器体系结构

#### 前缀解码器架构

> 前缀解码器架构(也称非因果解码器架构) 修正了因果解码器的掩码机制，以使其能够对前缀标记执行双向注意力 [157]，并仅对生成的标记执行单向注意力。

### 4.2.2 详细配置

> - 标准化
> - 激活函数
> - 位置编码
> - 注意力机制和偏差

### 4.2.3 预训练任务

> - 语言模型
> - 去噪自编码

### 4.2.4 总结与讨论

## 4.3 模型训练

### 4.3.1 优化设置

> - 批量训练
> - 学习率
> - 优化器
> - 稳定训练

### 4.3.2 可扩展的训练技术

#### 3D 并行

> - 数据并行
> - 流水线并行
> - 张量并行

#### ZeRO

#### 混合精度训练

#### 整体训练建议

> 通常，量化技术被广泛用于在推理阶段减少大语言模型的时间和空间成本 [189]。虽然会损失一些模型性能，但量化语言模型具有更小的模型大小和更快的推理速度

> 对于模型量化，INT8 量化是一个流行的选择 [190]。此外，一些研究工作尝试开发更激进的 INT4 量化方法 [82]。

# 5 大语言模型的适配微调

## 5.1 指令微调

> 两种微调预训练后的大语言模型的方法
> 1. 指令微调 —— 旨在增强(或解锁)大语言模型的能力
> 1. 对齐微调 —— 旨在将大语言模型的行为与人类的价值观或偏好对齐

### 5.1.1 格式化实例构造

#### 格式化已有数据集

#### 格式化人类需求

#### 实例构建的关键因素

> - 扩展指令
> - 格式设计

### 5.1.2 指令微调策略

> - 平衡数据分布
> - 结合指令微调和预训练

### 5.1.3 指令微调的效果

#### 性能改进

> 最近的研究在多个规模(从 77M 到 540B 不等)上对语言模型进 行了实验，表明不同规模的模型都可以从指令微调中受益 [83, 201]，随着参数规模的增加，性能也得到了提升 [84]。

> 此外，经过指令微调的较小模型甚至可以比未经微调的较大模型表现更好 [28, 83]。

#### 任务泛化性

## 5.2 对齐微调

### 5.2.1 对齐微调的背景

#### 背景

#### 对齐标准

> - 有用性
> - 诚实性
> - 无害性

### 5.2.2 人类反馈收集

#### 标注人员选择

#### 人类反馈收集

> - 基于排序的方法
> - 基于问题的方法
> - 基于规则的方法

### 5.2.3 基于人类反馈的强化学习

#### RLHF 系统

#### RLHF 的关键步骤

> - 监督微调
> - 训练奖励模型
> - RL 微调

# 6 使用

## 6.1 上下文学习

> “上下文学习”（ICL）首次在 GPT-3 中被提出，并成为利用大语言模型的典型方法

### 6.1.1 上下文学习的一般形式

### 6.1.2 样例设计

#### 样例选择

> - 启发式的方法
> - 基于大语言模型的方法

#### 样例格式

#### 样例顺序

### 6.1.3 底层机制

#### 预训练如何影响 ICL？

> ICL 首次在 GPT-3 [55] 中提出，其表明 ICL 的能力随着模型尺寸的增大而增强。而有些研究表明，小规模的预训练语言模型也可以通过特别设计的训练任务来展示出强大的 ICL 能力(例如学习根据由任务实例和查询组成的输入来预测标签)，甚至可能超越规模更大的模型[234]。因此，训练任务的设计是影响大语言模型的 ICL 能力的一个 重要因素。

> 研究表明，ICL 的性能主要取决于预训练语料的来源而非规模

> 当训练数据可以被聚类成许多不常见的类别，而不是均匀分布，模型就会出现 ICL 的能力。

#### 大语言模型如何实现 ICL？

## 6.2 思维链提示

### 6.2.1 用 CoT 进行上下文学习

#### 少样本 CoT

> - CoT 设计提示
> - 增强的 CoT 策略

#### 零样本 CoT

### 6.2.2 关于 CoT 的讨论

#### CoT 何时适用于大语言模型？

> 由于 CoT 是一种涌现能 力 [47]，它只能有效增强有 100 亿或更多参数的足够大的模型[32]，而对小模型则无效。

> 此外，由于CoT通过中间推理步骤增强了标准提示，它的效果主要体现在需要逐步推理的任务 [32]，例如算术推理、常识推理和符号推理。然而，对于不依赖于复杂推理的其他任务，它可能会比标准提示表现更差

#### 大语言模型为什么能够进行 CoT 推理？

##### CoT 能力的来源

> 关于 CoT 能力的来源，研究者普遍将其归因于使用代码进行训练，因为在代码数据训练过的模型表现出强大的推理能力

> 指令调整似乎不是获得 CoT 能力的关键原因

##### 各个组件的作用

# 7 能力评测

## 7.1 基础评测任务

### 7.1.1 语言生成

#### 语言建模

> 作为大语言模型最基本的能力，语言建模旨在基于前面的词元预测下一个词元 [15]，主要关注基本的语言理解和生成能力。

> 语言建模任务的性能通常遵循扩展定律 [30]，这意味着提升语言模型的参数量将提高准确性并降低困惑度。

#### 条件文本生成

> 作为语言生成中的一个重要话题，条件文本生成 [48] 旨在基于给定的条件生成满足特定任务需求的文本，通常包括机器翻译 [337]、文本摘要 [338] 和问答系统 [339] 等。

#### 代码合成

> 除了生成高质量的自然语言外，现有的大语言模型还表现出强大的生成形式化语言的能力，尤其是满足特定条件的计算机程序(即代码)，这种能力被称为代码合成

#### 主要问题

##### 可控生成

> 现有工作 [40] 表明，当生成文本的时候施加复杂的结构约束，大语言模型可以很好地处理局部关系(例如，相邻句子之间的交互)，但可能难以应对全局关系(即长距离相关性)。例如，要生成一个由多个段落组成的复杂长篇文章，仍然很难直接在全局上确保特定的文本结构(例如概念的顺序和逻辑流程)。对于需要遵循结构化规则或语法的生成任务，例如代码合成，会更加具有挑战性。

> 为了解决这个问题，一种潜在的解决方案是将一次性生成(即直接生成目标输出)扩展到大语言模型的迭代提示。

##### 专业化生成

> 直观上，领域知识对于模型的专业化至关重要。然而，将这种专业知识注入到大语言模型中并不容易。

> 正如最近的分析所讨论的 [46, 349]，当大语言模型被训练以展现某些特定的能力，使它们在某些领域表现出色时，它们可能会在其他领域遇到困难。这样的问题与神经网络训练中的灾难性遗忘 [350, 351] 有关，它指的是整合新旧知识时产生的冲突现象。

> 因此，开发有效的模型专业化方法至关重要，这些方法可以灵活地使大语言模型适应各种任务场景，并尽可能保留其原有的能力。

### 7.1.2 知识利用

#### 闭卷问答

#### 开卷问答

> 为了从外部资源中选择相关知识，大语言模型通常与一个文本检索器(甚至是一个搜索引擎)配对，该文本检索器与大语言模型独立或联合进行训练

#### 知识补全

#### 主要问题

##### 幻觉

> 幻觉在现有的大语言模型中广泛存在，甚至包括最优秀的大语言模型，如 GPT-4 [45]

##### 知识实时性

> 微调大语言模型是非常昂贵的，而且在增量训练大语言模型时很可能会导致灾难性遗忘问题。

> 直接修改内在知识或将特定知识注入大语言模型是很困难的

### 7.1.3 复杂推理

#### 知识推理

#### 符号推理

#### 数学推理

#### 主要问题

> - 不一致性
> - 数值计算

## 7.2 高级能力评估

### 7.2.1 人类对齐

### 7.2.2 与外部环境的互动

### 7.2.3 工具操作

## 7.3 公开基准和经验性分析

### 7.3.1 评测基准

> - MMLU
> - BIG-bench
> - HELM

### 7.3.2 大语言模型能力的综合分析

#### 通才

> - 熟练度
> - 稳定度

#### 专才

> - 医疗
> - 教育
> - 法律

# 8 总结与未来方向

## 理论与原理

> 已有工作显示，当语言模型的参数增加到某个临界规模(例如 100 亿)时，会以一种意想不到的方式(突然性能飞跃)涌现出一些能力 [32, 47]，通常包括上下文学习、指令跟随和逐步推理。

## 模型架构

## 模型训练

## 模型应用

> 由于在实际应用中微调的成本非常高，提示已成为使用大型语言模型的主要方法。通过将任务描述和示例合并到提示中，上下文学习(一种特殊形式的提示)赋予了 LLM 在新任务上表现良好的能力，甚至在某些情况下胜过全数据微调模型。

## 安全与对齐

## 应用与生态