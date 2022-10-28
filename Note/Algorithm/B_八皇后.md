## 题目

****[P1219 [USACO1.5]八皇后 Checker Challenge](https://www.luogu.com.cn/problem/P1219)****

## 解析

**Category:** DFS

这是一道经典的深度搜索题目，从第一行往下依次放入棋子（这样一定不会同行）

同一列、左斜和右斜用数组记录有没有被标记

- 列：i
- 左斜： r - i + n （这里不能用绝对值，会导致其对称左斜也会被标记，所以使用偏移量）
- 右斜：r + i

## 代码

```cpp
#include <iostream>
using namespace std;

const int N = 20;
int a[N];
bool l[N];       // list
bool obl[N * 2]; // oblique left(因为判定条件是r - i + n, 防止越界所以翻倍)
bool obr[N * 2]; // oblique right(因为判定条件是r + i, 防止越界所以翻倍)

int n, ans;

void show() {
    if (ans <= 3) {
        for (int i = 1; i <= n; i++)
            cout << a[i] << ' ';
        cout << endl;
    }
}

void dfs(int r) {
    if (r == n + 1) {
        ans++;
        show();
        return;
    }
    for (int i = 1; i <= n; i++) {
        if(l[i] == false && obl[r - i + n] == false && obr[i + r] == false) {
            a[r] = i;
            l[i] = obl[r - i + n] = obr[i + r] = true;
            dfs(r + 1);
            l[i] = obl[r - i + n] = obr[i + r] = false;
        }
    }
    return;
}

int main() {
    cin >> n;
    dfs(1);
    cout << ans;
    return 0;
}
```

## Mistake History

- a[i] = i;