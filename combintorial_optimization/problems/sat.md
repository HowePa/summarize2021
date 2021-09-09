---
sort: 5
---
# 布尔可满足性问题（ Boolean Satisfiability ）

## 问题描述
可满足性问题是确定是否存在满足给定布尔公式的解释的问题。换句话说，将给定布尔公式的变量一致地用值TRUE或FALSE替换。若存在一种替换方式使得公式的计算结果为TRUE，则称公式为可满足的，相反则称公式为不可满足的。   
> 对于公式”a AND NOT b“，当a=TRUE且b=FALSE时，公式的计算结果是TRUE，故公式是可满足的。    
> 对于公式”a AND NOT a“，无论a=TRUE还是a=FALSE，公式的计算结果都是FALSE，故公式是不可满足的。   

