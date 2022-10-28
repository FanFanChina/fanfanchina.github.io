## 题目

**[Prim算法求最小生成树](https://www.acwing.com/problem/content/description/860/)**

## 解析

**Category:** MST, Prim

**步骤:**

- 初始化每个点到连通块集合距离为正无穷
- n次迭代
    - 找到不在联通块内的距离集合最近的点 T
    - 将 T 纳入连通块集合内
    - -- 如果不是第一个点且当前点距离集合的距离为INF, 不存在最小生成树 --
    - -- 如果不是第一个点记录求和距离 --
    - 用 t 更新其他点到**集合**的距离

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 510, INF = 0x3f3f3f3f;
int g[N][N], n, m;
int dist[N];
bool st[N];

int prim() {
    int sum = 0;
    memset(dist, 0x3f, sizeof dist);
    for(int i = 1; i <= n; i ++ ) {
        int t = -1;
        for(int j = 1; j <= n; j ++ )
            if(!st[j] && (t == -1 || dist[t] > dist[j])) t = j;
        st[t] = true;
        if(i != 1 && dist[t] == INF) return INF;
        if(i != 1) sum += dist[t];
        for(int j = 1; j <= n; j ++ ) dist[j] = min(dist[j], g[t][j]);
    }
    return sum;
}

int main() {
    scanf("%d%d", &n, &m);
    memset(g, 0x3f, sizeof g);
    int a, b, c;
    while (m -- ) {
        scanf("%d%d%d", &a, &b, &c);
        g[a][b] = g[b][a] = min(g[a][b], c); 
    }
    int t = prim();
    if(t == INF) printf("impossible");
    else printf("%d", t);
    return 0;
}
```

## 错误历史

```cpp
if(i != 1) sum += dist[i];
```

