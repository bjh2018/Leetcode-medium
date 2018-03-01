Container With Most Water
====

1.问题描述
----

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.<br> 
Note: You may not slant the container and n is at least 2. <br>
给定n个非负整数a1，a2，...，an，其中每个代表坐标（i，ai）处的一个点。 绘制n条垂直线，使得线i的两个端点处于（i，ai）和（i，0）处。 找到两条线，它们与x轴一起形成一个容器，以使容器包含最多的水。<br>
注意：不得倾斜容器，并且n至少为2。<br>

2.思路
---

求构成的容器的最大容量，其实就是求两条直线与x轴未征得面积，其中高要区两者中较小的，宽是两条直线间的距离，求最大的就要从最小的宽开始找，然后不断的增加宽的长度，按照这种思路，就下厨了第一种代码。


3.代码I（超时）
----

```c
int maxArea(int* height, int heightSize) {
    long long v=0;
    long long max=0;
    for (int i=0; i<heightSize; i++) {
        for (int j=i+1; j<heightSize; j++) {
            int h=height[i]>height[j]?height[j]:height[i];
            v=(j-i)*h;
            if (v>max) {
                max=v;
            }
        }
    }
    return (int)max;
}
```

4.代码II
---

```c
int max (int x, int y) {
    if (x>y) return x;
    else return y;
}
int min (int x, int y) {
    if (x>y) return y;
    else return x;
}
int maxArea(int* height, int heightSize) {
    int maxarea = 0, l = 0, r = heightSize - 1;
        while (l < r) {
            maxarea = max(maxarea, min(height[l], height[r]) * (r - l));
            if (height[l] < height[r])
                l++;
            else
                r--;
        }
        return maxarea;
}
```

这个代码是把宽从最大减小到1，并且在减小款的过程中不断地使所能得到的高最大，最后当宽为1时，高也取到该情况下的最大值，就可以使面积最大。
