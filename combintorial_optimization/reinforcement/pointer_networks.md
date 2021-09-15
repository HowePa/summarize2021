---
sort: 1
---
# [Pointer Networks](https://arxiv.org/pdf/1506.03134.pdf)

## Abstract
本文提出一个神经网络结构，用来学习与输入序列的位置相关的输出序列的条件概率。  
- 问题难点：输出序列的规模不固定。(可扩展性)  
- 应用问题：排序(sort)、组合优化(CO)  

## Introduction
**RNN**受限于输入与输出的长度是固定的。**Seq2Seq**使用(RNN-->嵌入-->RNN-->输出)的结构消除了这些约束。但是使用Seq2Seq仍然需要先确定输出序列的大小，无法应用到组合问题中（组合问题的输出规模随着输入规模的变化而变化）。本文的贡献如下：
1. 提出了一个全新的简单且高效结构Pointer Net，通过使用softmax概率分布作为“指针“来解决序列长度可变的问题。
2. 将模型推广到三种不同的问题当中。
3. 模型可以计算得到如TSP问题这样的难以处理的问题的近似解决方案。

## Models
### Sequence-to-Sequence
Sequence-to-Sequence(Seq2Seq)模型实现了把一个序列转换成另一个序列的功能，并且**不要求输入序列和输出序列等长**。


```note
@inproceedings{Vinyals2015PointerN,  
  title={Pointer Networks},  
  author={Oriol Vinyals and Meire Fortunato and Navdeep Jaitly},  
  booktitle={NIPS},  
  year={2015}  
}  
```