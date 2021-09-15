---
sort: 2
---
# 旅行商问题(Travelling Salesman Problem)

## 问题描述
- 基本描述：一个商品推销员要去若干个城市推销商品，他从一个城市出发，需要经过所有城市后，回到出发地。应该如何选择行进路线，以使总的行程最短。   
- 图论描述：在一个**带权完全无向图**中，找一个权值最小的哈密顿回路。   
- 哈密顿回路：在一个无向图中，如果存在一条从给定起点到给定终点沿途恰好经过所有其他顶点一次的路径，则称该路径为哈密顿路径。闭合的哈密段路径（起点和终点是一个顶点）称作哈密顿回路。   

## 精确算法
### 暴力搜索
暴力搜索的解决方案就是尝试所有排列（有序组合），看看哪一条路径的权值最小。这种方法的时间复杂度是$$O(n!)$$，即城市数量的阶乘，因此这个解决方案即使对于只有20个城市的问题实例也不切实际。    
### Held-Karp算法
Held-Karp算法是一种基于动态规划的算法，算法每一步都计算所有点是最后一个点的可能性，且每一步都以来前一步的结果。  
> 将城市按照\\(1,2,...,n\\)标记，其中$$1$$表示起始城市。对于城市集合\\(S \subseteq \lbrace 2,...n \rbrace\\)的所有子集，计算从城市\\(1\\)到城市\\(e \neq 1 \wedge e \notin S\\)经过\\(S\\)中所有城市的路径的最短路径，路径长度计为\\(g(S,e)\\)，\\(d(u,v)\\)表示从$$u$$到$$v$$的直接距离，计算从最小的子集开始扩展到最大的子集。   
例如：\\(g(\emptyset,e)=d(1,e)\\), \\(g(\lbrace 2\rbrace,3)=len(1\rightarrow 2\rightarrow 3)\\), \\(g(\lbrace 2,3\rbrace,4)=min(len(1\rightarrow 2\rightarrow 3\rightarrow 4),len(1\rightarrow 3\rightarrow 2\rightarrow 4))\\)  
对于$$k$$个可能的最短路径存在：\\[ g(S,e)=\min_{1\leqslant i \leqslant k}g(S_i, s_i)+ d(s_i, e). \\]  

该算法的时间复杂度为\\( O(n^22^n) \\)，空间复杂度为\\( O(2^nn) \\)。

    def held_karp(dists):
        """
        Implementation of Held-Karp, an algorithm that solves the Traveling
        Salesman Problem using dynamic programming with memoization.
        Parameters:
            dists: distance matrix
        Returns:
            A tuple, (cost, path).
        """
        n = len(dists)
        C = {}

        for k in range(1, n):
            C[(1 << k, k)] = (dists[0][k], 0)
            
        for subset_size in range(2, n):
            for subset in itertools.combinations(range(1, n), subset_size):
                bits = 0
                for bit in subset:
                    bits |= 1 << bit

                for k in subset:
                    prev = bits & ~(1 << k)

                    res = []
                    for m in subset:
                        if m == 0 or m == k:
                            continue
                        res.append((C[(prev, m)][0] + dists[m][k], m))
                    C[(bits, k)] = min(res)

        bits = (2**n - 1) - 1

        res = []
        for k in range(1, n):
            res.append((C[(bits, k)][0] + dists[k][0], k))
        opt, parent = min(res)

        path = []
        for i in range(n - 1):
            path.append(parent)
            new_bits = bits & ~(1 << parent)
            _, parent = C[(bits, parent)]
            bits = new_bits

        path.append(0)

        return opt, list(reversed(path))

## 近似算法   

### 满足三角不等式的旅行商问题
在很多实际问题中，从一个地方\\(u\\)直接到另一个地方\\(w\\)花费的代价总是最小的。如果一条路径经过了某个中转站，则它不可能具有比直接到达更小的代价，即：
\\[ c(u,w) \leqslant c(u,v)+c(v,w). \\]
根据这一特性，我们可以先计算出图的最小生成树，其权值是最优旅行商路线的下界，然后根据最小生成树来生成一条遍历路线。  
> 1. compute a weighted minimum spanning tree \\(T\\) of \\(G\\)      
> 2. let \\(H\\) be a list of vertices, ordered according to when they are first visited in a preorder tree walk of \\(T\\)   
> 3. return the hamiltonian cycle \\(H\\)    

在给定带权完全无向图上，使用PRIM算法计算图的最小生成树T。从根节点开始对T进行遍历，在对T进行先序遍历时，只在第一次遇见一个顶点时，才将该顶点列出。  
这是一个**2-近似算法**。设\\(H^\prime\\)表示在给定顶点集合上的一个最优旅行路线。我们通过删除一个旅行路线中的任一条边而得到生成树，并且每条边的代价都是非负的。因此，算法第1行得到的最小生成树T的权值是最优旅行路线代价的一个下界：
\\[ c(T) \leqslant c(H^\prime), \\]
对T进行完全遍历时，在初次访问一个顶点时输出该顶点，并且在访问一棵子树返回后输出该顶点。我们称这个遍历为W。因为该完全遍历恰好经过了\\(T\\)的每条边两次，所以有：
\\[ c(W) = 2c(T), \\]
则W的代价在最优旅行路线代价的2倍之内：
\\[ c(W) \leqslant 2c(H^\prime). \\]  

### 最近邻算法
最近邻算法是一种基于贪心过程的简单启发式算法。算法通过选择随机城市开始旅行，并将最近的未访问城市添加到旅行中的最后一个城市，直到访问了所有城市结束。算法步骤如下：
> 1. 随机选择一个城市\\(n_0\\)作为起始城市。   
> 2. 选择最近的未访问的城市。   
> 3. 把当前城市标记为已访问。   
> 4. 如果还存在未访问的城市，执行第2步。   
> 5. 如果所有城市都已经访问过，终止程序。   

### Christofides算法

