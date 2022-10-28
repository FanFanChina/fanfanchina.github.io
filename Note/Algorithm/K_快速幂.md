## 题目

**[快速幂](https://www.acwing.com/problem/content/877/)**

## 解析

**Category:** 快速幂

**组件:**

- 若二进制最低位为1，res *= a
- 自乘 a *= a
- 右移 b >> 1

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef long long LL;
int n;

int main() {
    scanf("%d", &n);
    int a, b, p;
    while(n -- ) {
        scanf("%d%d%d", &a, &b, &p);
        int res = 1;
        while(b) {
            if(b & 1) res = (LL)res * a % p;
            a = (LL)a * a % p;
            b >>= 1;
        }
        printf("%d\n", res);
    }
    return 0;
}
```

