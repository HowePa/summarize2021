---
sort: 1
---
# 最小顶点覆盖(Minimum Vertex Cover)

## 问题描述
在图中选择最小的点集\\(S\\)来覆盖所有的边，即每条边都至少有一个端点在集合\\(S\\)中。  

## 近似算法
### 贪心算法
贪心策略每次都选择任意边，将其两个顶点并入覆盖集中，然后在边集中删除该边和与该边有公共顶点的边。  

```
def min_weighted_vertex_cover(G):
    cost = dict(G.nodes())
    # 当存在未覆盖的边时，选择一个未覆盖的边并更新其余边的状态。
    for u, v in G.edges():
        # 对于最小权顶点覆盖问题，贪心地选取两个顶点间权重最小的边。
        min_cost = min(cost[u], cost[v])
        # 在点集中删除被选边的两个顶点。
        cost[u] -= min_cost
        cost[v] -= min_cost
    return {u for u, c in cost.items() if c == 0}
```
这是一个**2-近似算法**。设$$A$$是算法中每层循环选出的边集合。为了覆盖$$A$$中的边，任意一个顶点覆盖都必须至少包含$$A$$中每条边的一个端点。如果一条边被选中，那么算法就会从$$E$$中删除所有与其端点关联的边。因此，$$A$$中不存在两条边具有共同的端点，从而$$A$$中不会存在两条边由最优解$$ C^\prime $$中的同一顶点所覆盖。故最有顶点覆盖的规模下界是：
\\[ \lvert C^\prime\rvert\geqslant\lvert A\rvert, \\]
算法每层循环都会挑选出一条边，其两个端点都不在C中，因此，所返回顶点覆盖的规模上界为：
\\[ \lvert C\rvert=2\lvert A\rvert, \\]
则有
\\[ \lvert C\rvert=2\lvert A\rvert\leqslant 2\lvert C^\prime\rvert. \\]