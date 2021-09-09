# NP-hard

- **P类问题**（polynominal）：存在多项式时间算法的问题。    
- **NP类问题**（Nondeterministic polynominal）：能在多项式时间内验证得出一个正确解的问题。P类问题是NP类问题的子集。  
- **NPC问题**（NP完全，Nondeterminism Polynomial complete）：存在这样一个NP问题，所有的NP问题都可以归约成它。换句话说，只要解决了这个问题，那么所有的NP问题都解决了。其定义要满足2个条件：首先，它得是一个NP问题；其次，所有的NP问题都可以归约成它。  
- **NP难问题**（NP-hard）：NP-Hard问题是这样一种问题，它满足NPC问题定义的第二条但不一定要满足第一条，即所有的NP问题都能约化到它，但是它不一定是一个NP问题。