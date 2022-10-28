## 题目

[**合并集合**](https://www.acwing.com/problem/content/838/)

## 解析

**Category:** Disjoint Set

这是一道常规的并查集模板题目，优化到带权值及以上就可以过掉

## 代码

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 10;
int id[N], s[N], n, m;

void init() {
    for(int i = 1; i <= n; i ++ ) id[i] = i, s[i] = 1;
}

int root(int x) {
    while(x != id[x]) id[x] = id[id[x]], x = id[x];
    return x;
}

void unition(int p, int q) {
    int rp = root(p);
    int rq = root(q);
    if(rp == rq) return;
    if(s[rp] < s[rq]) {
        id[rp] = rq;
        s[rq] += s[rp]; 
    } else {
        id[rq] = rp;
        s[rp] += s[rq];
    }
    
}

bool find(int p, int q) {
    return root(p) == root(q);
}

int main() {
    scanf("%d%d", &n, &m);
    init();
    char a;
    int b, c;
    while (m -- ) {
        cin >> a >> b >> c;
        if(a == 'M') {
            if(!find(b, c)) unition(b, c);
        } else {
            if(find(b, c)) printf("Yes\n");
            else printf("No\n");
        }
    }
    return 0;
}
```

## Mistake History

- 忘记使用init函数
