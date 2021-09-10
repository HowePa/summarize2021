---
sort: 1
---
# 最小顶点覆盖(Minimum Vertex Cover)

## 问题描述
在图中选择最小的点集\\(S\\)来覆盖所有的边，即每条边都至少有一个端点在集合\\(S\\)中。  

## 近似算法
### 贪心算法
贪心策略每次都选择任意边，将其两个顶点并入覆盖集中，然后在边集中删除该边和与该边有公共顶点的边。  
> 1. \\( C=\emptyset \\)    
> 2. while \\( E\neq\emptyset \\)   
> 3. &emsp; pick any \\(\lbrace u,v\rbrace \in E \\)     
> 4. &emsp; \\(C = C \cup \lbrace u,v\rbrace\\)   
> 5. &emsp; delete all edges incident to either \\(u\\) or \\(v\\)      
> 6. return \\(C\\)   

这是一个**2-近似算法**。设$$A$$是算法中第3行选出的边集合。为了覆盖$$A$$中的边，任意一个顶点覆盖都必须至少包含$$A$$中每条边的一个端点。如果一条边在第3行被选中，那么第5行就会从$$E$$中删除所有与其端点关联的边。因此，$$A$$中不存在两条边具有共同的端点，从而$$A$$中不会存在两条边由最优解$$ C^\prime $$中的同一顶点所覆盖。故最有顶点覆盖的规模下界是：
\\[ \lvert C^\prime\rvert\geqslant\lvert A\rvert, \\]
算法第3行每次执行都会挑选出一条边，其两个端点都不在C中，因此，所返回顶点覆盖的规模上界为：
\\[ \lvert C\rvert=2\lvert A\rvert, \\]
则有
\\[ \lvert C\rvert=2\lvert A\rvert\leqslant 2\lvert C^\prime\rvert. \\]