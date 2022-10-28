## 题目

[**区间合并**](https://www.acwing.com/problem/content/805/)

## 解析

**Categories:** 区间合并, Greedy

**步骤:**

- 全部区间按左端点进行排序
- 从前往后逐个扫描区间，能合并就合并

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 10;
struct Range {
    int l, r;
    bool operator < (const Range W) const {
        return l < W.l;
    }
}range[N];
int n;

int main() {
    scanf("%d", &n);
    for(int i = 1; i <= n; i ++ ) scanf("%d%d", &range[i].l, &range[i].r);
    sort(range + 1, range + 1 + n);
    int res = n, start = range[1].l, end = range[1].r;
    for(int i = 2; i <= n; i ++ ) {
        if(end >= range[i].r) res --;
        if(end >= range[i].l && end < range[i].r) res --, end = range[i].r;
        if(end < range[i].l) start = range[i].l, end = range[i].r;
    }
    printf("%d", res);
    return 0;
}
```

