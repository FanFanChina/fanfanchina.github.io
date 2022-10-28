## 题目

[**筛质数**](https://www.acwing.com/problem/content/870/)

## 解析

**Category:** Number Theory

**朴素算法:**

- 将大于2的数先放入一个数组中去(因为最小的的质数为2)
- 如果没被筛掉，存入质数数组
- 从前往后筛去每个数的不同倍数的数

**埃氏算法:**

- 其实我们只需要筛选去质数的不同倍数的数即可
- 解决方法就是把循环放到判断里面去即可

**线性筛法:**

- 利用每个合数的最小质因子来筛去它本身
- 将大于2的数先放入一个数组中去(因为最小的的质数为2)
- 如果没被筛掉，存入质数数组
- 循环枚举所有的质数，筛去所有的primes[j] * i，直到i能整除primes[j]

## 代码

```cpp
// 朴素算法 O(nlogn)
#include <bits/stdc++.h>
using namespace std;

const int N = 1e6 + 10;
int primes[N], cnt;
bool st[N];

void getPrimes(int n) {
    for(int i = 2; i <= n; i ++ ) {
        // 没被筛掉，存入质数数组
        if(!st[i]) primes[cnt ++ ] = i;
        // 筛去i的不同倍数的合数
        for(int j = i; j <= n; j += i ) st[j] = true;
    }
}

int main() {
    int n;
    scanf("%d", &n);
    getPrimes(n);
    printf("%d", cnt);
    return 0;
}
```

```cpp
// 埃氏算法 O(nlog(log(n))
#include <bits/stdc++.h>
using namespace std;

const int N = 1e6 + 10;
int primes[N], cnt;
bool st[N];

void getPrimes(int n) {
    for(int i = 2; i <= n; i ++ ) {
        if(!st[i]) {
            primes[cnt ++ ] = i;
            for(int j = i; j <= n; j += i ) st[j] = true;
        }
    }
}

int main() {
    int n;
    scanf("%d", &n);
    getPrimes(n);
    printf("%d", cnt);
    return 0;
}
```

```cpp
// 线性筛法
#include <bits/stdc++.h>
using namespace std;

const int N = 1e6 + 10;
int primes[N], cnt;
bool st[N];

void getPrimes(int n) {
    for(int i = 2; i <= n; i ++ ) {
        if(!st[i]) primes[cnt ++ ] = i;
        for(int j = 0; primes[j] <= n / i; j ++ ) {
            st[primes[j] * i] = true;
            if(i % primes[j] == 0) break;
        }
    }
}

int main() {
    int n;
    scanf("%d", &n);
    getPrimes(n);
    printf("%d", cnt);
    return 0;
}
```

