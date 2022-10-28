## 题目

[**差分**](https://www.acwing.com/problem/content/799/)

## 解析

差分其实是对前缀和的逆运算

**步骤:**

- 构造原数组A的差分数组B(A是B的前缀和数组)

- 将A数组的区间操作转化为B数组的端点操作

**原理:** 因为A是B的前缀和数组，对B[i]加上一个数c后A数组中A[i - n] 都会被加上c

## 代码

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 10;
int a[N], b[N];
int n, m;

void insert(int l, int r, int c) {
    b[l] += c;
    b[r + 1] -= c;
}

int main() {
    scanf("%d%d", &n, &m);
    // 读入并构建差分数组
    for(int i = 1; i <= n; i ++ ) scanf("%d", &a[i]), insert(i, i, a[i]);
    // 区间操作
    while(m -- ) {
        int l, r, c;
        scanf("%d%d%d", &l, &r, &c);
        insert(l, r, c);
    }
    // 直接在b数组上求前缀和
    for(int i = 1; i <= n; i ++ ) b[i] += b[i - 1], printf("%d ", b[i]);
    return 0;
}
```
