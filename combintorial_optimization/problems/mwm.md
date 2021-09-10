---
sort: 8
---
# 图匹配问题(Graph Matching)

## 问题描述
找出一个边集$$K$$，满足$$K$$中的所有边都没有公共顶点。  


## 精确算法
> In graph theory parlance, maximal matching and maximum matching are different (even in a bipartite graph).  
> **Maximal matching** simply means you cannot add any more edges to it as pointed out by donkopotamus.   
> **Maximum matching** means no matching has more edges than it.    
> 最大权匹配分为：**所有匹配中权值最大的匹配** 和 **最大基数匹配中权值最大的匹配**

### Hungary algorithm

    // 求二分图的 maximum match

    bool find(int u) {
        // 对于右点集中的每个节点 v
        for (v=1; v<=M; v++) {
            // 如果存在边 (u,v)，且节点 v这轮未被访问
            if (line[u][v] == true && vis[v] == false)      
            {
                vis[v] = 1;
                // 如果节点 v未匹配，或者存在增广路
                if (match[v] == 0 || find(match[v])) { 
                    // 递归探索增广路并修改匹配
                    match[v] = u;
                    return true;
                }
            }
        }
        return false;
    }

    int hungary() {
        int mm = 0;
        // 对于左点集中的每个节点 u
        for (u=1; u<=N; u++) {
            // 每轮都将右点集访问状态初始化为 0
            memset(vis, 0, sizeof(vis));
            if(find(u))
                mm += 1;
        }
        return mm;
    }
    
> **完备匹配：** 如果一个二分图，X部中的每一个顶点都与Y部中的一个顶点匹配，**或者**Y部中的每一个顶点也与X部中的一个顶点匹配，则称该匹配为完备匹配。  
> **最佳匹配：** 带权二分图的权值最大的完备匹配称为最佳匹配。   
> *通过添加权值为 0的边，使得最佳匹配和最大权匹配问题统一。*

### Kuhn-Munkres algorithm

    // 求二分图的最佳匹配

    bool dfs(int u) {
        vis_u[u] = true;
        for (int v=1; v<=M; v++) 
            if (!vis_v[v]) {
                int gap = ex_u[u] + ex_v[v] - weights[u][v];
                if (gap == 0) {
                    vis_v[v] = true;
                    if (matchright[v] == 0 || dfs(matchright[v])) {
                        matchleft[u] = v, matchright[v] = u;
                        return true;
                    }
                }
                else if (gap > 0) {
                    //找出边权与顶标和的最小的差值
                    if (gap < minz)
                        minz = gap;
                }
            }
        return false;
    }

    void km() {
        memset(matchleft, 0, sizeof matchleft);
        memset(matchright, 0, sizeof matchright);
        // 对于左点集中的每个节点 u
        for (int u=1; u<=N; u++) {
            while (true) {
                minz = INF;
                memset(vis_u, false, sizeof vis_u);
                memset(vis_v, false, sizeof vis_v);
                // 遍历寻找匹配
                if (dfs(u))
                    break;
                // 匹配失败
                // 更新所有节点的期望，左节点降低期望 minz，右节点增加期望 minz
                for (int i=1; i<=N; i++)
                    if (vis_u[i])
                        ex_u[i] -= minz;
                for (int i=1; j<=M; i++)
                    if (vis_v[i])
                        ex_v[i] += minz;
            }
        }
    }

### Blossom algorithm

    // 求一般图最大权匹配

## 近似算法