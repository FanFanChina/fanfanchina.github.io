## 题目

[**高精度加法**](https://www.acwing.com/problem/content/793/)

## 解析

**Category:** Number Theory

**Steps:**

- 字符串读入，倒序转换
- 锋十进一，循环完后仍有进位则push_back(1)
- 倒序输出答案

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

vector <int> add(vector <int> &A, vector <int> &B) {
    vector <int> C;
    int t = 0;
    for(int i = 0; i < A.size() || i < B.size(); i ++ ) {
        if(i < A.size()) t += A[i];
        if(i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }
    if(t) C.push_back(1);
    return C;
}

int main() {
    string a, b;
    vector <int> A, B;
    cin >> a >> b;
    // 倒序转换
    for(int i = a.size() - 1; i >= 0; i -- ) A.push_back(a[i] - '0');
    for(int i = b.size() - 1; i >= 0; i -- ) B.push_back(b[i] - '0');
    // 计算
    auto C = add(A, B);
    // 倒序输出
    for(int i = C.size() - 1; i >= 0; i -- ) printf("%d", C[i]);
    return 0;
}
```

