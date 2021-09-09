# 经典问题

## 组合优化问题
- [**布尔可满足性问题(Boolean Satisfiability, SAT)**](sat)：确定是否存在满足给定布尔公式的解释的问题。将给定布尔公式的变量一致地用值TRUE或FALSE替换。若存在一种替换方式使得公式的计算结果为TRUE，则称公式为可满足的，相反则称公式为不可满足的。   
- [**装箱问题(Bin Packing, BP)**](bpp)：以最小数量的箱子数将若干不同尺寸的物体全部装入箱中。  
- [**背包问题(Knapsack Problem, KP)**](kp)：给定一组物品，每种物品都有自己的重量和价格，在限定的总重量内，如何选择才能使得物品的总价格最高。   
- [**作业调度问题(Job Scheduling Problem, JSP)**](jsp)：n 个工件在 m 台机器上加工，每个工件有特定的加工工艺，每个工件加工的顺序及每道工序所花时间给定，安排工件在每台机器上工件的加工顺序，使得某种指标最优。  
- [**整数规划问题(Integer Programming, IP)**](ip)：一类要求问题的解中的全部或一部分变量为整数的数学规划。从约束条件的构成又可细分为线性、二次和非线性的整数规划。  
- [**最大公共子图问题(Maximum Common Subgraph, MCS)**](mcs)：给定两个无向图 G 和 F ，求一个最大的 G 的顶点子集 S ，使得 S 导出的子图`$G_S$`同构于 F 的某个子图`$F_S$`。

## 图优化问题
- [**旅行商问题(Traveling Salesman Problem, TSP)**](tsp)：一个商品推销员要去若干个城市推销商品，他从一个城市出发，需要经过所有城市后，回到出发地。应该如何选择行进路线，以使总的行程最短。  
- [**车辆路径问题(Vehicle Routing Problem, VRP)**](vrp)：一定数量的客户，各自有不同数量的货物需求，配送中心向客户提供货物，由一个车队负责分送货物，组织适当的行车路线，目标是使得客户的需求得到满足，并能在一定的约束下，达到诸如路程最短、成本最小、耗费时间最少等目的。   
- [**最大割问题(Maximum Cut, MaxCut)**](mcp)：将图的顶点划分为两个互补顶点集 S 和 T ，使 S 和 T 之间的边数尽可能大。   
- [**最小顶点覆盖问题(Minimum Vertex Cover, MVC)**](mvc)：在图中选择最小的点集 S 来覆盖所有的边，即每条边都至少有一个端点在集合 S 中。   
- [**最大团问题(Maximum Clique, MC)**](mc)：在一个无向图中找出一个点数最多的完全图。每对不同的顶点之间都恰连有一条边相连的图称为完全图。   
- [**最大独立集问题(Maximum Independent Set, MIS)**](mis)：独立集是指图 G 中两两互不相邻的顶点构成的集合。最大独立集是具有最大尺寸的独立集。   
- [**最小支配集问题(Minimum Dominating Set, MDS)**](mds)：在给定的图中找到一组顶点D，D中的顶点互不相邻（独立），且D之外的每个顶点都有相邻的顶点包含于D（支配）。   
- [**图着色问题(Graph Coloring, GC)**](gc)：将所有顶点分为 K 个颜色组，每个组形成一个 独立集，即其中没有相邻的顶点，求最小的 K 值。  
- [**图匹配问题(Graph Matching, GM)**](mwm)：找出一个边集 K ，满足 K 中的所有边都没有公共顶点。  