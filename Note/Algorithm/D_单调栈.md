## 题目

**[单调栈](https://www.acwing.com/problem/content/832/)**

## 解析

**Category:** 单调栈

这是一道简单的单调栈模板题

原理：当序列中存在 Ax  > Ay (x < y)时，对于下标为大于y的A来说，Ax永远不可能是答案，所以我们可以将其删去，最终栈中是一个严格单调递增的序列

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 100010;
int n;
int stk[N], tt;

int main() {
    scanf("%d", &n);
    for(int i = 1; i <= n; i ++ ) {
        int x;
        scanf("%d", &x);
        // 如果栈中有值，且栈顶元素值大于x，删去栈顶元素
        while(tt && stk[tt] >= x) tt --;
        // 如果栈中有值，此时栈顶元素值小于x，输出stk[tt]
        if(tt) printf("%d ", stk[tt]);
        // 栈内无元素，输出-1
        else printf("-1 ");
        // x 入栈
        stk[++tt] = x;
    }
    return 0;
}
```

## Mistake History

- ```c++
    if(tt && stk[tt] >= x) tt --;
    ```

