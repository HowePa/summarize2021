# 集合覆盖问题（ Set Covering Problem ）

## 问题描述 
选择最少的集合，覆盖全部的元素。   
一个集合系统$(X,F)$由一个有穷集$X$和一个$X$的子集族$F$构成，当$X$中的每一个元素至少属于$F$中的一个子集时：  
\\[ X=\bigcup_{S\in F}S \\]   
我们说一个子集$S\in F$覆盖了集合$X$的元素。   
集合覆盖问题是要找到一个最小规模的子集族$R\subseteq F$，使其成员覆盖$X$的所有成员：  
\\[ X=\bigcup_{S\in R}S \\]

## 精确算法

## 近似算法
贪心近似算法：每次循环都选择出能覆盖最多尚未被覆盖元素的集合。    
> Input: a set system $(X,S)$  
> Output: a set cover $R$   
> $U = X, R = \emptyset$     
> while $U \neq \emptyset$    
> &emsp; select an $S\in F$ that maximizes $|S\cap U|$  
> &emsp; $U = U - S$   
> &emsp; $R = R \cup S$    
> return R