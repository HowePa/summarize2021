# 近似算法（Approximation Algorithms)   

解决NP-hard问题有三种方法：   
1. 如果实际输入数据规模较小，则用指数级运算时间的算法就能很好地解决问题；
2. 对于一些能在多项式时间内解决的特殊情况，可以把它们单独列出来求解；
3. 可以寻找一些能够在多项式时间内得到近似最优解的方法。   

在实际应用中，近似最优解一般都能满足要求，这种返回近似最优解的算法称为**近似算法**。   

根据所要解决的问题，最优解可以定义为具有最大可能代价的解（最大化问题）或具有最小可能代价的解（最小化问题）。对于规模为$n$的输入，近似算法产生的近似解的代价$C$与最优解的代价$C^\*$相差一个因子$\rho(n)$，$\max(\frac{C}{C^\*},\frac{C^\*}{C})\leqslant\rho(n)$，我们将这个因子称为**近似比**。如果一个算法的近似比达到$\rho(n)$，则称该算法为$\rho(n)$近似算法。例如，一个1近似算法产生的解就是最优解，而一个近似比较大的近似算法可能会返回和最优解差很多的解。   
一些NP完全问题可以采用特定的多项式时间近似算法求解，这些算法通过消耗更多的计算时间，可以得到不断缩小的近似比。一个最优化问题的**近似模式**就是这样一种算法，它的输入除了该问题的实例外，还有一个值$\varepsilon>0$，使得对任何固定的$\varepsilon$，该模式都是一个$(1+\varepsilon)$近似算法。对一个近似模式来说，如果对任何固定的$\varepsilon>0$，该模式都以其输入实例规模$n$的多项式时间运行，则称此模式为**多项式时间近似模式**。随着$\varepsilon$的减小，多项式时间近似模式的运行时间可能会迅速增长。对一个近似模式来说，如果其运行时间表达式既为$1/\varepsilon$的多项式，又为输入实力规模$n$的多项式，则称其为**完全多项式时间近似模拟**。