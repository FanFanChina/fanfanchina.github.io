## 题目

[**试除法判定质数**](https://www.acwing.com/problem/content/description/868/)

## 解析

**Category:** Number Theory

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, t;

bool isPrime(int x) {
    // 最小的质数为2，若小于2，返回false
    if(x < 2) return false;
    // 只用枚举到sqrt(x)即可，即 i * i <= x
    // 为了防止数据越界，乘法变除法
    for(int i = 2; i <= x / i; i ++ ) {
        if(x % i == 0) return false;
    }
    return true;
}

int main() {
    cin >> n;
    while(n -- ) {
        cin >> t;
        if(isPrime(t)) printf("Yes\n");
        else printf("No\n");
    }
    return 0;
}
```

