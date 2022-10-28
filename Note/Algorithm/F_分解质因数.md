## 题目

**[分解质因数](https://www.acwing.com/problem/content/description/869/)**

## 解析

**Category:** Number Theory

**算术基本定理:** 不考虑排列顺序的情况下，每个正整数都能够以唯一的方式表示成它的质因数的乘积，例如: n=p1^a1 * p2^a2 *p3^a3.....pn^an

**步骤:**

- x 的质因子最多只包含一个大于 根号x 的质数。如果有两个，这两个因子的乘积就会大于 x，矛盾
- i 从 2 遍历到 根号x。 用 x / i，如果余数为 0，则 i 是一个质因子
- s 表示质因子 i 的指数，x /= i 为 0，则 s++， x = x / i 
- 最后检查是否有大于 根号x 的质因子，如果有，输出

**循环里面的 i 一定是一个质数:** 假如 i 是一个合数，那么它一定可以分解成多个质因子相乘的形式，这多个质因子同时也是 a 的质因子且比 i 要小，而比 i 小的数在之前的循环过程中一定是被条件除完了的，所以 i 不可能是合数，只可能是质数

## 代码

```c++
#include <bits/stdc++.h>
using namespace std;

int n, t;

void divide(int x) {
    for(int i = 2; i <= x / i; i ++ ) {
        if(x % i == 0) {
            // i 为底数
            // s 为指数
            int s = 0;
            while(x % i == 0) x /= i, s ++;
            printf("%d %d\n", i, s);
        }
    }
    // 还有剩余，单独处理
    if(x > 1) printf("%d 1\n", x);
    printf("\n");
}

int main() {
    scanf("%d", &n);
    while (n -- ) {
        scanf("%d", &t);
        divide(t);
    }
    return 0;
}
```

