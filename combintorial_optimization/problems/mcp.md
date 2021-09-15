---
sort: 4
---
# 最大割问题(Maximum Cut)

## 问题描述
对于一个图，最大切割是一个切割的大小至少是任何其他切割的大小。也就是说，它是将图的顶点划分为两个互补顶点集$$S$$和$$T$$，使$$S$$和$$T$$之间的边数尽可能大。在图中寻找最大割的问题称为最大割问题。   

## 精确算法


## 近似算法
### 随机算法
对于图中的每个节点，以概率p将其随机分配到两个互补顶点集中。  
```
def randomized_partitioning(G, p=0.5):
    # 以概率p随机选择节点加入cut集
    cut = {node for node in G.nodes() if random() < p}
    cut_weight = cut_weight(G, cut)
    partition = (cut, G.nodes - cut)
    return cut_weight, partition
```
执行此算法预期中会有一般的边被切割，故是一个**0.5-近似算法**。

### 贪心算法
首先将图中的节点分成两个互补顶点集，每次贪心地选择最佳的节点，使其从原点集交换到另一个点集后所得的割边权重和最大，知道割边权重和无法增大结束程序。   
```
def one_exchange(G, cut=set()):
    cut_weight = cut_weight(G, cut)
    while True:
        nodes = list(G.nodes())
        # 贪心地选择最佳的节点以保证获得的割边权重和最大
        best_node_to_swap = max(
            nodes,
            key=lambda v: cut_weight(G, _swap_node_partition(cut, v)),
        )
        potential_cut = _swap_node_partition(cut, best_node_to_swap)
        potential_cut_weight = cut_weight(G, potential_cut)

        if potential_cut_weight > cut_weight:
            cut = potential_cut
            cut_weight = potential_cut_weight
        else:
            break

    partition = (cut, G.nodes - cut)
    return cut_weight, partition
```
当算法终止时，每个顶点引出的边至少有一般被切割，否则移动节点就会获得更优解，因此，该切割至少包括$$|E|/2$$条边，也是个**0.5-近似算法**。

### 半正定规划
