Triangle
===

1.问题描述
---

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.<br>
For example, given the following triangle<br>
[<br>
     [2],  <br>
    [3,4], <br>
   [6,5,7],<br>
  [4,1,8,3]<br>
]<br>

The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11). <br>
Note:<br>
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.<br>
给定一个二维数组，二维数组可以按照三角形的形状排列，从第一个开始，只能跟下一行与第一个数相邻的数相加，求整个过程中的最小值。

2.思路
---

一开始打算每加一个数，就取一次最小值，得出最终的结果，但在运行过程中发现这样不一定能取得最小值，因为当你对上一组取完最小值之后，它能加的数就只能局限在
两个数之间，这样最终结果不一定最小，但是如果倒着对数组中的元素进行改变就会不同，比如要改变倒数第二行的的值，就要加上最后一行与其相邻的两个数的最小值，
这样就可以把每行有限制的结果都可以得出来进行比较。

3.代码
---

```c
int min(int x, int y) {
    if (x>y) return y;
    else return x;
}
int minimumTotal(int** triangle, int triangleRowSize, int *triangleColSizes) {
    for (int i=triangleRowSize-2; i>=0; i--) {
        for (int j=0; j<triangleColSizes[i]; j++) {//因为上一行的元素个数一定小于下一行，尽管下面j要加1，也依然可以
            triangle[i][j]+=min(triangle[i+1][j],triangle[i+1][j+1]);
        }
    }
    return triangle[0][0];
}
```

4.总结
---

如果取最值时，正向有限制的话，可以考虑从反向来解决。
