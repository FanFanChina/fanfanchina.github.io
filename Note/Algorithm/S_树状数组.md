## 引言

**树状数组:** 用数组模拟树形结构, 在存储值和修改值时以树形结构确定修改位置, 多用于动态区间求和以及区间查询问题

![](https://cdn.jsdelivr.net/gh/FanFanChina/StaticFiles/images/7.png)

## 组件

- **lowBit函数:** 求x的二进制表示的最低位1代表的数
- **add函数:** 创建和更新树状数组
- **sum函数:** 对[0 - x] 区间进行求和

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 10;
int tr[N], n, m, t;

int lowBit(int x) {
    return x & -x;
}

void add(int x, int v) {
    for(int i = x; i <= n; i += lowBit(i)) tr[i] += v;
}

int sum(int x) {
    int res = 0;
    for(int i = x; i; i -= lowBit(i)) res += tr[i];
    return res;
}

int main() {
    scanf("%d%d", &n, &m);
    for(int i = 1; i <= n; i ++ ) scanf("%d", &t), add(i, t);
    int a, b, c;
    while(m -- ) {
        scanf("%d%d%d", &a, &b, &c);
        if(a == 0) printf("%d\n", sum(c) - sum(b - 1));
        else add(b, c);
    }
    return 0;
}
```

