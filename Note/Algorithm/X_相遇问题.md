## 题目
[相遇问题](https://matiji.net/exam/brushquestion/60/4009/C448715ED43BEA9D2D47CED523050945)
## 解析
**Category:** Number Theory

**步骤:**
- 求A和B到达每一段的终点的时间ta和tb
- for循环找到A和B相遇的路段，条件为(ta[i] <= tb[i] && ta[i + 1] >= tb[i - 1])
- 先到的等待后到的，然后一起走，时间为|Sa - Sb| / (Ai + Bi)

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 1e6 + 10;

// 路段
int x[N];
// 每段的A、B的最大速度
int A[N], B[N];
// A、B到达每段终点的时间
double ta[N], tb[N];
int n;

int main() {
	// 读入
	cin >> n;
	for(int i = 0; i <= n; i ++ ) cin >> x[i];
	for(int i = 1; i <= n; i ++ ) cin >> A[i];
	for(int i = 1; i <= n; i ++ ) cin >> B[i];
	// 求ta和tb
	for(int i = 1; i <= n; i ++ ) ta[i] = ta[i - 1] + (double)(x[i] - x[i - 1]) / A[i];
	for(int i = n - 1; i >= 0; i -- ) tb[i] = tb[i + 1] + (double)(x[i + 1] - x[i]) / B[i + 1];
	double ans = 0;
	for(int i = 1; i <= n; i ++ )
		// 找到相遇路段
		if(ta[i] <= tb[i] && ta[i + 1] >= tb[i + 1])
			ans = (x[i] - x[i - 1] + ta[i - 1] * A[i] + tb[i] * B[i]) / (A[i] + B[i]);
	printf("%.2lf\n", ans);
	return 0;
}
```
