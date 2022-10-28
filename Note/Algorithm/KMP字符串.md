## 题目

[**KMP字符串**](https://www.acwing.com/problem/content/833/)

## 解析
>  一个人能走的多远不在于他在顺境时能走的多快，而在于他在逆境时多久能找到曾经的自己                                            —— KMP

KMP其实是对暴力算法的优化

**组件:**

- 求Next数组

    - 如果已经匹配过一段了，但是当前位置匹配不成功，Slide
    - 当前位置匹配成功，Keep Going
    - 更新 next 数组

- KMP 匹配算法

    - 如果已经匹配过一段了，但是当前位置匹配不成功，Slide

    - 当前位置匹配成功，Keep Going

    - 匹配完毕, 输出 + 继续匹配 + Slide

## 代码

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 100010, M = 1000010;

int n, m;
char p[N], s[M];
int ne[N];

int main() {
    cin >> n >> p + 1 >> m >> s + 1;
    // 求next数组
    for(int i = 2, j = 0; i <= n; i ++ ) {
        while(j && p[i] != p[j + 1]) j = ne[j];
        if(p[i] == p[j + 1]) j ++ ;
        ne[i] = j;
    }
    // KMP匹配
    for(int i = 1, j = 0; i <= m; i ++ ) {
        // 如果已经匹配过一段了，但是当前位置匹配不成功，Slide
        while(j && s[i] != p[j + 1]) j = ne[j];
        // 当前位置匹配成功，Keep Going
        if(s[i] == p[j + 1]) j ++ ;
        // 匹配完毕
        if(j == n) {
            // 输出起始位点(下标从0开始)
            printf("%d ", i - n);
            // 继续匹配, Slide  
            j = ne[j];
        }
    }
    return 0;
}
```

## Mistake History

- char ne[N]
