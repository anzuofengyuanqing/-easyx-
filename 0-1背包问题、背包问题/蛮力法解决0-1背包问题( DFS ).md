
```C
/**
使用蛮力法解决0/1背包问题（DFS遍历）
*/
#include<stdio.h>
#define N 100

```
```C

typedef struct {
	int wight;
	int value;
}Goods;

int n, bestValue, cv, cw, C;//物品数量，价值最大，当前价值，当前重量，背包容量
int X[N], cx[N];//最终存储状态，当前存储状态
Goods goods[N];//定义物品数组

```
```C

//递归实现深度优先遍历
int M_Dfs(int i) {
	if (i > n - 1) {
		if (bestValue < cv && cw <= C) {
			for (int k = 0; k < n; k++)
				X[k] = cx[k];//存储最优路径
			bestValue = cv;
		} 
		return bestValue;
	}
	//装入背包
	cw = cw + goods[i].wight;
	cv = cv + goods[i].value;
	cx[i] = 1;
	M_Dfs(i + 1);
	//不装入背包
	cw = cw - goods[i].wight;
	cv = cv - goods[i].value;
	cx[i] = 0;
	M_Dfs(i + 1);
	return bestValue;
}

```
```C

int main()
{
	//输入
	printf("物品种类n：");
	scanf_s("%d", &n);
	printf("背包容量C：");
	scanf_s("%d", &C);
	for (int i = 0; i < n; i++) {
		printf("物品%d的重量w[%d]及其价值v[%d]：", i + 1, i + 1, i + 1);
		scanf_s("%d%d", &goods[i].wight, &goods[i].value);
	}
	//核心算法
	int sum = M_Dfs(0);
	//输出
	printf("蛮力法求解0/1背包问题：\n 所有物品的状态: X=[");
	for (int i = 0; i < n; i++) {
		printf("%d ", X[i]) ;
	}
	printf("] 装入总价值%d :   \n", sum);
	getchar();
	return 0;
}

```
