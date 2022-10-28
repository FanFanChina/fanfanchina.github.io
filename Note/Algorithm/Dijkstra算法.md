## 概述

Dijkstra算法 —— 单 / 多源基于贪心的最短路径算法

## 朴素版Dijkstra算法

**适用范围:** 单源, 边的权值为正数

**步骤如下:**

- 初始化距离起点的距离

- 迭代n次(因为n个点，找n次)

    - 找到不在确定距离的集合中的距离起点最近的点t
    - 将t加入确定距离的集合中去
    - 用t来更新其他未确定的点的距离

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 510;
int n, m;
int d[N];
bool st[N];
int g[N][N]; 

void dijkstra(int start) {
    // 初始化距离
    memset(d, 0x3f, sizeof d);
    d[start] = 0;
    // for循环迭代
    for(int i = 1; i <= n; i ++ ) {
        // 找到不在确定集合中的距离起点最近的点
        int t = -1;
        for(int j = 1; j <= n; j ++ )
            if(!st[j] && (t == -1 || d[j] < d[t])) t = j;
        // 加入确定的集合之中
        st[t] = true;
        // 更新与之相连的未确定的点距离起点的距离
        for(int j = 1; j <= n; j ++ )
            d[j] = min(d[j], d[t] + g[t][j]);
    }
}

int main() {  
    scanf("%d%d", &n, &m);
    memset(g, 0x3f, sizeof g);
    int a, b, c;
    while(m -- ) {
        scanf("%d%d%d", &a, &b, &c);
        g[a][b] = min(g[a][b], c);
    }
    dijkstra(1);
    if(d[n] != 0x3f3f3f3f) printf("%d", d[n]);
    else printf("-1");
    return 0;
}
```

**ADD:** 对于重边取最下值即可，对于自环，因为算法只找未确定的点的特点，所以即使读入也毫无影响

## 堆优化版Dijkstra算法

**Pre-Knowledge:** 链式前向星

如果n过大(稀疏图)，两重循环就会爆掉，所以我们需要对算法进行优化

观察算法过程，我们可以发现每次找到未确定的距离最近的点时，都要循环n次

算上外层的for循环迭代，至少是n方级别的时间复杂度

我们用小顶堆加速这个过程，可以使用STL库中的priority_queue

```cpp
#include <bits/stdc++.h>

using namespace std;
typedef pair<int, int> PII; // 距离起点的最短距离|节点编号
const int N = 2e5;

int n, m;
int dist[N];
bool st[N];

// 链式前向星
int h[N], w[N], e[N], ne[N], idx;
void add(int a, int b, int c) {
    e[idx] = b, w[idx] = c, ne[idx] = h[a], h[a] = idx ++ ; 
}

// dijkstra
void dijkstra(int start) {
    // 初始化距离
    memset(dist, 0x3f, sizeof dist);
    dist[start] = 0;
    priority_queue <PII, vector <PII>, greater<PII> > heap;
    heap.push({0, start}); // 初始化头节点的距离
    // while迭代
    while(heap.size()) {
        // 找到头节点(不在已经确定的集合中的最近的点)
        auto t = heap.top(); heap.pop();
        int ver = t.second, distance = t.first;
        if(st[ver]) continue;
        // 将头节点加入确定集合
        st[ver] = true;
        // 更新与之相连的的点
        for(int i = h[ver]; ~i; i = ne[i]) {
            int j = e[i];
            if(dist[j] >  distance + w[i]) {
                dist[j] = distance + w[i];
                heap.push({dist[j], j}); // 记录距离，便于下一次筛选
            }
        }
    }
}

int main() {  
    // 链式前向星初始化头节点
    memset(h, -1, sizeof h);
    // 读入
    scanf("%d%d", &n, &m);
    int a, b, c;
    while(m -- ) {
        scanf("%d%d%d", &a, &b, &c);
        add(a, b, c);
    }
    // djkstra
    dijkstra(1);
    // 输出
    if(dist[n] == 0x3f3f3f3f) printf("-1");
    else printf("%d", dist[n]);
    return 0;
}
```

## Mistake History

- t = -1









