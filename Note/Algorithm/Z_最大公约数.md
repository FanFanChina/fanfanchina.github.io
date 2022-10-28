## 题目

**[最大公约数](https://www.acwing.com/problem/content/874/)**

## 解析

**Category:** 最大公约数

## 代码

```c++
#include <bits/stdc++.h>
using namespace std;

int n;

int gcd(int a, int b) {
    return  b ? gcd(b, a % b) : a;
}

int main() {
    scanf("%d", &n);
    while(n -- ) {
        int a, b;
        scanf("%d%d", &a, &b);
        printf("%d\n", gcd(a, b));
    }
}
```