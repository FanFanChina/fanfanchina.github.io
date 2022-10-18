## 题目

[码蹄杯复赛](https://matiji.net/exam/contest/contestdetail/62)

## 解析

## 代码

```cpp
#include<iostream>
#include<algorithm>
using namespace std;

const int N = 1e5 + 10;
long long int a[N], s[N];
long long int n;
long long int k;

long long int calcu(long long int x) {
    return a[x] * x - s[x];
}

int main() {
    scanf("%lld%lld",&n,&k);
    for (int i = 1; i <= n; i++) scanf("%lld",&a[i]);
    sort(a + 1, a + n + 1);
    for (int i = 1; i <= n; i++)
        s[i] = a[i] + s[i - 1];
    int l = 0, r = n + 1;
    while (l + 1 != r) {
        int mid = l + r >> 1;
        if (calcu(mid) <= k)
            l = mid;
        else
            r = mid;
    }
    k -= (l * a[l] - s[l]);
    k /= l;
    k += a[l];
    printf("%lld",k);
    return 0;
}
```
