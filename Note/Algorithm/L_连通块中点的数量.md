## 题目

[**连通块中点的数量**](https://www.acwing.com/problem/content/839/)

## 解析

**Category:** Disjoint Set

这是一道常规的并查集的运用

## 代码

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 10;
int id[N];
int s[N];
int n, m;

void init() {
    for(int i = 1; i <= n; i ++ ) id[i] = i, s[i] = 1;
}

int root(int x) {
    while(x != id[x]) id[x] = id[id[x]], x = id[x];
}

void unition(int p, int q) {
    int rp = root(p), rq = root(q);
    if(rp == rq) return;
    if(s[rp] < s[rq]) {
        id[rp] = rq;
        s[rq] += s[rp];
    } else {
        id[rq] = rp;
        s[rp] += s[rq];
    }
}

bool find(int a, int b) {
    return root(a) == root(b);
}


int main() {
    scanf("%d%d", &n, &m);
    init();
    string a;
    int b, c;
    while(m -- ) {
        cin >> a;
        if(a == "C") {
            cin >> b >> c;
            if(b != c) unition(b, c);
        } else if(a == "Q1"){
            cin >> b >> c;
            if(find(b, c)) printf("Yes\n");
            else printf("No\n");
        } else {
            cin >> b;
            printf("%d\n", s[root(b)]);
        }
    }
    return 0;
}
```

