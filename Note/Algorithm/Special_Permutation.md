## 题目

**[Special Permutation](https://codeforces.com/problemset/problem/1352/G)**

## 解析

**Category:** Constructive Algorithm

要使相邻数的差值处于2到4之间，我们先考虑一下特殊情况，相邻奇数或偶数的差值为二恰好满足题目要求，我们只需要在奇数和偶数的枚举之间加一些数字的翻转一保证相邻数的差值处于2到4之间即可，这里我们使奇数倒序排列，偶数升序排列，不过需要将偶数序列的前两位置换位置

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

int t, n;

int main() {
    cin >> t;
    while(t -- ) {
        cin >> n;
        if(n < 4) {
            cout << "-1" << endl;
            continue;
        }
        for(int i = n; i >= 1; i -- ) if(i & 1) cout << i << ' ';
        cout << '4' << ' ' << '2' << ' ';
        for(int i = 6; i <= n; i += 2) cout << i << ' ';
        cout << endl;
    }
    return 0;
}
```

